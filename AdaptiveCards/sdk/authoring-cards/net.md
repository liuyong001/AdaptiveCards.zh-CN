---
title: .NET SDK for 自适应卡
author: matthidinger
ms.author: mahiding
ms.date: 10/01/2017
ms.topic: article
ms.openlocfilehash: fa86d83a8f20490ec286b69653099ac8cd81b8ef
ms.sourcegitcommit: 4d80c553ab574befa8c84706fd85d22077915745
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68387346"
---
# <a name="net-sdk-for-authoring-cards"></a>用于创作插件的 .NET SDK

如我们在[入门](../../authoring-cards/getting-started.md)"页中所述, 自适应卡是一个 JSON 对象模型。 .NET 库可以更轻松地使用该 JSON。

> [!IMPORTANT]
> **V 0.5 中的重大更改**
> 
> 1. 包已从`Microsoft.AdaptiveCards`重命名为`AdaptiveCards`
> 1. 由于经常与框架类型发生名称冲突, 所有模型类都以 "自适应" 为前缀。 例如, `TextBlock`现在为`AdaptiveTextBlock`
> 1. 所有 "uri" 属性已从类型`string`更改为`Uri`
> 1. 前面的0.5 个预览中也有一些架构更改,[这里概述](https://github.com/Microsoft/AdaptiveCards/pull/633)了这些更改


## <a name="nuget-install"></a>NuGet 安装
`AdaptiveCards` NuGet 包提供了在 .net 中使用自适应卡的类型

[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.svg)](https://www.nuget.org/packages/AdaptiveCards)

```console
Install-Package AdaptiveCards -IncludePrerelease
```

## <a name="example-create-an-adaptivecard-and-serialize-to-json"></a>例如：创建 AdaptiveCard 并序列化为 JSON

此示例演示如何使用标准C#对象构建自适应卡, 然后将其序列化为 JSON, 以便通过网络进行传输。

```csharp
using AdaptiveCards;
// ...

AdaptiveCard card = new AdaptiveCard();

card.Body.Add(new AdaptiveTextBlock() 
{
    Text = "Hello",
    Size = AdaptiveTextSize.ExtraLarge
});

card.Body.Add(new AdaptiveImage() 
{
    Url = new Uri("http://adaptivecards.io/content/cats/1.png")
});

// serialize the card to JSON
string json = card.ToJson();
```

## <a name="example-parse-an-adaptivecard-from-json"></a>例如：分析 JSON 中的 AdaptiveCard

此示例演示如何将 JSON 有效负载分析为自适应卡。 这样就可以轻松地处理对象模型, 甚至可以使用[呈现器 sdk](../../rendering-cards/getting-started.md)在应用程序中呈现自适应卡。

```csharp
try
{
    // Get a JSON-serialized payload
    // Your app will probably get cards from somewhere else :)
    var client = new HttpClient();
    var response = await client.GetAsync("http://adaptivecards.io/payloads/ActivityUpdate.json");
    var json = await response.Content.ReadAsStringAsync();

    // Parse the JSON 
    AdaptiveCardParseResult result = AdaptiveCard.FromJson(json);

    // Get card from result
    AdaptiveCard card = result.Card;

    // Optional: check for any parse warnings
    // This includes things like unknown element "type"
    // or unknown properties on element
    IList<AdaptiveWarning> warnings = result.Warnings;
}
catch(AdaptiveSerializationException ex)
{
    // Failed to deserialize card 
    // This occurs from malformed JSON
    // or schema violations like required properties missing 
}
```
