---
title: 呈现卡片 - Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: 55e0fa828abf3b9af857d1deb7ecd3744b5a7280
ms.sourcegitcommit: 8c8067206f283d97a5aa4ec65ba23d3fe18962f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2019
ms.locfileid: "68299518"
---
# <a name="render-a-card---android"></a><span data-ttu-id="9ce5a-102">呈现卡片 - Android</span><span class="sxs-lookup"><span data-stu-id="9ce5a-102">Render a card - Android</span></span>

<span data-ttu-id="9ce5a-103">下面介绍如何使用 Android SDK 来呈现卡片。</span><span class="sxs-lookup"><span data-stu-id="9ce5a-103">Here's how to render a card using the Android SDK.</span></span>

## <a name="create-adaptive-card-object-instance-from-json-text"></a><span data-ttu-id="9ce5a-104">根据 JSON 文本创建自适应卡片对象实例</span><span class="sxs-lookup"><span data-stu-id="9ce5a-104">Create Adaptive Card Object Instance from JSON Text</span></span>

```java
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, elementParserRegistration);
AdaptiveCard adaptiveCard = parseResult.GetAdaptiveCard();
```
> [!IMPORTANT]
> <span data-ttu-id="9ce5a-105">**v1.2 的重大更改**</span><span class="sxs-lookup"><span data-stu-id="9ce5a-105">**Breaking changes for v1.2**</span></span>
> 

1. <span data-ttu-id="9ce5a-106">ElementParserRegistration 参数已更改为 ParseContext, 其中包含 ElementParserRegistration 和 ActionParserRegistration 对象</span><span class="sxs-lookup"><span data-stu-id="9ce5a-106">ElementParserRegistration parameter changed to ParseContext which includes an ElementParserRegistration and an ActionParserRegistration object</span></span>

```java
ParseContext context = new ParseContext(); // Empty parseContext so only known elements up to v1.2 will be parsed
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

<span data-ttu-id="9ce5a-107">或</span><span class="sxs-lookup"><span data-stu-id="9ce5a-107">or</span></span>

```java
ParseContext context = new ParseContext(elementParserRegistration, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

## <a name="render-a-card"></a><span data-ttu-id="9ce5a-108">呈现卡片</span><span class="sxs-lookup"><span data-stu-id="9ce5a-108">Render a card</span></span>

```java
RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, adaptiveCard, cardActionHandler, hostConfig);
View v = renderedCard.getView();
```
