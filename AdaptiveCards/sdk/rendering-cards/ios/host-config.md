---
title: 主机配置-iOS SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: fa420c0a6e9e9b7e5713b6cc528de39335f0b56c
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76727483"
---
# <a name="host-config---ios"></a>主机配置-iOS

可以通过 JSON 字符串生成的 HostConfig 配置主机

```objective-c
ACOParseResult *hostconfigParseResult = [ACOHostConfig FromJson:self.hostconfig];
```

可以实例化默认 HostConfig

```objective-c
ACOHostConfig *defaultConfig = [[ACHostConfig alloc] init];
```

## <a name="render-a-card-using-host-config"></a>使用主机配置呈现卡

Rederer 采用自适应卡和主机配置。HostConfig 可以为 nil，如果为 nil，则使用默认值。

```objective-c
ACRRenderResult *renderResult;
renderResult = [ACRRenderer render:cardParseResult.card
                            config:hostconfigParseResult.config
                   widthConstraint:300.0];
```

## <a name="customization"></a>自定义

有三种方法可自定义自适应卡呈现：

1. 主机配置
2. XIB
3. 自定义元素呈现
