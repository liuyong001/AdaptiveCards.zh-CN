---
title: 扩展性-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 07/16/2020
ms.topic: article
ms.openlocfilehash: 96da071980b8cf41b616297c44c70d181a4f6ac0
ms.sourcegitcommit: 65b792d73c264c943036343e05b75f2b0488e6e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "95001844"
---
# <a name="extensibility---javascript"></a>扩展性-JavaScript

## <a name="extensibility-with-the-js-sdk-version-20-and-greater"></a>适用于 JS SDK 版本2.0 及更高版本的扩展性

### <a name="before-you-start"></a>开始之前

> **重要提示**： JS SDK 2.0 和更高版本利用了 [TypeScript 修饰器](https://www.typescriptlang.org/docs/handbook/decorators.html)。 修饰器仍为实验功能，并且必须在文件中显式启用 `tsconfig.js` ：

```json
{
   "compilerOptions": {
       "experimentalDecorators": true
   }
}
```
2.0 版的 JS SDK 引入了自定义元素和操作的实现和注册方式的重大更改。 有关如何使用以前版本的 SDK 实现和注册元素或操作的示例，请参阅 [2.0 版之前的 JS SDK 扩展性](#extensibility-with-the-js-sdk-prior-to-version-20)。


### <a name="custom-elements"></a>自定义元素
创建自定义自适应卡元素类型的步骤如下：
- 创建一个派生自的新类 `CardElement`
- 通过声明静态属性定义创建其架构
- 实现其 `getJsonTypeName` 和 `internalRender` 方法
- 在全局元素注册表中注册它，或在每个卡上使用自定义注册表


我们来看一个示例并实现一个简单的进度栏元素：
```typescript
export class ProgressBar extends AC.CardElement {
    static readonly JsonTypeName = "ProgressBar";

    //#region Schema

    static readonly titleProperty = new AC.StringProperty(AC.Versions.v1_0, "title", true);
    static readonly valueProperty = new AC.NumProperty(AC.Versions.v1_0, "value");

    @AC.property(ProgressBar.titleProperty)
    get title(): string | undefined {
        return this.getValue(ProgressBar.titleProperty);
    }

    set title(value: string) {
        if (this.title !== value) {
            this.setValue(ProgressBar.titleProperty, value);

            this.updateLayout();
        }
    }

    @AC.property(ProgressBar.valueProperty)
    get value(): number {
        return this.getValue(ProgressBar.valueProperty);
    }

    set value(value: number) {
        let adjustedValue = value;

        if (adjustedValue < 0) {
            adjustedValue = 0;
        }
        else if (adjustedValue > 100) {
            adjustedValue = 100;
        }

        if (this.value !== adjustedValue) {
            this.setValue(ProgressBar.valueProperty, adjustedValue);

            this.updateLayout();
        }
    }

    //#endregion

    private _titleElement: HTMLElement;
    private _leftBarElement: HTMLElement;
    private _rightBarElement: HTMLElement;

    protected internalRender(): HTMLElement {
        let element = document.createElement("div");

        let textBlock = new AC.TextBlock();
        textBlock.setParent(this);
        textBlock.text = this.title;
        textBlock.wrap = true;

        this._titleElement = textBlock.render();
        this._titleElement.style.marginBottom = "6px";

        let progressBarElement = document.createElement("div");
        progressBarElement.style.display = "flex";

        this._leftBarElement = document.createElement("div");
        this._leftBarElement.style.height = "6px";
        this._leftBarElement.style.backgroundColor = AC.stringToCssColor(this.hostConfig.containerStyles.emphasis.foregroundColors.accent.default);

        this._rightBarElement = document.createElement("div");
        this._rightBarElement.style.height = "6px";
        this._rightBarElement.style.backgroundColor = AC.stringToCssColor(this.hostConfig.containerStyles.emphasis.backgroundColor);

        progressBarElement.append(this._leftBarElement, this._rightBarElement);

        element.append(this._titleElement, progressBarElement);

        return element;
    }

    getJsonTypeName(): string {
        return ProgressBar.JsonTypeName;
    }

    updateLayout(processChildren: boolean = true) {
        super.updateLayout(processChildren);

        if (this.renderedElement) {
            if (this.title) {
                this._titleElement.style.display = "none";
            }
            else {
                this._titleElement.style.removeProperty("display");
            }

            this._leftBarElement.style.flex = "1 1 " + this.value + "%";
            this._rightBarElement.style.flex = "1 1 " + (100 - this.value) + "%";
        }
    }
}
```
就是这样。 现在需要注册 ProgressBar 元素，才能被 SDK 识别。 可以全局注册：

```typescript
AC.GlobalRegistry.elements.register(ProgressBar.JsonTypeName, ProgressBar);
```

或者，你可以使用每个卡的注册表，这允许在你的应用程序中使用不同的注册表项：

```typescript
// Create a custom registry for elements
let elementRegistry = new AC.CardObjectRegistry<AC.CardElement>();

// Populate it with the default set of elements
AC.GlobalRegistry.populateWithDefaultElements(elementRegistry);

// Register the custom ProgressBar element
elementRegistry.register(ProgressBar.JsonTypeName, ProgressBar);

// Parse a card payload using the custom registry
let serializationContext = new AC.SerializationContext();
serializationContext.setElementRegistry(elementRegistry);

let card = new AC.AdaptiveCard();
card.parse(
    {
        type: "AdaptiveCard",
        version: "1.0",
        body: [
            {
                type: "ProgressBar",
                title: "This is a progress bar",
                value: 45
            }
        ]
    },
    serializationContext
);
```

### <a name="custom-inputs"></a>自定义输入
输入是专用于收集最终用户输入的数据的一种特殊类型的元素，随后可以将该数据作为参数传递给操作。

当涉及到输入时，自适应卡 1.x SDK 的版本2.x 中引入了两个值得注意的更改：
- **输入验证：** 现提供内置输入验证机制，可自动处理验证错误，包括视觉提示
- **辅助功能改进：** 内置输入可以更好地支持辅助功能

因此，实现自定义输入需要比实现简单元素稍微多一些逻辑。 下表列出了自定义输入实现为了 partiocipate 输入验证机制并可访问而应实现的所有方法：

| 方法 | 说明 |
| --------- | ------------- |
| `protected updateInputControlAriaLabelledBy()` | 此方法在输入验证序列过程中调用。 如果输入未通过验证，则会显示其关联的错误消息，并且需要更新基础输入控件的属性，以使 `aria-labelledby` 输入符合辅助功能要求。 自定义输入应重写 `updateInputControlAriaLabelledBy` ，以将相应的属性应用于 `aria-labelledby` 基础输入控件。 `getAllLabelIds(): string[]`方法可用于检索应在属性中指定的所有标签的 id `aria-labelledby` 。  |
| `protected internalRender(): HTMLElement` | 与任何其他自适应卡自定义元素一样， `internalRender` 必须重写以根据需要呈现输入。 这是要在其中创建实际基础输入控件的位置。 |
| `protected get isNullable(): boolean` | 指示输入是否支持 (实例的未定义值，例如 Input。 Text 确实如此，而 Input 却不支持。 ) 自定义输入应重写此属性 getter 以指示它们是否支持未定义的值。 基实现返回 `true` 。 |
| `public focus()` | 当遇到验证错误时，焦点将自动放置在验证失败的第一个输入上。 `focus`在某些情况下，的基实现将适用于自定义输入。 如果不是这种情况，自定义输入控件必须重写， `focus` 以显式将焦点放在基础输入控件上。  |
| `public abstract isSet(): boolean` | 指示输入的值是否已由用户设置。 在输入验证序列过程中调用此方法，以确定输入是通过还是未通过验证。 为了加入输入验证机制，自定义输入必须重写 `isSet` 。 |
| `public isValid(): boolean` | 指示输入的值是否有效。 在输入验证序列过程中调用此方法，以确定输入是通过还是未通过验证。 为了加入输入验证机制，应重写自定义输入 `isValid` 。 基实现返回 `true` 。 |
| `public abstract get value(): any` | 返回输入值。 自定义输入必须重写此，以便从基础输入控件检索输入值。 |


### <a name="custom-actions"></a>自定义操作
实现自定义操作的步骤与元素的步骤相同。 唯一的区别在于操作注册在操作注册表中，而不是在元素注册表中注册。

```typescript
export class AlertAction extends AC.Action {
    static readonly JsonTypeName = "Action.Alert";

    //#region Schema

    static readonly textProperty = new AC.StringProperty(AC.Versions.v1_0, "text", true);

    @AC.property(AlertAction.textProperty)
    text?: string;

    //#endregion

    getJsonTypeName(): string {
        return AlertAction.JsonTypeName;
    }

    execute() {
        alert(this.text);
    }
}
```

全局注册新操作：
```typescript
AC.GlobalRegistry.actions.register(AlertAction.JsonTypeName, AlertAction);
```

或使用每个卡的注册表：
```typescript
// Create a custom registry for actions
let actionRegistry = new AC.CardObjectRegistry<AC.Action>();

// Populate it with the default set of actions
AC.GlobalRegistry.populateWithDefaultActions(actionRegistry);

// Register the custom AlertAction type
actionRegistry.register(AlertAction.JsonTypeName, AlertAction);

// Parse a card payload using the custom registry
let serializationContext = new AC.SerializationContext();
serializationContext.setActionRegistry(actionRegistry);

let card = new AC.AdaptiveCard();
card.parse(
    {
        type: "AdaptiveCard",
        version: "1.0",
        body: [
            {
                type: "TextBlock",
                text: "This demonstrates the AlertAction action."
            }
        ],
        actions: [
            {
                type: "Action.Alert",
                title: "Click me!",
                text: "Hello World"
            }
        ]
    },
    serializationContext
);
```

## <a name="extensibility-with-the-js-sdk-prior-to-version-20"></a>2.0 版之前的 JS SDK 可扩展性

### <a name="custom-elements"></a>自定义元素

### <a name="before-you-start"></a>开始之前

> **重要提示**： JS SDK 2.0 和更高版本利用了 [TypeScript 修饰器](https://www.typescriptlang.org/docs/handbook/decorators.html)。 修饰器仍为实验功能，并且必须在文件中显式启用 `tsconfig.js` ：

```json
{
   "compilerOptions": {
       "experimentalDecorators": true
   }
}
```
2.0 版的 JS SDK 引入了自定义元素和操作的实现和注册方式的重大更改。 有关如何使用以前版本的 SDK 实现和注册元素或操作的示例，请参阅 [2.0 版之前的 JS SDK 扩展性](#extensibility-with-the-js-sdk-prior-to-version-20)。


### <a name="custom-elements"></a>自定义元素
创建自定义自适应卡元素类型的步骤如下：
- 创建一个派生自的新类 `CardElement`
- 通过声明静态属性定义创建其架构
- 实现其 `getJsonTypeName` 和 `internalRender` 方法
- 在全局元素注册表中注册它，或在每个卡上使用自定义注册表


我们来看一个示例并实现一个简单的进度栏元素：
```typescript
export class ProgressBar extends AC.CardElement {
    static readonly JsonTypeName = "ProgressBar";

    //#region Schema

    static readonly titleProperty = new AC.StringProperty(AC.Versions.v1_0, "title", true);
    static readonly valueProperty = new AC.NumProperty(AC.Versions.v1_0, "value");

    @AC.property(ProgressBar.titleProperty)
    get title(): string | undefined {
        return this.getValue(ProgressBar.titleProperty);
    }

    set title(value: string) {
        if (this.title !== value) {
            this.setValue(ProgressBar.titleProperty, value);

            this.updateLayout();
        }
    }

    @AC.property(ProgressBar.valueProperty)
    get value(): number {
        return this.getValue(ProgressBar.valueProperty);
    }

    set value(value: number) {
        let adjustedValue = value;

        if (adjustedValue < 0) {
            adjustedValue = 0;
        }
        else if (adjustedValue > 100) {
            adjustedValue = 100;
        }

        if (this.value !== adjustedValue) {
            this.setValue(ProgressBar.valueProperty, adjustedValue);

            this.updateLayout();
        }
    }

    //#endregion

    private _titleElement: HTMLElement;
    private _leftBarElement: HTMLElement;
    private _rightBarElement: HTMLElement;

    protected internalRender(): HTMLElement {
        let element = document.createElement("div");

        let textBlock = new AC.TextBlock();
        textBlock.setParent(this);
        textBlock.text = this.title;
        textBlock.wrap = true;

        this._titleElement = textBlock.render();
        this._titleElement.style.marginBottom = "6px";

        let progressBarElement = document.createElement("div");
        progressBarElement.style.display = "flex";

        this._leftBarElement = document.createElement("div");
        this._leftBarElement.style.height = "6px";
        this._leftBarElement.style.backgroundColor = AC.stringToCssColor(this.hostConfig.containerStyles.emphasis.foregroundColors.accent.default);

        this._rightBarElement = document.createElement("div");
        this._rightBarElement.style.height = "6px";
        this._rightBarElement.style.backgroundColor = AC.stringToCssColor(this.hostConfig.containerStyles.emphasis.backgroundColor);

        progressBarElement.append(this._leftBarElement, this._rightBarElement);

        element.append(this._titleElement, progressBarElement);

        return element;
    }

    getJsonTypeName(): string {
        return ProgressBar.JsonTypeName;
    }

    updateLayout(processChildren: boolean = true) {
        super.updateLayout(processChildren);

        if (this.renderedElement) {
            if (this.title) {
                this._titleElement.style.display = "none";
            }
            else {
                this._titleElement.style.removeProperty("display");
            }

            this._leftBarElement.style.flex = "1 1 " + this.value + "%";
            this._rightBarElement.style.flex = "1 1 " + (100 - this.value) + "%";
        }
    }
}
```
就是这样。 现在需要注册 ProgressBar 元素，才能被 SDK 识别。 可以全局注册：

```typescript
AC.GlobalRegistry.elements.register(ProgressBar.JsonTypeName, ProgressBar);
```

或者，你可以使用每个卡的注册表，这允许在你的应用程序中使用不同的注册表项：

```typescript
// Create a custom registry for elements
let elementRegistry = new AC.CardObjectRegistry<AC.CardElement>();

// Populate it with the default set of elements
AC.GlobalRegistry.populateWithDefaultElements(elementRegistry);

// Register the custom ProgressBar element
elementRegistry.register(ProgressBar.JsonTypeName, ProgressBar);

// Parse a card payload using the custom registry
let serializationContext = new AC.SerializationContext();
serializationContext.setElementRegistry(elementRegistry);

let card = new AC.AdaptiveCard();
card.parse(
    {
        type: "AdaptiveCard",
        version: "1.0",
        body: [
            {
                type: "ProgressBar",
                title: "This is a progress bar",
                value: 45
            }
        ]
    },
    serializationContext
);
```

### <a name="custom-actions"></a>自定义操作
实现自定义操作的步骤与元素的步骤相同。 唯一的区别在于操作注册在操作注册表中，而不是在元素注册表中注册。

```typescript
export class AlertAction extends AC.Action {
    static readonly JsonTypeName = "Action.Alert";

    //#region Schema

    static readonly textProperty = new AC.StringProperty(AC.Versions.v1_0, "text", true);

    @AC.property(AlertAction.textProperty)
    text?: string;

    //#endregion

    getJsonTypeName(): string {
        return AlertAction.JsonTypeName;
    }

    execute() {
        alert(this.text);
    }
}
```

全局注册新操作：
```typescript
AC.GlobalRegistry.actions.register(AlertAction.JsonTypeName, AlertAction);
```

或使用每个卡的注册表：
```typescript
// Create a custom registry for actions
let actionRegistry = new AC.CardObjectRegistry<AC.Action>();

// Populate it with the default set of actions
AC.GlobalRegistry.populateWithDefaultActions(actionRegistry);

// Register the custom AlertAction type
actionRegistry.register(AlertAction.JsonTypeName, AlertAction);

// Parse a card payload using the custom registry
let serializationContext = new AC.SerializationContext();
serializationContext.setActionRegistry(actionRegistry);

let card = new AC.AdaptiveCard();
card.parse(
    {
        type: "AdaptiveCard",
        version: "1.0",
        body: [
            {
                type: "TextBlock",
                text: "This demonstrates the AlertAction action."
            }
        ],
        actions: [
            {
                type: "Action.Alert",
                title: "Click me!",
                text: "Hello World"
            }
        ]
    },
    serializationContext
);
```

## <a name="extensibility-with-the-js-sdk-prior-to-version-20"></a>2.0 版之前的 JS SDK 可扩展性

### <a name="custom-elements"></a>自定义元素

创建自定义自适应卡元素类型的步骤如下：
- 创建一个派生自的新类 `CardElement`
- 实现其 `getJsonTypeName` 、 `parse` 、 `toJSON` `internalRender` 和 `renderSpeech` 方法
- 通过将其添加到呈现器的元素注册表来注册它

我们来看一个示例并实现一个简单的进度栏元素：

```typescript
import * as Adaptive from "adaptivecards";

export class ProgressBar extends Adaptive.CardElement {
    private _title: string;
    private _value: number = 0;
    private _titleElement: HTMLElement;
    private _leftBarElement: HTMLElement;
    private _rightBarElement: HTMLElement;

    protected internalRender(): HTMLElement {
        let element = document.createElement("div");

        let textBlock = new Adaptive.TextBlock();
        textBlock.setParent(this);
        textBlock.text = this.title;
        textBlock.wrap = true;

        this._titleElement = textBlock.render();
        this._titleElement.style.marginBottom = "6px";

        let progressBarElement = document.createElement("div");
        progressBarElement.style.display = "flex";

        this._leftBarElement = document.createElement("div");
        this._leftBarElement.style.height = "6px";
        this._leftBarElement.style.backgroundColor = Adaptive.stringToCssColor(this.hostConfig.containerStyles.emphasis.foregroundColors.accent.default);

        this._rightBarElement = document.createElement("div");
        this._rightBarElement.style.height = "6px";
        this._rightBarElement.style.backgroundColor = Adaptive.stringToCssColor(this.hostConfig.containerStyles.emphasis.backgroundColor);

        progressBarElement.append(this._leftBarElement, this._rightBarElement);

        element.append(this._titleElement, progressBarElement);

        return element;
    }

    getJsonTypeName(): string {
        return "ProgressBar";
    }

    toJSON(): any {
        let result = super.toJSON();

        Adaptive.setProperty(result, "title", this.title);
        Adaptive.setProperty(result, "value", this.value);

        return result;
    }

    parse(json: any, errors?: Array<Adaptive.IValidationError>) {
        super.parse(json, errors);

        this.title = Adaptive.getStringValueOrDefault(json["title"], undefined);
        this.value = Adaptive.getValueOrDefault(json["value"], this._value);
    }

    updateLayout(processChildren: boolean = true) {
        super.updateLayout(processChildren);

        if (this.renderedElement) {
            if (Adaptive.isNullOrEmpty(this.title)) {
                this._titleElement.style.display = "none";
            }
            else {
                this._titleElement.style.removeProperty("display");
            }

            this._leftBarElement.style.flex = "1 1 " + this.value + "%";
            this._rightBarElement.style.flex = "1 1 " + (100 - this.value) + "%";
        }
    }

    renderSpeech(): string {
        return (Adaptive.isNullOrEmpty(this.title) ? "Progress" : this.title) + " " + Math.ceil(this.value) + "%";
    }

    get title(): string {
        return this._title;
    }

    set title(value: string) {
        if (this._title !== value) {
            this._title = value;

            this.updateLayout();
        }
    }

    get value(): number {
        return this._value;
    }

    set value(value: number) {
        let adjustedValue = value;

        if (adjustedValue < 0) {
            adjustedValue = 0;
        }
        else if (adjustedValue > 100) {
            adjustedValue = 100;
        }

        if (this._value !== adjustedValue) {
            this._value = adjustedValue;

            this.updateLayout();
        }
    }
}
```

就是这样。 现在只需向呈现器注册进度栏类：

```typescript
Adaptive.AdaptiveCard.elementTypeRegistry.registerType("ProgressBar", () => { return new ProgressBar(); });
```

## <a name="custom-actions"></a>自定义操作

创建自定义自适应卡操作的步骤实质上与自定义元素的步骤相同。 下面是一个简单的警报操作示例，只显示具有可配置文本的消息框：

```typescript
import * as Adaptive from "adaptivecards";

export class AlertAction extends Adaptive.Action {
    text: string;

    getJsonTypeName(): string {
        return "Action.ALert";
    }

    execute() {
        alert(this.text);
    }

    parse(json: any) {
        super.parse(json);

        this.text = Adaptive.getStringValueOrDefault(json["text"], "Alert!");
    }

    toJSON() {
        let result = super.toJSON();

        Adaptive.setProperty(result, "text", this.text);

        return result;
    }
}
```

现在，注册新操作：

```typescript
Adaptive.AdaptiveCard.actionTypeRegistry.registerType("Action.Alert", () => { return new AlertAction(); });
```

## <a name="example"></a>示例

下面是一个示例卡，它使用 ProgressBar 元素和 AlertAction 操作：
```json
{
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "Custom ProgressBar element"
        },
        {
            "type": "ProgressBar",
            "title": "Please wait...",
            "value": 10
        }
    ],
    "actions": [
        {
            "type": "Action.Alert",
            "title": "Click me",
            "text": "Hello world!"
        }
    ]
}
```

下面是它的呈现方式： ![ 图像](https://user-images.githubusercontent.com/1334689/52665466-8155e780-2ec0-11e9-841a-7d272ad1d103.png)
