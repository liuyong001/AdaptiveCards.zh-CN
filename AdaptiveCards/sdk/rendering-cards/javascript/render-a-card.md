---
title: 呈现卡-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 16e4b3e057137e361be52d654fa937c5dae5ff6f
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454580"
---
# <a name="render-a-card---javascript"></a><span data-ttu-id="fc681-102">呈现卡-JavaScript</span><span class="sxs-lookup"><span data-stu-id="fc681-102">Render a card - JavaScript</span></span>

<span data-ttu-id="fc681-103">下面介绍如何使用 JavaScript SDK 呈现卡片。</span><span class="sxs-lookup"><span data-stu-id="fc681-103">Here's how to render a card using the JavaScript SDK.</span></span>

## <a name="usage"></a><span data-ttu-id="fc681-104">用法</span><span class="sxs-lookup"><span data-stu-id="fc681-104">Usage</span></span>

### <a name="import-the-module"></a><span data-ttu-id="fc681-105">导入模块</span><span class="sxs-lookup"><span data-stu-id="fc681-105">Import the module</span></span>

```js
// import the module
import * as AdaptiveCards from "adaptivecards";

// or require it
var AdaptiveCards = require("adaptivecards");

// or use the global variable if loaded from CDN
AdaptiveCards.renderCard(...);
```

## <a name="render-a-card"></a><span data-ttu-id="fc681-106">呈现卡片</span><span class="sxs-lookup"><span data-stu-id="fc681-106">Render a card</span></span>

```js
// Author a card
// In practice you'll probably get this from a service
// see http://adaptivecards.io/samples/ for inspiration
var card = {
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/adaptive-card-50.png"
        },
        {
            "type": "TextBlock",
            "text": "Hello **Adaptive Cards!**"
        }
    ],
    "actions": [
        {
            "type": "Action.OpenUrl",
            "title": "Learn more",
            "url": "http://adaptivecards.io"
        },
        {
            "type": "Action.OpenUrl",
            "title": "GitHub",
            "url": "http://github.com/Microsoft/AdaptiveCards"
        }
    ]
};

// Create an AdaptiveCard instance
var adaptiveCard = new AdaptiveCards.AdaptiveCard();

// Set its hostConfig property unless you want to use the default Host Config
// Host Config defines the style and behavior of a card
adaptiveCard.hostConfig = new AdaptiveCards.HostConfig({
    fontFamily: "Segoe UI, Helvetica Neue, sans-serif"
    // More host config options
});

// Set the adaptive card's event handlers. onExecuteAction is invoked
// whenever an action is clicked in the card
adaptiveCard.onExecuteAction = function(action) { alert("Ow!"); }

// For markdown support you need a third-party library
// E.g., to use markdown-it, include in your HTML page:
//     <script type="text/javascript" src="https://unpkg.com/markdown-it/dist/markdown-it.js"></script>
// And add this code to replace the default markdown handler:
//     AdaptiveCards.processMarkdown = function(text) { return markdownit().render(text); }

// Parse the card payload
adaptiveCard.parse(card);

// Render the card to an HTML element:
var renderedCard = adaptiveCard.render();

// And finally insert it somewhere in your page:
document.body.appendChild(renderedCard);
```