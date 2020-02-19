---
title: 扩展性-.NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: d1df38608abde9ad26c78bbc5f66eb3bbb3d1971
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454530"
---
# <a name="extensibility---net-html"></a><span data-ttu-id="8e36d-102">扩展性-.NET HTML</span><span class="sxs-lookup"><span data-stu-id="8e36d-102">Extensibility - .NET HTML</span></span>

## <a name="custom-element-rendering"></a><span data-ttu-id="8e36d-103">自定义元素呈现</span><span class="sxs-lookup"><span data-stu-id="8e36d-103">Custom Element Rendering</span></span>

<span data-ttu-id="8e36d-104">若要完全控制呈现器，可以使用 `ElementRenderers` 属性来**添加**、**删除**或**重写**默认呈现器。</span><span class="sxs-lookup"><span data-stu-id="8e36d-104">For full control of the renderer you can use the `ElementRenderers` property to **add**, **remove**, or **override** default renderers.</span></span>

<span data-ttu-id="8e36d-105">以下示例显示了如何定义并呈现一个自定义 `"type": "Rating"` 元素。</span><span class="sxs-lookup"><span data-stu-id="8e36d-105">The following example shows how you could define a custom `"type": "Rating"` element and render it.</span></span>

```csharp
// Register the new type with the JSON parser
AdaptiveTypedElementConverter.RegisterTypedElement<MyCustomRating>();

// Add the new type to the element renderer registry
renderer.ElementRenderers.Set<MyCustomRating>(MyCustomRating.Render);

// Define a custom Rating element type
public class MyCustomRating : AdaptiveElement
{
    public override string Type => "Rating";

    public double Rating { get; set; }

    public AdaptiveTextSize Size { get; set; }

    public AdaptiveTextColor Color { get; set; }

    public static FrameworkElement Render(MyCustomRating rating, AdaptiveRenderContext context)
    {
        var textBlock = new AdaptiveTextBlock
        {
            Size = rating.Size,
            Color = rating.Color
        };
        for (int i = 0; i < rating.Rating; i++)
        {
            textBlock.Text += "\u2605";
        }
        textBlock.Text += $" ({rating.Rating})";
        return context.Render(textBlock);
    }
}
```
