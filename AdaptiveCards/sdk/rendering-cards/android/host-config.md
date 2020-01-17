---
title: 主机配置-Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: 091e2093c380affc8c895d069a2f52061b991d2f
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145487"
---
# <a name="host-config---android"></a><span data-ttu-id="5ea10-102">主机配置-Android</span><span class="sxs-lookup"><span data-stu-id="5ea10-102">Host config - Android</span></span>

<span data-ttu-id="5ea10-103">若要自定义呈现器，请提供 HostConfig 对象的实例。</span><span class="sxs-lookup"><span data-stu-id="5ea10-103">To customize the renderer you provide an instance of the HostConfig object.</span></span> <span data-ttu-id="5ea10-104">（有关完整的说明，请参阅[主机配置架构](../../../rendering-cards/host-config.md)。）</span><span class="sxs-lookup"><span data-stu-id="5ea10-104">(See [Host Config Schema](../../../rendering-cards/host-config.md) for the full description.)</span></span>

<span data-ttu-id="5ea10-105">若要通过字符串创建 HostConfig 对象，请使用 DeserializeFromString 方法</span><span class="sxs-lookup"><span data-stu-id="5ea10-105">To Create a HostConfig object from a string, use the DeserializeFromString method</span></span>

```java
HostConfig hostConfig = HostConfig.DeserializeFromString(hostConfigText);
```