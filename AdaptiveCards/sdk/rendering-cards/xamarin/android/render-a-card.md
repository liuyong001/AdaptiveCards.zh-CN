---
title: 呈现卡-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: dc1d48e05e99d6254b9253efa7145cefeb2ed17c
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145971"
---
# <a name="render-a-card---xamarinandroid"></a><span data-ttu-id="4020a-102">呈现卡-Xamarin Android</span><span class="sxs-lookup"><span data-stu-id="4020a-102">Render a card - Xamarin.Android</span></span>

<span data-ttu-id="4020a-103">下面介绍如何使用 Xamarin 呈现卡。 Android SDK。</span><span class="sxs-lookup"><span data-stu-id="4020a-103">Here's how to render a card using the Xamarin.Android SDK.</span></span>

## <a name="create-adaptive-card-object-instance-from-json-text"></a><span data-ttu-id="4020a-104">根据 JSON 文本创建自适应卡片对象实例</span><span class="sxs-lookup"><span data-stu-id="4020a-104">Create Adaptive Card Object Instance from JSON Text</span></span>

```csharp
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;
// ...

ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.Version);
AdaptiveCard adaptiveCard = parseResult.AdaptiveCard;
```

<span data-ttu-id="4020a-105">或者，还可以使用 ```ParseContext``` 对象来反序列化自适应卡中包含的自定义元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4020a-105">or you can also use a ```ParseContext``` object to be able to deserialize custom elements that are included in your adaptive card like this:</span></span>

```csharp
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;
// ...

ParseContext context = new ParseContext(); // Empty parseContext so only known elements up to v1.2 will be parsed
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.Version, context);
```

<span data-ttu-id="4020a-106">或</span><span class="sxs-lookup"><span data-stu-id="4020a-106">or</span></span>

```csharp
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;
// ...

ParseContext context = new ParseContext(elementParserRegistration, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.Version, context);
```

## <a name="render-a-card"></a><span data-ttu-id="4020a-107">呈现卡片</span><span class="sxs-lookup"><span data-stu-id="4020a-107">Render a card</span></span>

<span data-ttu-id="4020a-108">若要呈现卡，需要一些信息</span><span class="sxs-lookup"><span data-stu-id="4020a-108">To be able to render a card you'll need some information</span></span>
* <span data-ttu-id="4020a-109">上下文：可从承载卡的活动中获得</span><span class="sxs-lookup"><span data-stu-id="4020a-109">context: Obtainable from the Activity the card is hosted in</span></span>
* <span data-ttu-id="4020a-110">fragmentManager：还可以从托管活动中检索</span><span class="sxs-lookup"><span data-stu-id="4020a-110">fragmentManager: can also be retrieved from the hosting activity</span></span>
* <span data-ttu-id="4020a-111">cardActionHandler：用于管理操作行为的[```ICardActionHandler```](adaptivecards-renderin-xamarin-android-renderer-actionhandler-icardactionhandler.md)实例</span><span class="sxs-lookup"><span data-stu-id="4020a-111">cardActionHandler: instance of [```ICardActionHandler```](adaptivecards-renderin-xamarin-android-renderer-actionhandler-icardactionhandler.md) to manage the action behaviour</span></span>

```csharp
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;
using AdaptiveCards.Rendering.Xamarin.Android.Renderer;
using AdaptiveCards.Rendering.Xamarin.Android.Renderer.ActionHandler;
// ...

var renderedCard = AdaptiveCardRenderer.Instance.Render(context, fragmentManager, adaptiveCard, cardActionHandler, hostConfig);
View v = renderedCard.View;
```
