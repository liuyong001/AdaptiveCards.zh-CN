---
title: JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 29786fe5e533e67558df88f58b1330aa6646b532
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454616"
---
# <a name="getting-started---javascript"></a><span data-ttu-id="da471-102">入门-JavaScript</span><span class="sxs-lookup"><span data-stu-id="da471-102">Getting started - JavaScript</span></span>

<span data-ttu-id="da471-103">正如我们在[入门](../../../authoring-cards/getting-started.md)"页中所述，自适应卡是 JSON 序列化的卡对象模型。</span><span class="sxs-lookup"><span data-stu-id="da471-103">As we described in [Getting Started](../../../authoring-cards/getting-started.md) page, an Adaptive Card is a JSON-serialized card object model.</span></span> <span data-ttu-id="da471-104">这是用于在浏览器中生成客户端 HTML 的 JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="da471-104">This is a JavaScript SDK for generating client-side HTML in the browser.</span></span>

## <a name="install"></a><span data-ttu-id="da471-105">安装</span><span class="sxs-lookup"><span data-stu-id="da471-105">Install</span></span>

### <a name="node"></a><span data-ttu-id="da471-106">节点</span><span class="sxs-lookup"><span data-stu-id="da471-106">Node</span></span>

<span data-ttu-id="da471-107">[![npm install](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards)</span><span class="sxs-lookup"><span data-stu-id="da471-107">[![npm install](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards)</span></span>

```console
npm install adaptivecards
```

### <a name="cdn"></a><span data-ttu-id="da471-108">CDN</span><span class="sxs-lookup"><span data-stu-id="da471-108">CDN</span></span>

```html
<script src="https://unpkg.com/adaptivecards/dist/adaptivecards.js"></script>
```

## <a name="usage"></a><span data-ttu-id="da471-109">用法</span><span class="sxs-lookup"><span data-stu-id="da471-109">Usage</span></span>

### <a name="import-the-module"></a><span data-ttu-id="da471-110">导入模块</span><span class="sxs-lookup"><span data-stu-id="da471-110">Import the module</span></span>

```js
// import the module
import * as AdaptiveCards from "adaptivecards";

// or require it
var AdaptiveCards = require("adaptivecards");

// or use the global variable if loaded from CDN
AdaptiveCards.renderCard(...);
```

## <a name="next-steps"></a><span data-ttu-id="da471-111">后续步骤</span><span class="sxs-lookup"><span data-stu-id="da471-111">Next steps</span></span>

<span data-ttu-id="da471-112">请参阅[呈现卡片](render-a-card.md)，了解后续步骤！</span><span class="sxs-lookup"><span data-stu-id="da471-112">See [Render a card](render-a-card.md) for the next steps!</span></span>
