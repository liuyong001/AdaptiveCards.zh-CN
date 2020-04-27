---
title: 将 SDK 模板化
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: 3a9bfcd1bf8f87959a747997e04f5c5ad2a79980
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "72163612"
---
# <a name="adaptive-card-templating-sdks"></a><span data-ttu-id="ab784-102">自适应卡片模板化 SDK</span><span class="sxs-lookup"><span data-stu-id="ab784-102">Adaptive Card Templating SDKs</span></span>

<span data-ttu-id="ab784-103">有了自适应卡片模板化 SDK，就可以轻松地使用任何受支持的平台上的实际数据来填充[卡片模板](language.md)。</span><span class="sxs-lookup"><span data-stu-id="ab784-103">The Adaptive Card Templating SDKs make it easy to populate a [card template](language.md) with real data on any supported platform.</span></span>

> <span data-ttu-id="ab784-104">有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)</span><span class="sxs-lookup"><span data-stu-id="ab784-104">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="ab784-105">这些功能为**预览版，可能会更改**。</span><span class="sxs-lookup"><span data-stu-id="ab784-105">These features are **in preview and subject to change**.</span></span> <span data-ttu-id="ab784-106">我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。</span><span class="sxs-lookup"><span data-stu-id="ab784-106">Your feedback is not only welcome, but  critical to ensure we deliver the features **you** need.</span></span>
> 
> <span data-ttu-id="ab784-107">在初始预览期间仅提供 JavaScript SDK，但 .NET SDK 应该很快就会推出。</span><span class="sxs-lookup"><span data-stu-id="ab784-107">During the initial preview only the JavaScript SDK is available, but a .NET SDK should arrive shortly.</span></span>

## <a name="javascript"></a><span data-ttu-id="ab784-108">JavaScript</span><span class="sxs-lookup"><span data-stu-id="ab784-108">JavaScript</span></span>

<span data-ttu-id="ab784-109">可以通过 npm 和 CDN 获取 [adaptivecards-templating](https://www.npmjs.com/package/adaptivecards-templating) 库。</span><span class="sxs-lookup"><span data-stu-id="ab784-109">The [adaptivecards-templating](https://www.npmjs.com/package/adaptivecards-templating) library is available on npm and via CDN.</span></span> <span data-ttu-id="ab784-110">如需完整文档，请查看包链接。</span><span class="sxs-lookup"><span data-stu-id="ab784-110">See the package link for full documentation.</span></span>

### <a name="npm"></a><span data-ttu-id="ab784-111">npm</span><span class="sxs-lookup"><span data-stu-id="ab784-111">npm</span></span>

```console
npm install adaptivecards-templating
```

### <a name="cdn"></a><span data-ttu-id="ab784-112">CDN</span><span class="sxs-lookup"><span data-stu-id="ab784-112">CDN</span></span>

```html
<script src="https://unpkg.com/adaptivecards-templating/dist/adaptivecards-templating.min.js"></script>
``` 

### <a name="usage"></a><span data-ttu-id="ab784-113">用法</span><span class="sxs-lookup"><span data-stu-id="ab784-113">Usage</span></span>

<span data-ttu-id="ab784-114">以下示例假定你还安装了 [adaptivecards](https://www.npmjs.com/package/adaptivecards) 库来呈现卡。</span><span class="sxs-lookup"><span data-stu-id="ab784-114">The sample below assumes you've also installed the [adaptivecards](https://www.npmjs.com/package/adaptivecards) library in order to render the card.</span></span> 

<span data-ttu-id="ab784-115">如果不打算呈现卡，可以删除 `parse` 和 `render` 代码。</span><span class="sxs-lookup"><span data-stu-id="ab784-115">If you don't plan on rendering the card then you can remove the `parse` and `render` code.</span></span> 

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

## <a name="net"></a><span data-ttu-id="ab784-116">.NET</span><span class="sxs-lookup"><span data-stu-id="ab784-116">.NET</span></span> 

```console
dotnet add package AdaptiveCards.Templating --version 0.1.0-alpha1
```

> [!NOTE]
>
> <span data-ttu-id="ab784-117">请考虑将上述版本更改为最新发布版本</span><span class="sxs-lookup"><span data-stu-id="ab784-117">Consider changing the version above to the latest published version</span></span>

<span data-ttu-id="ab784-118">导入库</span><span class="sxs-lookup"><span data-stu-id="ab784-118">Import the library</span></span> 

```cs
using AdaptiveCards.Templating
```

<span data-ttu-id="ab784-119">可以通过传入模板 JSON 和数据 JSON 来使用模板化引擎。</span><span class="sxs-lookup"><span data-stu-id="ab784-119">Use the templating engine by passing in your template JSON and data JSON.</span></span>

```cs
var templateJson = @"
{
    ""type"": ""AdaptiveCard"",
    ""version"": ""1.0"",
    ""body"": [
        {
            ""type"": ""TextBlock"",
            ""text"": ""Hello {name}""
        }
    ]
}";

var dataJson = @"
{
    ""name"": ""Mickey Mouse""
}";

var transformer = new AdaptiveTransformer();
var cardJson = transformer.Transform(templateJson, dataJson);
```
