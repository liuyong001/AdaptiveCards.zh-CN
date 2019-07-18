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
# <a name="render-a-card---android"></a>呈现卡片 - Android

下面介绍如何使用 Android SDK 来呈现卡片。

## <a name="create-adaptive-card-object-instance-from-json-text"></a>根据 JSON 文本创建自适应卡片对象实例

```java
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, elementParserRegistration);
AdaptiveCard adaptiveCard = parseResult.GetAdaptiveCard();
```
> [!IMPORTANT]
> **v1.2 的重大更改**
> 

1. ElementParserRegistration 参数已更改为 ParseContext, 其中包含 ElementParserRegistration 和 ActionParserRegistration 对象

```java
ParseContext context = new ParseContext(); // Empty parseContext so only known elements up to v1.2 will be parsed
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

或

```java
ParseContext context = new ParseContext(elementParserRegistration, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

## <a name="render-a-card"></a>呈现卡片

```java
RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, adaptiveCard, cardActionHandler, hostConfig);
View v = renderedCard.getView();
```
