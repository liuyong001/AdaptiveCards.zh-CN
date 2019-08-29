---
title: 扩展性-UWP SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 198726d2fe310778afabccf05341d5c1de5cd968
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553039"
---
# <a name="extensibility---uwp"></a><span data-ttu-id="cfced-102">扩展性-UWP</span><span class="sxs-lookup"><span data-stu-id="cfced-102">Extensibility - UWP</span></span>

## <a name="changing-per-element-rendering"></a><span data-ttu-id="cfced-103">更改每个元素的呈现</span><span class="sxs-lookup"><span data-stu-id="cfced-103">Changing per element rendering</span></span>

<span data-ttu-id="cfced-104">实现呈现器类并在呈现器中设置它</span><span class="sxs-lookup"><span data-stu-id="cfced-104">Implement a renderer class and set it in the renderer</span></span>

```csharp
// My custom renderer is going to replace how textblocks should render!
public class MyCustomRenderer : IAdaptiveElementRenderer
{
    public UIElement Render(IAdaptiveCardElement element, AdaptiveRenderContext context)
    {
        var adaptiveTextBlock = element as AdaptiveTextBlock;
        TextBlock textblock = new TextBlock()
        {
            Text = adaptiveTextBlock.Text + "I want every single textblock to append this text, and it should be aligned to the right!",
            HorizontalAlignment = HorizontalAlignment.Right
        };

        return textblock;
    }
}

renderer.ElementRenderers.Set("TextBlock", new MyCustomRenderer());
```