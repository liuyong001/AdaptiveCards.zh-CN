---
title: 呈现卡-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 08/30/2020
ms.topic: article
ms.openlocfilehash: 4e3bf8d1774933d0c163c34bbe0838fbc9bb842b
ms.sourcegitcommit: 65b792d73c264c943036343e05b75f2b0488e6e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "95001834"
---
# <a name="render-a-card---javascript"></a><span data-ttu-id="81769-102">呈现卡-JavaScript</span><span class="sxs-lookup"><span data-stu-id="81769-102">Render a card - JavaScript</span></span>

<span data-ttu-id="81769-103">下面介绍如何使用 JavaScript SDK 呈现卡片。</span><span class="sxs-lookup"><span data-stu-id="81769-103">Here's how to render a card using the JavaScript SDK.</span></span>

## <a name="usage"></a><span data-ttu-id="81769-104">使用情况</span><span class="sxs-lookup"><span data-stu-id="81769-104">Usage</span></span>

### <a name="import-the-module"></a><span data-ttu-id="81769-105">导入模块</span><span class="sxs-lookup"><span data-stu-id="81769-105">Import the module</span></span>

```js
// import the module
import * as AdaptiveCards from "adaptivecards";

// or require it
var AdaptiveCards = require("adaptivecards");

// or use the global variable if loaded from CDN
AdaptiveCards.renderCard(...);
```

## <a name="render-a-card"></a><span data-ttu-id="81769-106">呈现卡片</span><span class="sxs-lookup"><span data-stu-id="81769-106">Render a card</span></span>

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
//     AdaptiveCards.AdaptiveCard.onProcessMarkdown = function (text, result) {
//         result.outputHtml = markdownit().render(text);
//         result.didProcess = true;
//     };

// Parse the card payload
adaptiveCard.parse(card);

// Render the card to an HTML element:
var renderedCard = adaptiveCard.render();

// And finally insert it somewhere in your page:
document.body.appendChild(renderedCard);
```