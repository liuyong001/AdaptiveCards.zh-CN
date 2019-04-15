---
title: 主机配置的 iOS SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: b788ecc5c2371d2575e0165296365238535dd7c5
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553699"
---
# <a name="host-config---ios"></a>主机配置-iOS

可以通过 HostConfig 可以生成 JSON 字符串来配置主机

```objective-c
ACOParseResult *hostconfigParseResult = [ACOHostConfig FromJson:self.hostconfig];
```

可以实例化默认 HostConfig

```objective-c
ACOHostConfig *defaultConfig = [[ACHostConfig alloc] init];
```

## <a name="render-a-card-using-host-config"></a>呈现使用主机配置的卡

Rederer 采用自适应卡和主机配置。HostConfig 可为零，而如果 nil，将使用默认值。

```objective-c
ACRRenderResult *renderResult;
renderResult = [ACRRenderer render:cardParseResult.card
                            config:hostconfigParseResult.config
                   widthConstraint:300.0];
```