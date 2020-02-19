---
title: 扩展性-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 4c43637d81bcf43251638133c66d1c77b92ace56
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454670"
---
# <a name="extensibility---javascript"></a><span data-ttu-id="82a76-102">扩展性-JavaScript</span><span class="sxs-lookup"><span data-stu-id="82a76-102">Extensibility - JavaScript</span></span>

## <a name="implement-and-register-a-custom-element"></a><span data-ttu-id="82a76-103">实现并注册自定义元素</span><span class="sxs-lookup"><span data-stu-id="82a76-103">Implement and register a custom element</span></span>

<span data-ttu-id="82a76-104">创建自定义自适应卡元素类型的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="82a76-104">The steps for creating a custom Adaptive Card element type are:</span></span>
- <span data-ttu-id="82a76-105">创建一个新类，从 `CardElement`</span><span class="sxs-lookup"><span data-stu-id="82a76-105">Create a new class driving from `CardElement`</span></span>
- <span data-ttu-id="82a76-106">实现其 `getJsonTypeName`、`parse`、`toJSON`、`internalRender` 和 `renderSpeech` 方法</span><span class="sxs-lookup"><span data-stu-id="82a76-106">Implement its `getJsonTypeName`, `parse`, `toJSON`, `internalRender` and `renderSpeech` methods</span></span>
- <span data-ttu-id="82a76-107">通过将其添加到呈现器的元素注册表来注册它</span><span class="sxs-lookup"><span data-stu-id="82a76-107">Register it by adding it to the renderer's element registry</span></span>

<span data-ttu-id="82a76-108">我们来看一个示例并实现一个简单的进度栏元素：</span><span class="sxs-lookup"><span data-stu-id="82a76-108">Let's take an example and implement a simple Progress Bar element:</span></span>

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

<span data-ttu-id="82a76-109">就这么简单。</span><span class="sxs-lookup"><span data-stu-id="82a76-109">That's it.</span></span> <span data-ttu-id="82a76-110">现在只需向呈现器注册进度栏类：</span><span class="sxs-lookup"><span data-stu-id="82a76-110">Now just register the Progress Bar class with the renderer:</span></span>

```typescript
Adaptive.AdaptiveCard.elementTypeRegistry.registerType("ProgressBar", () => { return new ProgressBar(); });
```

## <a name="implement-and-register-a-custom-action"></a><span data-ttu-id="82a76-111">实现并注册自定义操作</span><span class="sxs-lookup"><span data-stu-id="82a76-111">Implement and register a custom action</span></span>

<span data-ttu-id="82a76-112">创建自定义自适应卡操作的步骤实质上与自定义元素的步骤相同。</span><span class="sxs-lookup"><span data-stu-id="82a76-112">The steps for creating a custom Adaptive Card action are essentially the same as those for custom elements.</span></span> <span data-ttu-id="82a76-113">下面是一个简单的警报操作示例，只显示具有可配置文本的消息框：</span><span class="sxs-lookup"><span data-stu-id="82a76-113">Here is a simple example of an Alert Action that simply displays a message box with configurable text:</span></span>

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

<span data-ttu-id="82a76-114">现在，注册新操作：</span><span class="sxs-lookup"><span data-stu-id="82a76-114">Now register the new action:</span></span>

```
Adaptive.AdaptiveCard.actionTypeRegistry.registerType("Action.Alert", () => { return new AlertAction(); });
```

## <a name="example"></a><span data-ttu-id="82a76-115">示例</span><span class="sxs-lookup"><span data-stu-id="82a76-115">Example</span></span>

<span data-ttu-id="82a76-116">下面是一个示例卡，它使用 ProgressBar 元素和 AlertAction 操作：</span><span class="sxs-lookup"><span data-stu-id="82a76-116">Here is a sample card that uses both the ProgressBar element and AlertAction action:</span></span>
```
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

<span data-ttu-id="82a76-117">下面是它的呈现方式： ![映像](https://user-images.githubusercontent.com/1334689/52665466-8155e780-2ec0-11e9-841a-7d272ad1d103.png)</span><span class="sxs-lookup"><span data-stu-id="82a76-117">And here is how it renders: ![image](https://user-images.githubusercontent.com/1334689/52665466-8155e780-2ec0-11e9-841a-7d272ad1d103.png)</span></span>
