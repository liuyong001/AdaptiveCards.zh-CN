---
title: .NET SDK 的自适应卡
author: matthidinger
ms.author: mahiding
ms.date: 10/01/2017
ms.topic: article
ms.openlocfilehash: 37dec7651a574194eb00d46014431dfb5764f9b7
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553739"
---
# <a name="net-sdk-for-authoring-cards"></a>用于创作卡.NET SDK

如我们所述[Getting Started](../../authoring-cards/getting-started.md)页上，自适应卡是一个 JSON 对象模型。 .NET 库，可使用该 JSON 容易得多。

> [!IMPORTANT]
> **从 v0.5 的重大更改**
> 
> 1. 从包重命名`Microsoft.AdaptiveCards`到 `AdaptiveCards`
> 1. 由于与 framework 类型的常见名称冲突，而模型的所有类具有已使用作为都前缀"Adaptive"。 例如，`TextBlock`现在 `AdaptiveTextBlock`
> 1. 所有"uri"属性已从类型`string`到 `Uri`
> 1. 也已经 v0.5 预览版中，这是某些架构更改[此处所述](https://github.com/Microsoft/AdaptiveCards/pull/633)


## <a name="nuget-install"></a>NuGet 安装
`AdaptiveCards` NuGet 包提供用于使用与在.NET 中的自适应卡类型

[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.svg)](https://www.nuget.org/packages/AdaptiveCards)

```console
Install-Package AdaptiveCards -IncludePrerelease
```

## <a name="example-create-an-adaptivecard-and-serialize-to-json"></a>例如：创建 AdaptiveCard 和序列化到 JSON

此示例演示如何构建自适应卡使用标准C#对象，然后其序列化为 JSON 的传输通过缆线。

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

## <a name="example-parse-an-adaptivecard-from-json"></a>例如：分析从 JSON AdaptiveCard

此示例演示如何分析 JSON 有效负载为自适应卡。 这样就可以轻松来操作对象模型或甚至使用您的应用程序内呈现自适应卡我们[呈现器 Sdk](../../rendering-cards/getting-started.md)。

```csharp
try
{
    // Get a JSON-serialized payload
    // Your app will probably get cards from somewhere else :)
    var client = new HttpClient("http://adaptivecards.io/payloads/ActivityUpdate.json");
    var response = await client.GetAsync(cardUrl);
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
