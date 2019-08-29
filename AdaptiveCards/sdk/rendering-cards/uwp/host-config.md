---
title: 主机配置-UWP SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 85c8807d2a368e00b414b427fae8a9f0253873c8
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553669"
---
# <a name="host-config---uwp"></a><span data-ttu-id="b98fe-102">主机配置-UWP</span><span class="sxs-lookup"><span data-stu-id="b98fe-102">Host config - UWP</span></span>

<span data-ttu-id="b98fe-103">若要自定义呈现器, 请提供 HostConfig 对象的实例。</span><span class="sxs-lookup"><span data-stu-id="b98fe-103">To customize the renderer you provide an instance of the HostConfig object.</span></span> <span data-ttu-id="b98fe-104">(有关完整的说明, 请参阅[主机配置架构](../../../rendering-cards/host-config.md)。)</span><span class="sxs-lookup"><span data-stu-id="b98fe-104">(See [Host Config Schema](../../../rendering-cards/host-config.md) for the full description.)</span></span>

> <span data-ttu-id="b98fe-105">HostConfig 对象将用默认值实例化, 因此你可以仅设置要更改的属性。</span><span class="sxs-lookup"><span data-stu-id="b98fe-105">The HostConfig object will be instantiated with defaults, so you can set just the properties you want to change.</span></span>

<span data-ttu-id="b98fe-106">例如：</span><span class="sxs-lookup"><span data-stu-id="b98fe-106">Example:</span></span>

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

> <span data-ttu-id="b98fe-107">或者, 可以从 JSON 字符串加载 HostConfig。</span><span class="sxs-lookup"><span data-stu-id="b98fe-107">Alternatively, you can load the HostConfig from a JSON string.</span></span>

<span data-ttu-id="b98fe-108">例如：</span><span class="sxs-lookup"><span data-stu-id="b98fe-108">Example:</span></span>

```csharp
var hostConfig = AdaptiveHostConfig.FromJsonString(jsonString); 

renderer.HostConfig = hostConfig;
```

<span data-ttu-id="b98fe-109">在将其传递给 UWPRenderer 时, 将设置默认的 HostConfig, 以便将其用于每个呈现的卡。</span><span class="sxs-lookup"><span data-stu-id="b98fe-109">When you pass it in to the UWPRenderer you are setting the default HostConfig to use for every card you render.</span></span>