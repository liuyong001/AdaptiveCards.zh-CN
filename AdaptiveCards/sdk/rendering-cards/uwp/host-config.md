---
title: 托管配置-UWP SDK
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
# <a name="host-config---uwp"></a><span data-ttu-id="7799c-102">主机配置-UWP</span><span class="sxs-lookup"><span data-stu-id="7799c-102">Host config - UWP</span></span>

<span data-ttu-id="7799c-103">若要自定义呈现器您提供 HostConfig 对象的实例。</span><span class="sxs-lookup"><span data-stu-id="7799c-103">To customize the renderer you provide an instance of the HostConfig object.</span></span> <span data-ttu-id="7799c-104">(请参阅[主机配置架构](../../../rendering-cards/host-config.md)有关完整说明。)</span><span class="sxs-lookup"><span data-stu-id="7799c-104">(See [Host Config Schema](../../../rendering-cards/host-config.md) for the full description.)</span></span>

> <span data-ttu-id="7799c-105">因此，你可以设置你想要更改的属性，则将使用默认值，实例化 HostConfig 对象。</span><span class="sxs-lookup"><span data-stu-id="7799c-105">The HostConfig object will be instantiated with defaults, so you can set just the properties you want to change.</span></span>

<span data-ttu-id="7799c-106">例如：</span><span class="sxs-lookup"><span data-stu-id="7799c-106">Example:</span></span>

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

> <span data-ttu-id="7799c-107">或者，您可以从 JSON 字符串加载 HostConfig。</span><span class="sxs-lookup"><span data-stu-id="7799c-107">Alternatively, you can load the HostConfig from a JSON string.</span></span>

<span data-ttu-id="7799c-108">例如：</span><span class="sxs-lookup"><span data-stu-id="7799c-108">Example:</span></span>

```csharp
var hostConfig = AdaptiveHostConfig.FromJsonString(jsonString); 

renderer.HostConfig = hostConfig;
```

<span data-ttu-id="7799c-109">将其传递到 UWPRenderer 时需要设置默认 HostConfig 要用于您呈现每个卡。</span><span class="sxs-lookup"><span data-stu-id="7799c-109">When you pass it in to the UWPRenderer you are setting the default HostConfig to use for every card you render.</span></span>