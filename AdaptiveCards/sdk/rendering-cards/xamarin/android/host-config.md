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
# <a name="host-config---android"></a>主机配置-Android

若要自定义呈现器，请提供 HostConfig 对象的实例。 （有关完整的说明，请参阅[主机配置架构](../../../../rendering-cards/host-config.md)。）

若要通过字符串创建 ```HostConfig``` 对象，请使用如下所示的 ```DeserializeFromString``` 方法：

```csharp
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;
// ...

HostConfig Config = HostConfig.DeserializeFromString(configJson);
```