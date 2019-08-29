---
title: 主机配置-.NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: dc5b6767d5f8611111b56f30f05a7b5fc8d1cbf4
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552409"
---
# <a name="host-config---net-html"></a>主机配置-.NET HTML

[主机配置](../../../rendering-cards/host-config.md)是所有呈现器都理解的共享配置对象。 可以通过它来定义常见样式（例如，字体系列、字体大小、默认间距）和行为（例如，操作的最大数量）。每个平台呈现器会自动解释这些样式和行为。 

这样的目的是确保每个平台呈现器生成的本机 UI 在外观上非常相似，尽量减少你的工作。

```csharp
// Construct programmatically
renderer.HostConfig = new AdaptiveHostConfig() 
{
    FontFamily = "Comic Sans",
    FontSizes = {
        Small = 15,
        Default = 20,
        Medium = 25,
        Large = 30,
        ExtraLarge= 40
    }
};

// Or parse from JSON
renderer.HostConfig  = AdaptiveHostConfig.FromJson(@"{
    ""fontFamily"": ""Comic Sans"",
    ""fontSizes"": {
        ""small"": 25,
        ""default"": 26,
        ""medium"": 27,
        ""large"": 28,
        ""extraLarge"": 29
    }
}");
```