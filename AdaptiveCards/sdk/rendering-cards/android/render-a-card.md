---
title: 呈现卡片 - Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: c9fbfa788af0b0c7f16824bf9c369fa59a1b80f5
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145467"
---
# <a name="render-a-card---android"></a><span data-ttu-id="6920a-102">呈现卡片 - Android</span><span class="sxs-lookup"><span data-stu-id="6920a-102">Render a card - Android</span></span>

<span data-ttu-id="6920a-103">下面介绍如何使用 Android SDK 来呈现卡片。</span><span class="sxs-lookup"><span data-stu-id="6920a-103">Here's how to render a card using the Android SDK.</span></span>

## <a name="create-adaptive-card-object-instance-from-json-text"></a><span data-ttu-id="6920a-104">根据 JSON 文本创建自适应卡片对象实例</span><span class="sxs-lookup"><span data-stu-id="6920a-104">Create Adaptive Card Object Instance from JSON Text</span></span>

```java
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, elementParserRegistration);
AdaptiveCard adaptiveCard = parseResult.GetAdaptiveCard();
```
> [!IMPORTANT]
> <span data-ttu-id="6920a-105">**v1.2 的重大更改**</span><span class="sxs-lookup"><span data-stu-id="6920a-105">**Breaking changes for v1.2**</span></span>
> 

1. <span data-ttu-id="6920a-106">ElementParserRegistration 参数已更改为 ParseContext，其中包含 ElementParserRegistration 和 ActionParserRegistration 对象</span><span class="sxs-lookup"><span data-stu-id="6920a-106">ElementParserRegistration parameter changed to ParseContext which includes an ElementParserRegistration and an ActionParserRegistration object</span></span>

```java
ParseContext context = new ParseContext(); // Empty parseContext so only known elements up to v1.2 will be parsed
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

<span data-ttu-id="6920a-107">或</span><span class="sxs-lookup"><span data-stu-id="6920a-107">or</span></span>

```java
ParseContext context = new ParseContext(elementParserRegistration, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

## <a name="render-a-card"></a><span data-ttu-id="6920a-108">呈现卡片</span><span class="sxs-lookup"><span data-stu-id="6920a-108">Render a card</span></span>

```java
RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, adaptiveCard, cardActionHandler, hostConfig);
View v = renderedCard.getView();
```
