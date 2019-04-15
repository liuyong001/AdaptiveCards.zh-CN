---
title: JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 9684b96bba5168a1f07549468274ce5d74c01820
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553459"
---
# <a name="getting-started---javascript"></a><span data-ttu-id="976c2-102">获取已开始-JavaScript</span><span class="sxs-lookup"><span data-stu-id="976c2-102">Getting started - JavaScript</span></span>

<span data-ttu-id="976c2-103">如我们所述[Getting Started](../../../authoring-cards/getting-started.md)页上，自适应卡是一个 JSON 序列化卡对象模型。</span><span class="sxs-lookup"><span data-stu-id="976c2-103">As we described in [Getting Started](../../../authoring-cards/getting-started.md) page, an Adaptive Card is a JSON-serialized card object model.</span></span> <span data-ttu-id="976c2-104">这是用于在浏览器中生成客户端的 HTML 的 JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="976c2-104">This is a JavaScript SDK for generating client-side HTML in the browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="976c2-105">**从 v0.5 的重大更改**</span><span class="sxs-lookup"><span data-stu-id="976c2-105">**Breaking changes from v0.5**</span></span>
> 
> 1. <span data-ttu-id="976c2-106">从包重命名`microsoft-adaptivecards`到 `adaptivecards`</span><span class="sxs-lookup"><span data-stu-id="976c2-106">Package renamed from `microsoft-adaptivecards` to `adaptivecards`</span></span>
> 1. <span data-ttu-id="976c2-107">静态`AdaptiveCards.setHostConfig()`已被移动到的实例成员`AdaptiveCard`。</span><span class="sxs-lookup"><span data-stu-id="976c2-107">The static `AdaptiveCards.setHostConfig()` has been moved to an instance member of `AdaptiveCard`.</span></span> <span data-ttu-id="976c2-108">例如， `myCard.hostConfig = {}`</span><span class="sxs-lookup"><span data-stu-id="976c2-108">E.g., `myCard.hostConfig = {}`</span></span> 
> 1. <span data-ttu-id="976c2-109">`HostConfig` 已进入，但各种重命名和移动。</span><span class="sxs-lookup"><span data-stu-id="976c2-109">`HostConfig` has gone though various renames and moves.</span></span> <span data-ttu-id="976c2-110">请参阅[sample.json](https://github.com/Microsoft/AdaptiveCards/blob/master/samples/HostConfig/sample.json)主机配置的当前结构</span><span class="sxs-lookup"><span data-stu-id="976c2-110">See the [sample.json](https://github.com/Microsoft/AdaptiveCards/blob/master/samples/HostConfig/sample.json) Host Config for current structure</span></span>
> 1. <span data-ttu-id="976c2-111">也已经 v0.5 预览版中，这是某些架构更改[此处所述](https://github.com/Microsoft/AdaptiveCards/pull/633)</span><span class="sxs-lookup"><span data-stu-id="976c2-111">There have also been some schema changes from the v0.5 preview, which are [outlined here](https://github.com/Microsoft/AdaptiveCards/pull/633)</span></span>
> 1. <span data-ttu-id="976c2-112">静态`renderCard()`函数已删除，因为它是冗余的类方法。</span><span class="sxs-lookup"><span data-stu-id="976c2-112">The static `renderCard()` function was removed as it was redundant with the class methods.</span></span> <span data-ttu-id="976c2-113">使用`adaptiveCard.render()`如下所述。</span><span class="sxs-lookup"><span data-stu-id="976c2-113">Use `adaptiveCard.render()` as described below.</span></span> 


## <a name="install"></a><span data-ttu-id="976c2-114">安装</span><span class="sxs-lookup"><span data-stu-id="976c2-114">Install</span></span>

### <a name="node"></a><span data-ttu-id="976c2-115">节点</span><span class="sxs-lookup"><span data-stu-id="976c2-115">Node</span></span>

<span data-ttu-id="976c2-116">[![npm 安装](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards)</span><span class="sxs-lookup"><span data-stu-id="976c2-116">[![npm install](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards)</span></span>

```console
npm install adaptivecards --save
```

### <a name="cdn"></a><span data-ttu-id="976c2-117">CDN</span><span class="sxs-lookup"><span data-stu-id="976c2-117">CDN</span></span>

```html
<script src="https://unpkg.com/adaptivecards/dist/adaptivecards.js"></script>
```

## <a name="usage"></a><span data-ttu-id="976c2-118">用法</span><span class="sxs-lookup"><span data-stu-id="976c2-118">Usage</span></span>

### <a name="import-the-module"></a><span data-ttu-id="976c2-119">导入模块</span><span class="sxs-lookup"><span data-stu-id="976c2-119">Import the module</span></span>

```js
// import the module
import * as AdaptiveCards from "adaptivecards";

// or require it
var AdaptiveCards = require("adaptivecards");

// or use the global variable if loaded from CDN
AdaptiveCards.renderCard(...);
```

## <a name="next-steps"></a><span data-ttu-id="976c2-120">后续步骤</span><span class="sxs-lookup"><span data-stu-id="976c2-120">Next steps</span></span>

<span data-ttu-id="976c2-121">请参阅[呈现卡片](render-a-card.md)以了解后续步骤 ！</span><span class="sxs-lookup"><span data-stu-id="976c2-121">See [Render a card](render-a-card.md) for the next steps!</span></span>
