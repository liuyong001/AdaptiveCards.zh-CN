---
title: 主机配置-UWP SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 6f14830a643b064c6169cf3143bbc7cd4ce45937
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454970"
---
# <a name="host-config---uwp"></a>主机配置-UWP

若要自定义呈现器，请提供 HostConfig 对象的实例。 （有关完整的说明，请参阅[主机配置架构](../../../rendering-cards/host-config.md)。）

> HostConfig 对象将用默认值实例化，因此你可以仅设置要更改的属性。

示例：

```csharp
var hostConfig = new AdaptiveHostConfig() 
{
    FontSizes = {
        Small = 15,
        Normal = 20,
        Medium = 25,
        Large = 30,
        ExtraLarge= 40
    }
};
renderer.HostConfig = hostConfig;
```

> 或者，可以从 JSON 字符串加载 HostConfig。

示例：

```csharp
var hostConfig = AdaptiveHostConfig.FromJsonString(jsonString); 

renderer.HostConfig = hostConfig;
```

在将其传递给 UWPRenderer 时，将设置默认的 HostConfig，以便将其用于每个呈现的卡。