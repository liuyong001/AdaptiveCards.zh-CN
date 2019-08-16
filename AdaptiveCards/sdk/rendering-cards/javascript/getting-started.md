---
title: JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 4a6030dda12ab8d9a1e5c387cec63d45e84660d8
ms.sourcegitcommit: aa044167fd0b32b485ea2ce014afcf0b332bf1a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69529841"
---
# <a name="getting-started---javascript"></a><span data-ttu-id="3213f-102">入门-JavaScript</span><span class="sxs-lookup"><span data-stu-id="3213f-102">Getting started - JavaScript</span></span>

<span data-ttu-id="3213f-103">正如我们在[入门](../../../authoring-cards/getting-started.md)"页中所述, 自适应卡是 JSON 序列化的卡对象模型。</span><span class="sxs-lookup"><span data-stu-id="3213f-103">As we described in [Getting Started](../../../authoring-cards/getting-started.md) page, an Adaptive Card is a JSON-serialized card object model.</span></span> <span data-ttu-id="3213f-104">这是用于在浏览器中生成客户端 HTML 的 JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="3213f-104">This is a JavaScript SDK for generating client-side HTML in the browser.</span></span>

## <a name="install"></a><span data-ttu-id="3213f-105">安装</span><span class="sxs-lookup"><span data-stu-id="3213f-105">Install</span></span>

### <a name="node"></a><span data-ttu-id="3213f-106">节点</span><span class="sxs-lookup"><span data-stu-id="3213f-106">Node</span></span>

<span data-ttu-id="3213f-107">[![npm 安装](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards)</span><span class="sxs-lookup"><span data-stu-id="3213f-107">[![npm install](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards)</span></span>

```console
npm install adaptivecards
```

### <a name="cdn"></a><span data-ttu-id="3213f-108">CDN</span><span class="sxs-lookup"><span data-stu-id="3213f-108">CDN</span></span>

```html
<script src="https://unpkg.com/adaptivecards/dist/adaptivecards.js"></script>
```

## <a name="usage"></a><span data-ttu-id="3213f-109">用法</span><span class="sxs-lookup"><span data-stu-id="3213f-109">Usage</span></span>

### <a name="import-the-module"></a><span data-ttu-id="3213f-110">导入模块</span><span class="sxs-lookup"><span data-stu-id="3213f-110">Import the module</span></span>

```js
// import the module
import * as AdaptiveCards from "adaptivecards";

// or require it
var AdaptiveCards = require("adaptivecards");

// or use the global variable if loaded from CDN
AdaptiveCards.renderCard(...);
```

## <a name="next-steps"></a><span data-ttu-id="3213f-111">后续步骤</span><span class="sxs-lookup"><span data-stu-id="3213f-111">Next steps</span></span>

<span data-ttu-id="3213f-112">请参阅[呈现卡片](render-a-card.md)，了解后续步骤！</span><span class="sxs-lookup"><span data-stu-id="3213f-112">See [Render a card](render-a-card.md) for the next steps!</span></span>
