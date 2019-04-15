---
title: 呈现卡-.NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: 8dc1baffb91f0755f1955ee02b8a3e820b0d34e4
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553099"
---
# <a name="render-a-card---net-html"></a><span data-ttu-id="4511c-102">呈现卡-.NET HTML</span><span class="sxs-lookup"><span data-stu-id="4511c-102">Render a card - .NET HTML</span></span>

<span data-ttu-id="4511c-103">下面介绍了如何呈现使用.NET HTML SDK 的卡。</span><span class="sxs-lookup"><span data-stu-id="4511c-103">Here's how to render a card using the .NET HTML SDK.</span></span>

## <a name="instantiate-a-renderer"></a><span data-ttu-id="4511c-104">实例化一个呈现器</span><span class="sxs-lookup"><span data-stu-id="4511c-104">Instantiate a renderer</span></span>

<span data-ttu-id="4511c-105">下一步是创建呈现器的实例。</span><span class="sxs-lookup"><span data-stu-id="4511c-105">The next step is to create an instance of the renderer.</span></span> 

```csharp
using AdaptiveCards;
using AdaptiveCards.Rendering;
using AdaptiveCards.Rendering.Html;
// ... 

// Create a card renderer
AdaptiveCardRenderer renderer = new AdaptiveCardRenderer();

// For fun, check the schema version this renderer supports
AdaptiveSchemaVersion schemaVersion = renderer.SupportedSchemaVersion; // 1.0
```

## <a name="render-a-card-to-html"></a><span data-ttu-id="4511c-106">以 html 格式呈现数据卡</span><span class="sxs-lookup"><span data-stu-id="4511c-106">Render a card to HTML</span></span>

```csharp
// Build a simple card
// In the real world this would probably be provided as JSON
AdaptiveCard card = new AdaptiveCard()
{
    Body = { new AdaptiveTextBlock() { Text = "Hello World" } }
};

try
{
    // Render the card
    RenderedAdaptiveCard renderedCard = renderer.RenderCard(card);

    // Get the output HTML 
    HtmlTag html = renderedCard.Html;

    // (Optional) Check for any renderer warnings
    // This includes things like an unknown element type found in the card
    // Or the card exceeded the maxmimum number of supported actions, etc
    IList<AdaptiveWarning> warnings = renderedCard.Warnings;
}
catch(AdaptiveException ex)
{
    // Failed rendering
}
```
