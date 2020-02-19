---
title: 呈现卡片 - .NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: 0280e37506e1034572f518b1f596e8f1a3bb30be
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454460"
---
# <a name="render-a-card---net-html"></a><span data-ttu-id="0fa76-102">呈现卡片 - .NET HTML</span><span class="sxs-lookup"><span data-stu-id="0fa76-102">Render a card - .NET HTML</span></span>

<span data-ttu-id="0fa76-103">下面介绍如何使用 .NET HTML SDK 来呈现卡片。</span><span class="sxs-lookup"><span data-stu-id="0fa76-103">Here's how to render a card using the .NET HTML SDK.</span></span>

## <a name="instantiate-a-renderer"></a><span data-ttu-id="0fa76-104">实例化呈现器</span><span class="sxs-lookup"><span data-stu-id="0fa76-104">Instantiate a renderer</span></span>

<span data-ttu-id="0fa76-105">下一步是创建呈现器的实例。</span><span class="sxs-lookup"><span data-stu-id="0fa76-105">The next step is to create an instance of the renderer.</span></span> 

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

## <a name="render-a-card-to-html"></a><span data-ttu-id="0fa76-106">将卡片呈现为 HTML</span><span class="sxs-lookup"><span data-stu-id="0fa76-106">Render a card to HTML</span></span>

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
    // Or the card exceeded the maximum number of supported actions, etc
    IList<AdaptiveWarning> warnings = renderedCard.Warnings;
}
catch(AdaptiveException ex)
{
    // Failed rendering
}
```
