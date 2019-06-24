---
title: 呈现卡片 - Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: a4eeda54a80c959ff9a1246371240954b4c3fb12
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67134288"
---
# <a name="render-a-card---android"></a><span data-ttu-id="0d5f0-102">呈现卡片 - Android</span><span class="sxs-lookup"><span data-stu-id="0d5f0-102">Render a card - Android</span></span>

<span data-ttu-id="0d5f0-103">下面介绍如何使用 Android SDK 来呈现卡片。</span><span class="sxs-lookup"><span data-stu-id="0d5f0-103">Here's how to render a card using the Android SDK.</span></span>

## <a name="create-adaptive-card-object-instance-from-json-text"></a><span data-ttu-id="0d5f0-104">根据 JSON 文本创建自适应卡片对象实例</span><span class="sxs-lookup"><span data-stu-id="0d5f0-104">Create Adaptive Card Object Instance from JSON Text</span></span>

```java
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, elementParserRegistration);
AdaptiveCard adaptiveCard = parseResult.GetAdaptiveCard();
```
> [!IMPORTANT]
> <span data-ttu-id="0d5f0-105">**v1.2 的重大更改**</span><span class="sxs-lookup"><span data-stu-id="0d5f0-105">**Breaking changes for v1.2**</span></span>
> 
> 1. <span data-ttu-id="0d5f0-106">ElementParserRegistration 参数已更改为 ParseContext，后者包括 ElementParserRegistration 和 ActionRegistration 对象</span><span class="sxs-lookup"><span data-stu-id="0d5f0-106">ElementParserRegistration parameter changed to ParseContext which includes an ElementParserRegistration and an ActionRegistration object</span></span>
> ```java
> ParseContext context = new ParseContext(elementParserRegistration, actionParserRegistration);
> ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
> ```

## <a name="render-a-card"></a><span data-ttu-id="0d5f0-107">呈现卡片</span><span class="sxs-lookup"><span data-stu-id="0d5f0-107">Render a card</span></span>

```java
RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, getSupportFragmentManager(), adaptiveCard, cardActionHandler, new HostConfig());
View v = renderedCard.getView();
```
