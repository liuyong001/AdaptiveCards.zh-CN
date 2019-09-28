---
title: .NET SDK for 自适应卡
author: matthidinger
ms.author: mahiding
ms.date: 10/01/2017
ms.topic: article
ms.openlocfilehash: 10400d5db3aac8ea60e5f03f5ab5d9b013211954
ms.sourcegitcommit: 4dd40521cd39313657f1dab642f49ff04098ba35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71343735"
---
# <a name="net-sdk-for-authoring-cards"></a>用于创作插件的 .NET SDK

如我们在[入门](../../authoring-cards/getting-started.md)"页中所述, 自适应卡是一个 JSON 对象模型。 .NET 库可以更轻松地使用该 JSON。


## <a name="nuget-install"></a>NuGet 安装
`AdaptiveCards` NuGet 包提供了在 .net 中使用自适应卡的类型

[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.svg)](https://www.nuget.org/packages/AdaptiveCards)

```console
Install-Package AdaptiveCards
```

## <a name="example-create-an-adaptivecard-and-serialize-to-json"></a>例如：创建 AdaptiveCard 并序列化为 JSON

此示例演示如何使用标准C#对象构建自适应卡, 然后将其序列化为 JSON, 以便通过网络进行传输。

```csharp
using AdaptiveCards;
// ...

AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion(1, 0));

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
