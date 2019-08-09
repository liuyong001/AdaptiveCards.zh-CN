---
title: 模板化 Sdk
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: 5f60a458af99f1b88e8ee428a8f29f1849be9b62
ms.sourcegitcommit: a16f53ba10a8607deacde5c8cc78927cac58657c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68878874"
---
# <a name="adaptive-card-templating-sdks"></a><span data-ttu-id="051ce-102">自适应卡模板化 Sdk</span><span class="sxs-lookup"><span data-stu-id="051ce-102">Adaptive Card Templating SDKs</span></span>

<span data-ttu-id="051ce-103">自适应卡模板化 Sdk 使你能够轻松地在任何受支持的平台上使用实际数据填充[卡模板](language.md)。</span><span class="sxs-lookup"><span data-stu-id="051ce-103">The Adaptive Card Templating SDKs make it easy to populate a [card template](language.md) with real data on any supported platform.</span></span>

> <span data-ttu-id="051ce-104">有关[自适应卡模板的概述](index.md), 请阅读此概述</span><span class="sxs-lookup"><span data-stu-id="051ce-104">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="051ce-105">这些功能**处于预览阶段, 可能会有所更改**。</span><span class="sxs-lookup"><span data-stu-id="051ce-105">These features are **in preview and subject to change**.</span></span> <span data-ttu-id="051ce-106">你的反馈不仅是欢迎的, 而且确保我们能够提供**所**需的功能至关重要。</span><span class="sxs-lookup"><span data-stu-id="051ce-106">Your feedback is not only welcome, but  critical to ensure we deliver the features **you** need.</span></span>
> 
> <span data-ttu-id="051ce-107">在初始预览过程中, 仅可使用 JavaScript SDK, 但 .NET SDK 应该很快就会到达。</span><span class="sxs-lookup"><span data-stu-id="051ce-107">During the initial preview only the JavaScript SDK is available, but a .NET SDK should arrive shortly.</span></span>

## <a name="javascript"></a><span data-ttu-id="051ce-108">JavaScript</span><span class="sxs-lookup"><span data-stu-id="051ce-108">JavaScript</span></span>

<span data-ttu-id="051ce-109">[Adaptivecards 模板](https://www.npmjs.com/package/adaptivecards-templating)库在 npm 上和通过 CDN 提供。</span><span class="sxs-lookup"><span data-stu-id="051ce-109">The [adaptivecards-templating](https://www.npmjs.com/package/adaptivecards-templating) library is available on npm and via CDN.</span></span> <span data-ttu-id="051ce-110">有关完整文档, 请参阅包链接。</span><span class="sxs-lookup"><span data-stu-id="051ce-110">See the package link for full documentation.</span></span>

### <a name="npm"></a><span data-ttu-id="051ce-111">npm</span><span class="sxs-lookup"><span data-stu-id="051ce-111">npm</span></span>

```console
npm install adaptivecards-templating
```

### <a name="cdn"></a><span data-ttu-id="051ce-112">CDN</span><span class="sxs-lookup"><span data-stu-id="051ce-112">CDN</span></span>

```html
<script src="https://unpkg.com/adaptivecards-templating/dist/adaptivecards-templating.min.js"></script>
``` 

### <a name="usage"></a><span data-ttu-id="051ce-113">用法</span><span class="sxs-lookup"><span data-stu-id="051ce-113">Usage</span></span>

<span data-ttu-id="051ce-114">下面的示例假定还安装了[adaptivecards](https://www.npmjs.com/package/adaptivecards)库, 以便呈现卡。</span><span class="sxs-lookup"><span data-stu-id="051ce-114">The sample below assumes you've also installed the [adaptivecards](https://www.npmjs.com/package/adaptivecards) library in order to render the card.</span></span> 

<span data-ttu-id="051ce-115">如果不打算呈现卡`parse` , 则可以删除和`render`代码。</span><span class="sxs-lookup"><span data-stu-id="051ce-115">If you don't plan on rendering the card then you can remove the `parse` and `render` code.</span></span> 

```js
import * as ACData from "adaptivecards-templating";
import * as AdaptiveCards from "adaptivecards";
 
// Define a template payload
var templatePayload = {
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "Hello {name}!"
        }
    ]
};
 
// Create a Template instamce from the template payload
var template = new ACData.Template(templatePayload);
 
// Create a data binding context, and set its $root property to the
// data object to bind the template to
var context = new ACData.EvaluationContext();
context.$root = {
    "name": "Mickey Mouse"
};
 
// "Expand" the template - this generates the final Adaptive Card,
// ready to render
var card = template.expand(context);
 
// Render the card
var adaptiveCard = new AdaptiveCards.AdaptiveCard();
adaptiveCard.parse(card);
 
var htmlElement = adaptiveCard.render();
```

## <a name="net-coming-soon"></a><span data-ttu-id="051ce-116">.NET (即将*推出*)</span><span class="sxs-lookup"><span data-stu-id="051ce-116">.NET (*coming soon*)</span></span>

<span data-ttu-id="051ce-117">尚未工作:</span><span class="sxs-lookup"><span data-stu-id="051ce-117">NOT WORKING YET:</span></span> 

```console
nuget install AdaptiveCards.Templating
```
