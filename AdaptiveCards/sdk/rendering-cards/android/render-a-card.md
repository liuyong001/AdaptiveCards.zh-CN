---
title: 呈现卡片的 Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: b93ce97a41152641892e6a69d5221842181fcb72
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552509"
---
# <a name="render-a-card---android"></a><span data-ttu-id="f136c-102">呈现卡-Android</span><span class="sxs-lookup"><span data-stu-id="f136c-102">Render a card - Android</span></span>

<span data-ttu-id="f136c-103">下面介绍了如何呈现使用 Android SDK 的卡。</span><span class="sxs-lookup"><span data-stu-id="f136c-103">Here's how to render a card using the Android SDK.</span></span>

## <a name="create-adaptive-card-object-instance-from-json-text"></a><span data-ttu-id="f136c-104">从 JSON 文本创建自适应卡对象实例</span><span class="sxs-lookup"><span data-stu-id="f136c-104">Create Adaptive Card Object Instance from JSON Text</span></span>

```java
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION);
AdaptiveCard adaptiveCard = parseResult.GetAdaptiveCard();
```

## <a name="render-a-card"></a><span data-ttu-id="f136c-105">呈现数据卡</span><span class="sxs-lookup"><span data-stu-id="f136c-105">Render a card</span></span>

```java
RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, getSupportFragmentManager(), adaptiveCard, cardActionHandler, new HostConfig());
View v = renderedCard.getView();
```