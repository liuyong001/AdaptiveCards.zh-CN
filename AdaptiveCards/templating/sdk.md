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
# <a name="adaptive-card-templating-sdks"></a>自适应卡模板化 Sdk

自适应卡模板化 Sdk 使你能够轻松地在任何受支持的平台上使用实际数据填充[卡模板](language.md)。

> 有关[自适应卡模板的概述](index.md), 请阅读此概述

> [!IMPORTANT] 
> 
> 这些功能**处于预览阶段, 可能会有所更改**。 你的反馈不仅是欢迎的, 而且确保我们能够提供**所**需的功能至关重要。
> 
> 在初始预览过程中, 仅可使用 JavaScript SDK, 但 .NET SDK 应该很快就会到达。

## <a name="javascript"></a>JavaScript

[Adaptivecards 模板](https://www.npmjs.com/package/adaptivecards-templating)库在 npm 上和通过 CDN 提供。 有关完整文档, 请参阅包链接。

### <a name="npm"></a>npm

```console
npm install adaptivecards-templating
```

### <a name="cdn"></a>CDN

```html
<script src="https://unpkg.com/adaptivecards-templating/dist/adaptivecards-templating.min.js"></script>
``` 

### <a name="usage"></a>用法

下面的示例假定还安装了[adaptivecards](https://www.npmjs.com/package/adaptivecards)库, 以便呈现卡。 

如果不打算呈现卡`parse` , 则可以删除和`render`代码。 

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

## <a name="net-coming-soon"></a>.NET (即将*推出*)

尚未工作: 

```console
nuget install AdaptiveCards.Templating
```
