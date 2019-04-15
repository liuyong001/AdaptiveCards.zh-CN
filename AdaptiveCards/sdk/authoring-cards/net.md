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
# <a name="net-sdk-for-authoring-cards"></a><span data-ttu-id="8c38b-102">用于创作卡.NET SDK</span><span class="sxs-lookup"><span data-stu-id="8c38b-102">.NET SDK for Authoring Cards</span></span>

<span data-ttu-id="8c38b-103">如我们所述[Getting Started](../../authoring-cards/getting-started.md)页上，自适应卡是一个 JSON 对象模型。</span><span class="sxs-lookup"><span data-stu-id="8c38b-103">As we described in the [Getting Started](../../authoring-cards/getting-started.md) page, an Adaptive Card is a JSON object model.</span></span> <span data-ttu-id="8c38b-104">.NET 库，可使用该 JSON 容易得多。</span><span class="sxs-lookup"><span data-stu-id="8c38b-104">The .NET library makes working with that JSON much easier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8c38b-105">**从 v0.5 的重大更改**</span><span class="sxs-lookup"><span data-stu-id="8c38b-105">**Breaking changes from v0.5**</span></span>
> 
> 1. <span data-ttu-id="8c38b-106">从包重命名`Microsoft.AdaptiveCards`到 `AdaptiveCards`</span><span class="sxs-lookup"><span data-stu-id="8c38b-106">Package renamed from `Microsoft.AdaptiveCards` to `AdaptiveCards`</span></span>
> 1. <span data-ttu-id="8c38b-107">由于与 framework 类型的常见名称冲突，而模型的所有类具有已使用作为都前缀"Adaptive"。</span><span class="sxs-lookup"><span data-stu-id="8c38b-107">Due to frequent name collisions with framework types, all model classes have been prefixed with "Adaptive".</span></span> <span data-ttu-id="8c38b-108">例如，`TextBlock`现在 `AdaptiveTextBlock`</span><span class="sxs-lookup"><span data-stu-id="8c38b-108">E.g., `TextBlock` is now `AdaptiveTextBlock`</span></span>
> 1. <span data-ttu-id="8c38b-109">所有"uri"属性已从类型`string`到 `Uri`</span><span class="sxs-lookup"><span data-stu-id="8c38b-109">All "uri" properties were changed from type `string` to `Uri`</span></span>
> 1. <span data-ttu-id="8c38b-110">也已经 v0.5 预览版中，这是某些架构更改[此处所述](https://github.com/Microsoft/AdaptiveCards/pull/633)</span><span class="sxs-lookup"><span data-stu-id="8c38b-110">There have also been some schema changes from the v0.5 preview, which are [outlined here](https://github.com/Microsoft/AdaptiveCards/pull/633)</span></span>


## <a name="nuget-install"></a><span data-ttu-id="8c38b-111">NuGet 安装</span><span class="sxs-lookup"><span data-stu-id="8c38b-111">NuGet Install</span></span>
<span data-ttu-id="8c38b-112">`AdaptiveCards` NuGet 包提供用于使用与在.NET 中的自适应卡类型</span><span class="sxs-lookup"><span data-stu-id="8c38b-112">The `AdaptiveCards` NuGet package provides types for working with adaptive cards in .NET</span></span>

<span data-ttu-id="8c38b-113">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.svg)](https://www.nuget.org/packages/AdaptiveCards)</span><span class="sxs-lookup"><span data-stu-id="8c38b-113">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.svg)](https://www.nuget.org/packages/AdaptiveCards)</span></span>

```console
Install-Package AdaptiveCards -IncludePrerelease
```

## <a name="example-create-an-adaptivecard-and-serialize-to-json"></a><span data-ttu-id="8c38b-114">例如：创建 AdaptiveCard 和序列化到 JSON</span><span class="sxs-lookup"><span data-stu-id="8c38b-114">Example: Create an AdaptiveCard and serialize to JSON</span></span>

<span data-ttu-id="8c38b-115">此示例演示如何构建自适应卡使用标准C#对象，然后其序列化为 JSON 的传输通过缆线。</span><span class="sxs-lookup"><span data-stu-id="8c38b-115">This example demonstrates how to build an Adaptive Card using standard C# objects and then serialize it to JSON for transport over the wire.</span></span>

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

## <a name="example-parse-an-adaptivecard-from-json"></a><span data-ttu-id="8c38b-116">例如：分析从 JSON AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="8c38b-116">Example: Parse an AdaptiveCard from JSON</span></span>

<span data-ttu-id="8c38b-117">此示例演示如何分析 JSON 有效负载为自适应卡。</span><span class="sxs-lookup"><span data-stu-id="8c38b-117">This example demonstrates how to parse a JSON payload into an Adaptive Card.</span></span> <span data-ttu-id="8c38b-118">这样就可以轻松来操作对象模型或甚至使用您的应用程序内呈现自适应卡我们[呈现器 Sdk](../../rendering-cards/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="8c38b-118">This makes it easy to manipulate the object model or even render Adaptive Cards inside your app by using our [renderer SDKs](../../rendering-cards/getting-started.md).</span></span>

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
