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
# <a name="adaptive-card-templating-sdks"></a>自适应卡片模板化 SDK

有了自适应卡片模板化 SDK，就可以轻松地使用任何受支持的平台上的实际数据来填充[卡片模板](language.md)。

> 有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)

> [!IMPORTANT] 
> 
> 这些功能为**预览版，可能会更改**。 我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。
> 
> 在初始预览期间仅提供 JavaScript SDK，但 .NET SDK 应该很快就会推出。

## <a name="javascript"></a>JavaScript

可以通过 npm 和 CDN 获取 [adaptivecards-templating](https://www.npmjs.com/package/adaptivecards-templating) 库。 如需完整文档，请查看包链接。

### <a name="npm"></a>npm

```console
npm install adaptivecards-templating
```

### <a name="cdn"></a>CDN

```html
<script src="https://unpkg.com/adaptivecards-templating/dist/adaptivecards-templating.min.js"></script>
``` 

### <a name="usage"></a>用法

以下示例假定你还安装了 [adaptivecards](https://www.npmjs.com/package/adaptivecards) 库来呈现卡。 

如果不打算呈现卡，可以删除 `parse` 和 `render` 代码。 

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

## <a name="net"></a>.NET 

```console
dotnet add package AdaptiveCards.Templating --version 0.1.0-alpha1
```

> [!NOTE]
>
> 请考虑将上述版本更改为最新发布版本

导入库 

```cs
using AdaptiveCards.Templating
```

可以通过传入模板 JSON 和数据 JSON 来使用模板化引擎。

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
