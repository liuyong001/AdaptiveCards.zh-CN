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
# <a name="net-sdk-for-authoring-cards"></a><span data-ttu-id="4e9d6-102">用于创作插件的 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4e9d6-102">.NET SDK for Authoring Cards</span></span>

<span data-ttu-id="4e9d6-103">如我们在[入门](../../authoring-cards/getting-started.md)"页中所述, 自适应卡是一个 JSON 对象模型。</span><span class="sxs-lookup"><span data-stu-id="4e9d6-103">As we described in the [Getting Started](../../authoring-cards/getting-started.md) page, an Adaptive Card is a JSON object model.</span></span> <span data-ttu-id="4e9d6-104">.NET 库可以更轻松地使用该 JSON。</span><span class="sxs-lookup"><span data-stu-id="4e9d6-104">The .NET library makes working with that JSON much easier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e9d6-105">**V 0.5 中的重大更改**</span><span class="sxs-lookup"><span data-stu-id="4e9d6-105">**Breaking changes from v0.5**</span></span>
> 
> 1. <span data-ttu-id="4e9d6-106">包已从`Microsoft.AdaptiveCards`重命名为`AdaptiveCards`</span><span class="sxs-lookup"><span data-stu-id="4e9d6-106">Package renamed from `Microsoft.AdaptiveCards` to `AdaptiveCards`</span></span>
> 1. <span data-ttu-id="4e9d6-107">由于经常与框架类型发生名称冲突, 所有模型类都以 "自适应" 为前缀。</span><span class="sxs-lookup"><span data-stu-id="4e9d6-107">Due to frequent name collisions with framework types, all model classes have been prefixed with "Adaptive".</span></span> <span data-ttu-id="4e9d6-108">例如, `TextBlock`现在为`AdaptiveTextBlock`</span><span class="sxs-lookup"><span data-stu-id="4e9d6-108">E.g., `TextBlock` is now `AdaptiveTextBlock`</span></span>
> 1. <span data-ttu-id="4e9d6-109">所有 "uri" 属性已从类型`string`更改为`Uri`</span><span class="sxs-lookup"><span data-stu-id="4e9d6-109">All "uri" properties were changed from type `string` to `Uri`</span></span>
> 1. <span data-ttu-id="4e9d6-110">前面的0.5 个预览中也有一些架构更改,[这里概述](https://github.com/Microsoft/AdaptiveCards/pull/633)了这些更改</span><span class="sxs-lookup"><span data-stu-id="4e9d6-110">There have also been some schema changes from the v0.5 preview, which are [outlined here](https://github.com/Microsoft/AdaptiveCards/pull/633)</span></span>


## <a name="nuget-install"></a><span data-ttu-id="4e9d6-111">NuGet 安装</span><span class="sxs-lookup"><span data-stu-id="4e9d6-111">NuGet Install</span></span>
<span data-ttu-id="4e9d6-112">`AdaptiveCards` NuGet 包提供了在 .net 中使用自适应卡的类型</span><span class="sxs-lookup"><span data-stu-id="4e9d6-112">The `AdaptiveCards` NuGet package provides types for working with adaptive cards in .NET</span></span>

<span data-ttu-id="4e9d6-113">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.svg)](https://www.nuget.org/packages/AdaptiveCards)</span><span class="sxs-lookup"><span data-stu-id="4e9d6-113">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.svg)](https://www.nuget.org/packages/AdaptiveCards)</span></span>

```console
Install-Package AdaptiveCards -IncludePrerelease
```

## <a name="example-create-an-adaptivecard-and-serialize-to-json"></a><span data-ttu-id="4e9d6-114">例如：创建 AdaptiveCard 并序列化为 JSON</span><span class="sxs-lookup"><span data-stu-id="4e9d6-114">Example: Create an AdaptiveCard and serialize to JSON</span></span>

<span data-ttu-id="4e9d6-115">此示例演示如何使用标准C#对象构建自适应卡, 然后将其序列化为 JSON, 以便通过网络进行传输。</span><span class="sxs-lookup"><span data-stu-id="4e9d6-115">This example demonstrates how to build an Adaptive Card using standard C# objects and then serialize it to JSON for transport over the wire.</span></span>

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

## <a name="example-parse-an-adaptivecard-from-json"></a><span data-ttu-id="4e9d6-116">例如：分析 JSON 中的 AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="4e9d6-116">Example: Parse an AdaptiveCard from JSON</span></span>

<span data-ttu-id="4e9d6-117">此示例演示如何将 JSON 有效负载分析为自适应卡。</span><span class="sxs-lookup"><span data-stu-id="4e9d6-117">This example demonstrates how to parse a JSON payload into an Adaptive Card.</span></span> <span data-ttu-id="4e9d6-118">这样就可以轻松地处理对象模型, 甚至可以使用[呈现器 sdk](../../rendering-cards/getting-started.md)在应用程序中呈现自适应卡。</span><span class="sxs-lookup"><span data-stu-id="4e9d6-118">This makes it easy to manipulate the object model or even render Adaptive Cards inside your app by using our [renderer SDKs](../../rendering-cards/getting-started.md).</span></span>

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
