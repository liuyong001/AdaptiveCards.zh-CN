---
title: 将 SDK 模板化
author: matthidinger
ms.author: mahiding
ms.date: 05/15/2020
ms.topic: article
ms.openlocfilehash: dc20c22995bb0a259bc801a6ffcd674967bbe78f
ms.sourcegitcommit: c921a7bb15a95c0ceb803ad375501ee3b8bef028
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83631349"
---
# <a name="adaptive-card-templating-sdks"></a>自适应卡片模板化 SDK

有了自适应卡片模板化 SDK，就可以轻松地使用任何受支持的平台上的实际数据来填充[卡片模板](language.md)。

> 有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)

> [!IMPORTANT] 
> 
> **2020 年 5 月候选发布版本**中的**中断性变更**
>
> 我们正在努力工作，力求尽早发布模板，我们已经在做最后的冲刺了！ 发布之前，我们需要进行一些小的中断性变更。

## <a name="breaking-changes-as-of-may-2020"></a>2020 年 5 月起的中断性变更

1. 绑定语法已从 `{...}` 更改为 `${...}`。 
    * 例如：`"text": "Hello {name}"` 变为 `"text": "Hello ${name}"`
2. JavaScript API 不再包含 `EvaluationContext` 对象。 只需将数据传递到 `expand` 函数。 有关完整的详细信息，请参阅 [SDK 页](sdk.md)。
3. .NET API 经过了重新设计，以便更紧密地匹配 JavaScript API。 有关完整详细信息，请查看以下内容。

## <a name="javascript"></a>JavaScript

可以通过 npm 和 CDN 获取 [adaptivecards-templating](https://www.npmjs.com/package/adaptivecards-templating) 库。 如需完整文档，请查看包链接。

### <a name="npm"></a>npm

[![npm install](https://img.shields.io/npm/v/adaptivecards-templating.svg)](https://www.npmjs.com/package/adaptivecards-templating)

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
            "text": "Hello ${name}!"
        }
    ]
};
 
// Create a Template instamce from the template payload
var template = new ACData.Template(templatePayload);
 
// Expand the template with your `$root` data object.
// This binds it to the data and produces the final Adaptive Card payload
var cardPayload = template.expand({
   $root: {
      name: "Matt Hidinger"
   }
});
 
// OPTIONAL: Render the card (required the adaptivecards library loaded)
var adaptiveCard = new AdaptiveCards.AdaptiveCard();
adaptiveCard.parse(cardPayload);
 
var htmlElement = adaptiveCard.render();
```

## <a name="net"></a>.NET 

> [!IMPORTANT] 
> 
> .NET 候选发布版本将于 5 月 23 日左右发布。 查找版本 `1.0.0-RC1`
>

[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Templating.svg)](https://www.nuget.org/packages/AdaptiveCards.Templating)

```console
dotnet add package AdaptiveCards.Templating
```

### <a name="usage"></a>用法

```cs
// Import the library 
using AdaptiveCards.Templating;
```

```cs
var templateJson = @"
{
    ""type"": ""AdaptiveCard"",
    ""version"": ""1.2"",
    ""body"": [
        {
            ""type"": ""TextBlock"",
            ""text"": ""Hello ${name}!""
        }
    ]
}";

// Create a Template instance from the template payload
AdaptiveCardTemplate template = new AdaptiveCardTemplate(templateJson);

// You can use any serializable object as your data
var myData = new
{
    Name = "Matt Hidinger"
};

// "Expand" the template - this generates the final Adaptive Card payload
string cardJson = template.Expand(myData);
```

### <a name="custom-functions"></a>自定义函数

除了预生成函数外，还可以将自定义函数添加到自适应表达式库中。

下面的示例中添加了 stringFormat 自定义函数，并使用该函数设置字符串的格式。
```cs
string jsonTemplate = @"{
    ""type"": ""AdaptiveCard"",
    ""version"": ""1.0"",
    ""body"": [{
        ""type"": ""TextBlock"",
        ""text"": ""${stringFormat(strings.myName, person.firstName, person.lastName)}""
    }]
}";

string jsonData = @"{
    ""strings"": {
        ""myName"": ""My name is {0} {1}""
    },
    ""person"": {
        ""firstName"": ""Andrew"",
        ""lastName"": ""Leader""
    }
}";

AdaptiveCardTemplate template = new AdaptiveCardTemplate(jsonTemplate);

var context = new EvaluationContext
{
    Root = jsonData
};

// a custom function is added
AdaptiveExpressions.Expression.Functions.Add("stringFormat", (args) =>
{
    string formattedString = "";

    // argument is packed in sequential order as defined in the template
    // For example, suppose we have "${stringFormat(strings.myName, person.firstName, person.lastName)}"
    // args will have following entries
    // args[0]: strings.myName
    // args[1]: person.firstName
    // args[2]: strings.lastName
    if (args[0] != null && args[1] != null && args[2] != null) 
    {
        string formatString = args[0];
        string[] stringArguments = {args[1], args[2] };
        formattedString = string.Format(formatString, stringArguments);
    }
    return formattedString;
});

string cardJson = template.Expand(context);
```

## <a name="troubleshooting"></a>疑难解答
问： 我为什么会遇到 AdaptiveTemplateException ```expand()```？   
A. 如果错误消息看上去类似于 '\<offending item>' at line, '\<line number>' is **malformed for '$data : ' pair**"。   
请确保为 "$data" 提供的值是有效的 json，如数字、布尔值、对象和数组，或确保正确使用了自适应模板语言的语法，条目在数据上下文中的行号处。 请注意，${LineItem} 和“8”可以更改。

问： 我为什么会遇到 ArgumentNullException ```expand()```？   
A. 如果错误消息看起来类似于 "**Check if parent data context is set, or please enter a non-null value for** '\<offending item>' at line, '\<line number>'"。   
它指示不存在所请求的数据绑定的数据上下文。 请确保设置了根数据上下文，如果存在，请确保有数据上下文可用于行号所指示的当前绑定。
