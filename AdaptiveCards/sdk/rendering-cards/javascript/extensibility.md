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
# <a name="extensibility---javascript"></a><span data-ttu-id="d34d4-102">扩展性-JavaScript</span><span class="sxs-lookup"><span data-stu-id="d34d4-102">Extensibility - JavaScript</span></span>

## <a name="extensibility-with-the-js-sdk-version-20-and-greater"></a><span data-ttu-id="d34d4-103">适用于 JS SDK 版本2.0 及更高版本的扩展性</span><span class="sxs-lookup"><span data-stu-id="d34d4-103">Extensibility with the JS SDK version 2.0 and greater</span></span>

### <a name="before-you-start"></a><span data-ttu-id="d34d4-104">开始之前</span><span class="sxs-lookup"><span data-stu-id="d34d4-104">Before you start</span></span>

> <span data-ttu-id="d34d4-105">**重要提示**： JS SDK 2.0 和更高版本利用了 [TypeScript 修饰器](https://www.typescriptlang.org/docs/handbook/decorators.html)。</span><span class="sxs-lookup"><span data-stu-id="d34d4-105">**IMPORTANT**: Version 2.0 and greater of the JS SDK makes use of [TypeScript decorators](https://www.typescriptlang.org/docs/handbook/decorators.html).</span></span> <span data-ttu-id="d34d4-106">修饰器仍为实验功能，并且必须在文件中显式启用 `tsconfig.js` ：</span><span class="sxs-lookup"><span data-stu-id="d34d4-106">Decorators are still an experimental feature and must be explicitly enabled in your `tsconfig.js` file:</span></span>

```json
{
   "compilerOptions": {
       "experimentalDecorators": true
   }
}
```
<span data-ttu-id="d34d4-107">2.0 版的 JS SDK 引入了自定义元素和操作的实现和注册方式的重大更改。</span><span class="sxs-lookup"><span data-stu-id="d34d4-107">Version 2.0 of the JS SDK introduces breaking changes in the way custom elements and actions are implemented and registered.</span></span> <span data-ttu-id="d34d4-108">有关如何使用以前版本的 SDK 实现和注册元素或操作的示例，请参阅 [2.0 版之前的 JS SDK 扩展性](#extensibility-with-the-js-sdk-prior-to-version-20)。</span><span class="sxs-lookup"><span data-stu-id="d34d4-108">For an example on how to implement and register an element or action using previous versions of the SDK, see [Extensibility with the JS SDK prior to version 2.0](#extensibility-with-the-js-sdk-prior-to-version-20).</span></span>


### <a name="custom-elements"></a><span data-ttu-id="d34d4-109">自定义元素</span><span class="sxs-lookup"><span data-stu-id="d34d4-109">Custom elements</span></span>
<span data-ttu-id="d34d4-110">创建自定义自适应卡元素类型的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="d34d4-110">The steps for creating a custom Adaptive Card element type are:</span></span>
- <span data-ttu-id="d34d4-111">创建一个派生自的新类 `CardElement`</span><span class="sxs-lookup"><span data-stu-id="d34d4-111">Create a new class deriving from `CardElement`</span></span>
- <span data-ttu-id="d34d4-112">通过声明静态属性定义创建其架构</span><span class="sxs-lookup"><span data-stu-id="d34d4-112">Create its schema by declaring static property definitions</span></span>
- <span data-ttu-id="d34d4-113">实现其 `getJsonTypeName` 和 `internalRender` 方法</span><span class="sxs-lookup"><span data-stu-id="d34d4-113">Implement its `getJsonTypeName`, and `internalRender` methods</span></span>
- <span data-ttu-id="d34d4-114">在全局元素注册表中注册它，或在每个卡上使用自定义注册表</span><span class="sxs-lookup"><span data-stu-id="d34d4-114">Register it in the global element registry, or use a custom registry on a per-card basis</span></span>


<span data-ttu-id="d34d4-115">我们来看一个示例并实现一个简单的进度栏元素：</span><span class="sxs-lookup"><span data-stu-id="d34d4-115">Let's take an example and implement a simple Progress Bar element:</span></span>
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
<span data-ttu-id="d34d4-116">就是这样。</span><span class="sxs-lookup"><span data-stu-id="d34d4-116">That's it.</span></span> <span data-ttu-id="d34d4-117">现在需要注册 ProgressBar 元素，才能被 SDK 识别。</span><span class="sxs-lookup"><span data-stu-id="d34d4-117">The ProgressBar element now needs to be registered in order to be recognized by the SDK.</span></span> <span data-ttu-id="d34d4-118">可以全局注册：</span><span class="sxs-lookup"><span data-stu-id="d34d4-118">You can register it globally:</span></span>

```typescript
AC.GlobalRegistry.elements.register(ProgressBar.JsonTypeName, ProgressBar);
```

<span data-ttu-id="d34d4-119">或者，你可以使用每个卡的注册表，这允许在你的应用程序中使用不同的注册表项：</span><span class="sxs-lookup"><span data-stu-id="d34d4-119">Or you can use a per-card registry, which allows the use of different registries for different cards in your application:</span></span>

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

### <a name="custom-inputs"></a><span data-ttu-id="d34d4-120">自定义输入</span><span class="sxs-lookup"><span data-stu-id="d34d4-120">Custom inputs</span></span>
<span data-ttu-id="d34d4-121">输入是专用于收集最终用户输入的数据的一种特殊类型的元素，随后可以将该数据作为参数传递给操作。</span><span class="sxs-lookup"><span data-stu-id="d34d4-121">An input is a special type of element dedicated to collecting data entered by the end user that can subsequently be passed as parameter to actions.</span></span>

<span data-ttu-id="d34d4-122">当涉及到输入时，自适应卡 1.x SDK 的版本2.x 中引入了两个值得注意的更改：</span><span class="sxs-lookup"><span data-stu-id="d34d4-122">Versions 2.x of the Adaptive Cards JS SDK introduces two notable changes when it comes to inputs:</span></span>
- <span data-ttu-id="d34d4-123">**输入验证：** 现提供内置输入验证机制，可自动处理验证错误，包括视觉提示</span><span class="sxs-lookup"><span data-stu-id="d34d4-123">**Input validation:** there is now a built-in input validation mechanism that automatically handles validation errors including visual cues</span></span>
- <span data-ttu-id="d34d4-124">**辅助功能改进：** 内置输入可以更好地支持辅助功能</span><span class="sxs-lookup"><span data-stu-id="d34d4-124">**Accessibility improvements:** built-in inputs have better support for accessibility features</span></span>

<span data-ttu-id="d34d4-125">因此，实现自定义输入需要比实现简单元素稍微多一些逻辑。</span><span class="sxs-lookup"><span data-stu-id="d34d4-125">Because of this, implementing custom inputs requires a little more logic than implementing simple elements.</span></span> <span data-ttu-id="d34d4-126">下表列出了自定义输入实现为了 partiocipate 输入验证机制并可访问而应实现的所有方法：</span><span class="sxs-lookup"><span data-stu-id="d34d4-126">The table below lists all the methods a custom input implementation should to implement in order to partiocipate in the input validation mechanism and be accessible:</span></span>

| <span data-ttu-id="d34d4-127">方法</span><span class="sxs-lookup"><span data-stu-id="d34d4-127">Method</span></span> | <span data-ttu-id="d34d4-128">说明</span><span class="sxs-lookup"><span data-stu-id="d34d4-128">Description</span></span> |
| --------- | ------------- |
| `protected updateInputControlAriaLabelledBy()` | <span data-ttu-id="d34d4-129">此方法在输入验证序列过程中调用。</span><span class="sxs-lookup"><span data-stu-id="d34d4-129">This method  is called during the input validation sequence.</span></span> <span data-ttu-id="d34d4-130">如果输入未通过验证，则会显示其关联的错误消息，并且需要更新基础输入控件的属性，以使 `aria-labelledby` 输入符合辅助功能要求。</span><span class="sxs-lookup"><span data-stu-id="d34d4-130">When an input fails validation, its associated error message is displayed and the underlying input control's `aria-labelledby` attribute needs to be updated in order for the input to comply with accessibility requirements.</span></span> <span data-ttu-id="d34d4-131">自定义输入应重写 `updateInputControlAriaLabelledBy` ，以将相应的属性应用于 `aria-labelledby` 基础输入控件。</span><span class="sxs-lookup"><span data-stu-id="d34d4-131">Custom inputs SHOULD override `updateInputControlAriaLabelledBy` to apply the appropriate `aria-labelledby` attribute to the underlying input control.</span></span> <span data-ttu-id="d34d4-132">`getAllLabelIds(): string[]`方法可用于检索应在属性中指定的所有标签的 id `aria-labelledby` 。</span><span class="sxs-lookup"><span data-stu-id="d34d4-132">The `getAllLabelIds(): string[]` method can be used to retrieve the Ids of all the labels that should be specified in the `aria-labelledby` attribute.</span></span>  |
| `protected internalRender(): HTMLElement` | <span data-ttu-id="d34d4-133">与任何其他自适应卡自定义元素一样， `internalRender` 必须重写以根据需要呈现输入。</span><span class="sxs-lookup"><span data-stu-id="d34d4-133">Just like for any other Adaptive Card custom element, `internalRender` MUST be overridden to render your input as desired.</span></span> <span data-ttu-id="d34d4-134">这是要在其中创建实际基础输入控件的位置。</span><span class="sxs-lookup"><span data-stu-id="d34d4-134">This is where you'll want to create the actual underlying input control.</span></span> |
| `protected get isNullable(): boolean` | <span data-ttu-id="d34d4-135">指示输入是否支持 (实例的未定义值，例如 Input。 Text 确实如此，而 Input 却不支持。 ) 自定义输入应重写此属性 getter 以指示它们是否支持未定义的值。</span><span class="sxs-lookup"><span data-stu-id="d34d4-135">Indicates whether the input supports undefined values (for instance, Input.Text does, whereas Input.Toggle doesn't.) Custom inputs SHOULD override this property getter to indicate if they support undefined values.</span></span> <span data-ttu-id="d34d4-136">基实现返回 `true` 。</span><span class="sxs-lookup"><span data-stu-id="d34d4-136">The base implementation returns `true`.</span></span> |
| `public focus()` | <span data-ttu-id="d34d4-137">当遇到验证错误时，焦点将自动放置在验证失败的第一个输入上。</span><span class="sxs-lookup"><span data-stu-id="d34d4-137">When validation errors are encountered, the focus is automatically placed on the first input that failed validation.</span></span> <span data-ttu-id="d34d4-138">`focus`在某些情况下，的基实现将适用于自定义输入。</span><span class="sxs-lookup"><span data-stu-id="d34d4-138">The base implementation of `focus` will in some cases just work for custom inputs.</span></span> <span data-ttu-id="d34d4-139">如果不是这种情况，自定义输入控件必须重写， `focus` 以显式将焦点放在基础输入控件上。</span><span class="sxs-lookup"><span data-stu-id="d34d4-139">When that isn't the case, custom input controls MUST override `focus` to explicitly put the focus on the underlying input control.</span></span>  |
| `public abstract isSet(): boolean` | <span data-ttu-id="d34d4-140">指示输入的值是否已由用户设置。</span><span class="sxs-lookup"><span data-stu-id="d34d4-140">Indicates whether the input's value has been set by the user.</span></span> <span data-ttu-id="d34d4-141">在输入验证序列过程中调用此方法，以确定输入是通过还是未通过验证。</span><span class="sxs-lookup"><span data-stu-id="d34d4-141">This method is called during the input validation sequence to determine if the input passes or fails validation.</span></span> <span data-ttu-id="d34d4-142">为了加入输入验证机制，自定义输入必须重写 `isSet` 。</span><span class="sxs-lookup"><span data-stu-id="d34d4-142">Custom inputs MUST override `isSet` in order to participate in the input validation mechanism.</span></span> |
| `public isValid(): boolean` | <span data-ttu-id="d34d4-143">指示输入的值是否有效。</span><span class="sxs-lookup"><span data-stu-id="d34d4-143">Indicates whether the value of the input is valid.</span></span> <span data-ttu-id="d34d4-144">在输入验证序列过程中调用此方法，以确定输入是通过还是未通过验证。</span><span class="sxs-lookup"><span data-stu-id="d34d4-144">This method is called during the input validation sequence to determine if the input passes or fails validation.</span></span> <span data-ttu-id="d34d4-145">为了加入输入验证机制，应重写自定义输入 `isValid` 。</span><span class="sxs-lookup"><span data-stu-id="d34d4-145">Custom inputs SHOULD override `isValid` in order to participate in the input validation mechanism.</span></span> <span data-ttu-id="d34d4-146">基实现返回 `true` 。</span><span class="sxs-lookup"><span data-stu-id="d34d4-146">The base implementation returns `true`.</span></span> |
| `public abstract get value(): any` | <span data-ttu-id="d34d4-147">返回输入值。</span><span class="sxs-lookup"><span data-stu-id="d34d4-147">Returns the value of the input.</span></span> <span data-ttu-id="d34d4-148">自定义输入必须重写此，以便从基础输入控件检索输入值。</span><span class="sxs-lookup"><span data-stu-id="d34d4-148">Custom inputs MUST override this so that the value of the input is retrieved from the underlying input control.</span></span> |


### <a name="custom-actions"></a><span data-ttu-id="d34d4-149">自定义操作</span><span class="sxs-lookup"><span data-stu-id="d34d4-149">Custom actions</span></span>
<span data-ttu-id="d34d4-150">实现自定义操作的步骤与元素的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="d34d4-150">The steps to implementing a custom action are the same as those for elements.</span></span> <span data-ttu-id="d34d4-151">唯一的区别在于操作注册在操作注册表中，而不是在元素注册表中注册。</span><span class="sxs-lookup"><span data-stu-id="d34d4-151">The only difference is that actions are registered in action registries, and not in element registries.</span></span>

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

<span data-ttu-id="d34d4-152">全局注册新操作：</span><span class="sxs-lookup"><span data-stu-id="d34d4-152">Register the new action globally:</span></span>
```typescript
AC.GlobalRegistry.actions.register(AlertAction.JsonTypeName, AlertAction);
```

<span data-ttu-id="d34d4-153">或使用每个卡的注册表：</span><span class="sxs-lookup"><span data-stu-id="d34d4-153">Or use a per-card registry:</span></span>
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

## <a name="extensibility-with-the-js-sdk-prior-to-version-20"></a><span data-ttu-id="d34d4-154">2.0 版之前的 JS SDK 可扩展性</span><span class="sxs-lookup"><span data-stu-id="d34d4-154">Extensibility with the JS SDK prior to version 2.0</span></span>

### <a name="custom-elements"></a><span data-ttu-id="d34d4-155">自定义元素</span><span class="sxs-lookup"><span data-stu-id="d34d4-155">Custom elements</span></span>

### <a name="before-you-start"></a><span data-ttu-id="d34d4-156">开始之前</span><span class="sxs-lookup"><span data-stu-id="d34d4-156">Before you start</span></span>

> <span data-ttu-id="d34d4-157">**重要提示**： JS SDK 2.0 和更高版本利用了 [TypeScript 修饰器](https://www.typescriptlang.org/docs/handbook/decorators.html)。</span><span class="sxs-lookup"><span data-stu-id="d34d4-157">**IMPORTANT**: Version 2.0 and greater of the JS SDK makes use of [TypeScript decorators](https://www.typescriptlang.org/docs/handbook/decorators.html).</span></span> <span data-ttu-id="d34d4-158">修饰器仍为实验功能，并且必须在文件中显式启用 `tsconfig.js` ：</span><span class="sxs-lookup"><span data-stu-id="d34d4-158">Decorators are still an experimental feature and must be explicitly enabled in your `tsconfig.js` file:</span></span>

```json
{
   "compilerOptions": {
       "experimentalDecorators": true
   }
}
```
<span data-ttu-id="d34d4-159">2.0 版的 JS SDK 引入了自定义元素和操作的实现和注册方式的重大更改。</span><span class="sxs-lookup"><span data-stu-id="d34d4-159">Version 2.0 of the JS SDK introduces breaking changes in the way custom elements and actions are implemented and registered.</span></span> <span data-ttu-id="d34d4-160">有关如何使用以前版本的 SDK 实现和注册元素或操作的示例，请参阅 [2.0 版之前的 JS SDK 扩展性](#extensibility-with-the-js-sdk-prior-to-version-20)。</span><span class="sxs-lookup"><span data-stu-id="d34d4-160">For an example on how to implement and register an element or action using previous versions of the SDK, see [Extensibility with the JS SDK prior to version 2.0](#extensibility-with-the-js-sdk-prior-to-version-20).</span></span>


### <a name="custom-elements"></a><span data-ttu-id="d34d4-161">自定义元素</span><span class="sxs-lookup"><span data-stu-id="d34d4-161">Custom elements</span></span>
<span data-ttu-id="d34d4-162">创建自定义自适应卡元素类型的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="d34d4-162">The steps for creating a custom Adaptive Card element type are:</span></span>
- <span data-ttu-id="d34d4-163">创建一个派生自的新类 `CardElement`</span><span class="sxs-lookup"><span data-stu-id="d34d4-163">Create a new class deriving from `CardElement`</span></span>
- <span data-ttu-id="d34d4-164">通过声明静态属性定义创建其架构</span><span class="sxs-lookup"><span data-stu-id="d34d4-164">Create its schema by declaring static property definitions</span></span>
- <span data-ttu-id="d34d4-165">实现其 `getJsonTypeName` 和 `internalRender` 方法</span><span class="sxs-lookup"><span data-stu-id="d34d4-165">Implement its `getJsonTypeName`, and `internalRender` methods</span></span>
- <span data-ttu-id="d34d4-166">在全局元素注册表中注册它，或在每个卡上使用自定义注册表</span><span class="sxs-lookup"><span data-stu-id="d34d4-166">Register it in the global element registry, or use a custom registry on a per-card basis</span></span>


<span data-ttu-id="d34d4-167">我们来看一个示例并实现一个简单的进度栏元素：</span><span class="sxs-lookup"><span data-stu-id="d34d4-167">Let's take an example and implement a simple Progress Bar element:</span></span>
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
<span data-ttu-id="d34d4-168">就是这样。</span><span class="sxs-lookup"><span data-stu-id="d34d4-168">That's it.</span></span> <span data-ttu-id="d34d4-169">现在需要注册 ProgressBar 元素，才能被 SDK 识别。</span><span class="sxs-lookup"><span data-stu-id="d34d4-169">The ProgressBar element now needs to be registered in order to be recognized by the SDK.</span></span> <span data-ttu-id="d34d4-170">可以全局注册：</span><span class="sxs-lookup"><span data-stu-id="d34d4-170">You can register it globally:</span></span>

```typescript
AC.GlobalRegistry.elements.register(ProgressBar.JsonTypeName, ProgressBar);
```

<span data-ttu-id="d34d4-171">或者，你可以使用每个卡的注册表，这允许在你的应用程序中使用不同的注册表项：</span><span class="sxs-lookup"><span data-stu-id="d34d4-171">Or you can use a per-card registry, which allows the use of different registries for different cards in your application:</span></span>

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

### <a name="custom-actions"></a><span data-ttu-id="d34d4-172">自定义操作</span><span class="sxs-lookup"><span data-stu-id="d34d4-172">Custom actions</span></span>
<span data-ttu-id="d34d4-173">实现自定义操作的步骤与元素的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="d34d4-173">The steps to implementing a custom action are the same as those for elements.</span></span> <span data-ttu-id="d34d4-174">唯一的区别在于操作注册在操作注册表中，而不是在元素注册表中注册。</span><span class="sxs-lookup"><span data-stu-id="d34d4-174">The only difference is that actions are registered in action registries, and not in element registries.</span></span>

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

<span data-ttu-id="d34d4-175">全局注册新操作：</span><span class="sxs-lookup"><span data-stu-id="d34d4-175">Register the new action globally:</span></span>
```typescript
AC.GlobalRegistry.actions.register(AlertAction.JsonTypeName, AlertAction);
```

<span data-ttu-id="d34d4-176">或使用每个卡的注册表：</span><span class="sxs-lookup"><span data-stu-id="d34d4-176">Or use a per-card registry:</span></span>
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

## <a name="extensibility-with-the-js-sdk-prior-to-version-20"></a><span data-ttu-id="d34d4-177">2.0 版之前的 JS SDK 可扩展性</span><span class="sxs-lookup"><span data-stu-id="d34d4-177">Extensibility with the JS SDK prior to version 2.0</span></span>

### <a name="custom-elements"></a><span data-ttu-id="d34d4-178">自定义元素</span><span class="sxs-lookup"><span data-stu-id="d34d4-178">Custom elements</span></span>

<span data-ttu-id="d34d4-179">创建自定义自适应卡元素类型的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="d34d4-179">The steps for creating a custom Adaptive Card element type are:</span></span>
- <span data-ttu-id="d34d4-180">创建一个派生自的新类 `CardElement`</span><span class="sxs-lookup"><span data-stu-id="d34d4-180">Create a new class deriving from `CardElement`</span></span>
- <span data-ttu-id="d34d4-181">实现其 `getJsonTypeName` 、 `parse` 、 `toJSON` `internalRender` 和 `renderSpeech` 方法</span><span class="sxs-lookup"><span data-stu-id="d34d4-181">Implement its `getJsonTypeName`, `parse`, `toJSON`, `internalRender` and `renderSpeech` methods</span></span>
- <span data-ttu-id="d34d4-182">通过将其添加到呈现器的元素注册表来注册它</span><span class="sxs-lookup"><span data-stu-id="d34d4-182">Register it by adding it to the renderer's element registry</span></span>

<span data-ttu-id="d34d4-183">我们来看一个示例并实现一个简单的进度栏元素：</span><span class="sxs-lookup"><span data-stu-id="d34d4-183">Let's take an example and implement a simple Progress Bar element:</span></span>

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

<span data-ttu-id="d34d4-184">就是这样。</span><span class="sxs-lookup"><span data-stu-id="d34d4-184">That's it.</span></span> <span data-ttu-id="d34d4-185">现在只需向呈现器注册进度栏类：</span><span class="sxs-lookup"><span data-stu-id="d34d4-185">Now just register the Progress Bar class with the renderer:</span></span>

```typescript
Adaptive.AdaptiveCard.elementTypeRegistry.registerType("ProgressBar", () => { return new ProgressBar(); });
```

## <a name="custom-actions"></a><span data-ttu-id="d34d4-186">自定义操作</span><span class="sxs-lookup"><span data-stu-id="d34d4-186">Custom actions</span></span>

<span data-ttu-id="d34d4-187">创建自定义自适应卡操作的步骤实质上与自定义元素的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="d34d4-187">The steps for creating a custom Adaptive Card action are essentially the same as those for custom elements.</span></span> <span data-ttu-id="d34d4-188">下面是一个简单的警报操作示例，只显示具有可配置文本的消息框：</span><span class="sxs-lookup"><span data-stu-id="d34d4-188">Here is a simple example of an Alert Action that simply displays a message box with configurable text:</span></span>

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

<span data-ttu-id="d34d4-189">现在，注册新操作：</span><span class="sxs-lookup"><span data-stu-id="d34d4-189">Now register the new action:</span></span>

```typescript
Adaptive.AdaptiveCard.actionTypeRegistry.registerType("Action.Alert", () => { return new AlertAction(); });
```

## <a name="example"></a><span data-ttu-id="d34d4-190">示例</span><span class="sxs-lookup"><span data-stu-id="d34d4-190">Example</span></span>

<span data-ttu-id="d34d4-191">下面是一个示例卡，它使用 ProgressBar 元素和 AlertAction 操作：</span><span class="sxs-lookup"><span data-stu-id="d34d4-191">Here is a sample card that uses both the ProgressBar element and AlertAction action:</span></span>
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

<span data-ttu-id="d34d4-192">下面是它的呈现方式： ![ 图像](https://user-images.githubusercontent.com/1334689/52665466-8155e780-2ec0-11e9-841a-7d272ad1d103.png)</span><span class="sxs-lookup"><span data-stu-id="d34d4-192">And here is how it renders: ![image](https://user-images.githubusercontent.com/1334689/52665466-8155e780-2ec0-11e9-841a-7d272ad1d103.png)</span></span>
