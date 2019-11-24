---
title: 将 SDK 模板化
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: 3a9bfcd1bf8f87959a747997e04f5c5ad2a79980
ms.sourcegitcommit: 90afb3729931b0e4cae19b17ef9e49453c2d2bf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2019
ms.locfileid: "72163612"
---
# <a name="adaptive-card-templating-sdks"></a>自适应卡模板化 Sdk

自适应卡模板化 Sdk 使你能够轻松地在任何受支持的平台上使用实际数据填充[卡模板](language.md)。

> 有关[自适应卡模板的概述](index.md)，请阅读此概述

> [!IMPORTANT] 
> 
> 这些功能为**预览版，可能会更改**。 我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。
> 
> 在初始预览过程中，仅可使用 JavaScript SDK，但 .NET SDK 应该很快就会到达。

## <a name="javascript"></a>JavaScript

[Adaptivecards 模板](https://www.npmjs.com/package/adaptivecards-templating)库在 npm 上和通过 CDN 提供。 有关完整文档，请参阅包链接。

### <a name="npm"></a>npm

```console
npm install adaptivecards-templating
```

### <a name="cdn"></a>CDN

```html
<script src="https://unpkg.com/adaptivecards-templating/dist/adaptivecards-templating.min.js"></script>
``` 

### <a name="usage"></a>Usage

下面的示例假定还安装了[adaptivecards](https://www.npmjs.com/package/adaptivecards)库，以便呈现卡。 

如果不打算着色卡，可以删除 `parse` 和 `render` 代码。 

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
> 请考虑将上述版本更改为最新发布的版本

导入库 

```cs
using AdaptiveCards.Templating
```

通过传入模板 JSON 和数据 JSON，使用模板化引擎。

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
