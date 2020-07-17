---
title: 扩展性-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 07/16/2020
ms.topic: article
ms.openlocfilehash: 81c60e200d2fcbc844a3ae3f4fdefa0ddaa399d3
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417538"
---
# <a name="extensibility---javascript"></a><span data-ttu-id="a1427-102">扩展性-JavaScript</span><span class="sxs-lookup"><span data-stu-id="a1427-102">Extensibility - JavaScript</span></span>

## <a name="extensibility-with-the-js-sdk-version-20-and-greater"></a><span data-ttu-id="a1427-103">适用于 JS SDK 版本2.0 及更高版本的扩展性</span><span class="sxs-lookup"><span data-stu-id="a1427-103">Extensibility with the JS SDK version 2.0 and greater</span></span>

### <a name="before-you-start"></a><span data-ttu-id="a1427-104">开始之前</span><span class="sxs-lookup"><span data-stu-id="a1427-104">Before you start</span></span>

> <span data-ttu-id="a1427-105">**重要提示**： JS SDK 2.0 和更高版本利用了[TypeScript 修饰器](https://www.typescriptlang.org/docs/handbook/decorators.html)。</span><span class="sxs-lookup"><span data-stu-id="a1427-105">**IMPORTANT**: Version 2.0 and greater of the JS SDK makes use of [TypeScript decorators](https://www.typescriptlang.org/docs/handbook/decorators.html).</span></span> <span data-ttu-id="a1427-106">修饰器仍为实验功能，并且必须在文件中显式启用 `tsconfig.js` ：</span><span class="sxs-lookup"><span data-stu-id="a1427-106">Decorators are still an experimental feature and must be explicitly enabled in your `tsconfig.js` file:</span></span>

```json
{
   "compilerOptions": {
       "experimentalDecorators": true
   }
}
```
<span data-ttu-id="a1427-107">2.0 版的 JS SDK 引入了自定义元素和操作的实现和注册方式的重大更改。</span><span class="sxs-lookup"><span data-stu-id="a1427-107">Version 2.0 of the JS SDK introduces breaking changes in the way custom elements and actions are implemented and registered.</span></span> <span data-ttu-id="a1427-108">有关如何使用以前版本的 SDK 实现和注册元素或操作的示例，请参阅[2.0 版之前的 JS SDK 扩展性](#extensibility-with-the-js-sdk-prior-to-version-20)。</span><span class="sxs-lookup"><span data-stu-id="a1427-108">For an example on how to implement and register an element or action using previous versions of the SDK, see [Extensibility with the JS SDK prior to version 2.0](#extensibility-with-the-js-sdk-prior-to-version-20).</span></span>


### <a name="custom-elements"></a><span data-ttu-id="a1427-109">自定义元素</span><span class="sxs-lookup"><span data-stu-id="a1427-109">Custom elements</span></span>
<span data-ttu-id="a1427-110">创建自定义自适应卡元素类型的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="a1427-110">The steps for creating a custom Adaptive Card element type are:</span></span>
- <span data-ttu-id="a1427-111">创建一个派生自的新类`CardElement`</span><span class="sxs-lookup"><span data-stu-id="a1427-111">Create a new class deriving from `CardElement`</span></span>
- <span data-ttu-id="a1427-112">通过声明静态属性定义创建其架构</span><span class="sxs-lookup"><span data-stu-id="a1427-112">Create its schema by declaring static property definitions</span></span>
- <span data-ttu-id="a1427-113">实现其 `getJsonTypeName` 和 `internalRender` 方法</span><span class="sxs-lookup"><span data-stu-id="a1427-113">Implement its `getJsonTypeName`, and `internalRender` methods</span></span>
- <span data-ttu-id="a1427-114">在全局元素注册表中注册它，或在每个卡上使用自定义注册表</span><span class="sxs-lookup"><span data-stu-id="a1427-114">Register it in the global element registry, or use a custom registry on a per-card basis</span></span>


<span data-ttu-id="a1427-115">我们来看一个示例并实现一个简单的进度栏元素：</span><span class="sxs-lookup"><span data-stu-id="a1427-115">Let's take an example and implement a simple Progress Bar element:</span></span>
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
<span data-ttu-id="a1427-116">就是这样。</span><span class="sxs-lookup"><span data-stu-id="a1427-116">That's it.</span></span> <span data-ttu-id="a1427-117">现在需要注册 ProgressBar 元素，才能被 SDK 识别。</span><span class="sxs-lookup"><span data-stu-id="a1427-117">The ProgressBar element now needs to be registered in order to be recognized by the SDK.</span></span> <span data-ttu-id="a1427-118">可以全局注册：</span><span class="sxs-lookup"><span data-stu-id="a1427-118">You can register it globally:</span></span>

```typescript
AC.GlobalRegistry.elements.register(ProgressBar.JsonTypeName, ProgressBar);
```

<span data-ttu-id="a1427-119">或者，你可以使用每个卡的注册表，这允许在你的应用程序中使用不同的注册表项：</span><span class="sxs-lookup"><span data-stu-id="a1427-119">Or you can use a per-card registry, which allows the use of different registries for different cards in your application:</span></span>

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

### <a name="custom-actions"></a><span data-ttu-id="a1427-120">自定义操作</span><span class="sxs-lookup"><span data-stu-id="a1427-120">Custom actions</span></span>
<span data-ttu-id="a1427-121">实现自定义操作的步骤与元素的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="a1427-121">The steps to implementing a custom action are the same as those for elements.</span></span> <span data-ttu-id="a1427-122">唯一的区别在于操作注册在操作注册表中，而不是在元素注册表中注册。</span><span class="sxs-lookup"><span data-stu-id="a1427-122">The only difference is that actions are registered in action registries, and not in element registries.</span></span>

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

<span data-ttu-id="a1427-123">全局注册新操作：</span><span class="sxs-lookup"><span data-stu-id="a1427-123">Register the new action globally:</span></span>
```typescript
AC.GlobalRegistry.actions.register(AlertAction.JsonTypeName, AlertAction);
```

<span data-ttu-id="a1427-124">或使用每个卡的注册表：</span><span class="sxs-lookup"><span data-stu-id="a1427-124">Or use a per-card registry:</span></span>
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

## <a name="extensibility-with-the-js-sdk-prior-to-version-20"></a><span data-ttu-id="a1427-125">2.0 版之前的 JS SDK 可扩展性</span><span class="sxs-lookup"><span data-stu-id="a1427-125">Extensibility with the JS SDK prior to version 2.0</span></span>

### <a name="custom-elements"></a><span data-ttu-id="a1427-126">自定义元素</span><span class="sxs-lookup"><span data-stu-id="a1427-126">Custom elements</span></span>

<span data-ttu-id="a1427-127">创建自定义自适应卡元素类型的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="a1427-127">The steps for creating a custom Adaptive Card element type are:</span></span>
- <span data-ttu-id="a1427-128">创建一个派生自的新类`CardElement`</span><span class="sxs-lookup"><span data-stu-id="a1427-128">Create a new class deriving from `CardElement`</span></span>
- <span data-ttu-id="a1427-129">实现其 `getJsonTypeName` 、 `parse` 、 `toJSON` `internalRender` 和 `renderSpeech` 方法</span><span class="sxs-lookup"><span data-stu-id="a1427-129">Implement its `getJsonTypeName`, `parse`, `toJSON`, `internalRender` and `renderSpeech` methods</span></span>
- <span data-ttu-id="a1427-130">通过将其添加到呈现器的元素注册表来注册它</span><span class="sxs-lookup"><span data-stu-id="a1427-130">Register it by adding it to the renderer's element registry</span></span>

<span data-ttu-id="a1427-131">我们来看一个示例并实现一个简单的进度栏元素：</span><span class="sxs-lookup"><span data-stu-id="a1427-131">Let's take an example and implement a simple Progress Bar element:</span></span>

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

<span data-ttu-id="a1427-132">就是这样。</span><span class="sxs-lookup"><span data-stu-id="a1427-132">That's it.</span></span> <span data-ttu-id="a1427-133">现在只需向呈现器注册进度栏类：</span><span class="sxs-lookup"><span data-stu-id="a1427-133">Now just register the Progress Bar class with the renderer:</span></span>

```typescript
Adaptive.AdaptiveCard.elementTypeRegistry.registerType("ProgressBar", () => { return new ProgressBar(); });
```

## <a name="custom-actions"></a><span data-ttu-id="a1427-134">自定义操作</span><span class="sxs-lookup"><span data-stu-id="a1427-134">Custom actions</span></span>

<span data-ttu-id="a1427-135">创建自定义自适应卡操作的步骤实质上与自定义元素的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="a1427-135">The steps for creating a custom Adaptive Card action are essentially the same as those for custom elements.</span></span> <span data-ttu-id="a1427-136">下面是一个简单的警报操作示例，只显示具有可配置文本的消息框：</span><span class="sxs-lookup"><span data-stu-id="a1427-136">Here is a simple example of an Alert Action that simply displays a message box with configurable text:</span></span>

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

<span data-ttu-id="a1427-137">现在，注册新操作：</span><span class="sxs-lookup"><span data-stu-id="a1427-137">Now register the new action:</span></span>

```typescript
Adaptive.AdaptiveCard.actionTypeRegistry.registerType("Action.Alert", () => { return new AlertAction(); });
```

## <a name="example"></a><span data-ttu-id="a1427-138">示例</span><span class="sxs-lookup"><span data-stu-id="a1427-138">Example</span></span>

<span data-ttu-id="a1427-139">下面是一个示例卡，它使用 ProgressBar 元素和 AlertAction 操作：</span><span class="sxs-lookup"><span data-stu-id="a1427-139">Here is a sample card that uses both the ProgressBar element and AlertAction action:</span></span>
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

<span data-ttu-id="a1427-140">下面是它的呈现方式： ![ 图像](https://user-images.githubusercontent.com/1334689/52665466-8155e780-2ec0-11e9-841a-7d272ad1d103.png)</span><span class="sxs-lookup"><span data-stu-id="a1427-140">And here is how it renders: ![image](https://user-images.githubusercontent.com/1334689/52665466-8155e780-2ec0-11e9-841a-7d272ad1d103.png)</span></span>
