---
title: 主机配置-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 554b32d9d088e82fb0fd48bec4b94340e843abeb
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76146121"
---
# <a name="host-config---android"></a><span data-ttu-id="d2816-102">主机配置-Android</span><span class="sxs-lookup"><span data-stu-id="d2816-102">Host config - Android</span></span>

<span data-ttu-id="d2816-103">若要自定义呈现器，请提供 HostConfig 对象的实例。</span><span class="sxs-lookup"><span data-stu-id="d2816-103">To customize the renderer you provide an instance of the HostConfig object.</span></span> <span data-ttu-id="d2816-104">（有关完整的说明，请参阅[主机配置架构](../../../../rendering-cards/host-config.md)。）</span><span class="sxs-lookup"><span data-stu-id="d2816-104">(See [Host Config Schema](../../../../rendering-cards/host-config.md) for the full description.)</span></span>

<span data-ttu-id="d2816-105">若要通过字符串创建 ```HostConfig``` 对象，请使用如下所示的 ```DeserializeFromString``` 方法：</span><span class="sxs-lookup"><span data-stu-id="d2816-105">To create a ```HostConfig``` object from a string, use the ```DeserializeFromString``` method like this:</span></span>

```csharp
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;
// ...

HostConfig Config = HostConfig.DeserializeFromString(configJson);
```