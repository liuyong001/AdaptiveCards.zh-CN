---
title: 呈现卡-UWP SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 1a72cb9ba72811d4e98a48116fa08245e13a6392
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552429"
---
# <a name="render-a-card---uwp"></a><span data-ttu-id="da860-102">呈现卡-UWP</span><span class="sxs-lookup"><span data-stu-id="da860-102">Render a card - UWP</span></span>

<span data-ttu-id="da860-103">下面介绍了如何呈现使用 UWP SDK 的卡。</span><span class="sxs-lookup"><span data-stu-id="da860-103">Here's how to render a card using the UWP SDK.</span></span>

## <a name="create-an-instance-of-your-renderer"></a><span data-ttu-id="da860-104">创建您的呈现器的实例</span><span class="sxs-lookup"><span data-stu-id="da860-104">Create an instance of your renderer</span></span>

<span data-ttu-id="da860-105">创建呈现器库的实例。</span><span class="sxs-lookup"><span data-stu-id="da860-105">Create an instance of the renderer library.</span></span> 

```csharp
using AdaptiveCards.Rendering.Uwp;
// ...

var renderer = new AdaptiveCardRenderer();
```

## <a name="create-a-card-from-a-json-string"></a><span data-ttu-id="da860-106">从 JSON 字符串创建卡片</span><span class="sxs-lookup"><span data-stu-id="da860-106">Create a card from a JSON string</span></span>

```csharp
var card = AdaptiveCard.FromJsonString(jsonString);
```

## <a name="create-a-card-from-a-json-object"></a><span data-ttu-id="da860-107">从 JSON 对象中创建卡片</span><span class="sxs-lookup"><span data-stu-id="da860-107">Create a card from a JSON object</span></span>

```csharp
var card = AdaptiveCard.FromJson(jsonObject);
```

## <a name="render-a-card"></a><span data-ttu-id="da860-108">呈现数据卡</span><span class="sxs-lookup"><span data-stu-id="da860-108">Render a card</span></span>

<span data-ttu-id="da860-109">获取源的数据卡，并将其呈现。</span><span class="sxs-lookup"><span data-stu-id="da860-109">Acquire a card from a source and render it.</span></span>

```csharp
RenderedAdaptiveCard renderedAdaptiveCard =  renderer.RenderAdaptiveCard(card);

// Check if the render was successful
if (renderedAdaptiveCard.FrameworkElement != null)
{
    // Get the framework element
    var uiCard = renderedAdaptiveCard.FrameworkElement;

    // Add it to your UI
    myGrid.Children.Add(uiCard);
}
```

## <a name="example"></a><span data-ttu-id="da860-110">示例</span><span class="sxs-lookup"><span data-stu-id="da860-110">Example</span></span>

<span data-ttu-id="da860-111">下面是 UWP 呈现器中的示例。</span><span class="sxs-lookup"><span data-stu-id="da860-111">Here is an example from the UWP renderer.</span></span>

```csharp
var renderer = new AdaptiveCardRenderer();
var card = AdaptiveCard.FromJsonString(jsonString);
var renderedAdaptiveCard = renderer.RenderAdaptiveCard(card.AdaptiveCard);
if (renderedAdaptiveCard.FrameworkElement != null)
{
    myGrid.Children.Add(renderedAdaptiveCard.FrameworkElement);
}
...
```