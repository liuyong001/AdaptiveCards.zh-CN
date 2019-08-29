---
title: 主机配置-Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: c44cf609fd52423a1ca17988a875c6dc48550007
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553339"
---
# <a name="host-config---android"></a><span data-ttu-id="c6531-102">主机配置-Android</span><span class="sxs-lookup"><span data-stu-id="c6531-102">Host config - Android</span></span>

<span data-ttu-id="c6531-103">若要自定义呈现器, 请提供 HostConfig 对象的实例。</span><span class="sxs-lookup"><span data-stu-id="c6531-103">To customize the renderer you provide an instance of the HostConfig object.</span></span> <span data-ttu-id="c6531-104">(有关完整的说明, 请参阅[主机配置架构](../../../rendering-cards/host-config.md)。)</span><span class="sxs-lookup"><span data-stu-id="c6531-104">(See [Host Config Schema](../../../rendering-cards/host-config.md) for the full description.)</span></span>

<span data-ttu-id="c6531-105">若要通过字符串创建 HostConfig 对象, 请使用 DeserializeFromString 方法</span><span class="sxs-lookup"><span data-stu-id="c6531-105">To Create a HostConfig object from a string, use the DeserializeFromString method</span></span>

```java
HostConfig hostConfig = HostConfig.DeserializeFromString(hostConfigText);
```