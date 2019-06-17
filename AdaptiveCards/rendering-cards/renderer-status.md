---
title: 呈现器状态
author: matthidinger
ms.author: mahiding
ms.date: 10/12/2018
ms.topic: article
ms.openlocfilehash: bffa49012a8ebe686fc033f98b2438d2e9e959cc
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67138030"
---
# <a name="renderer-status"></a>呈现器状态
下表显示每个呈现器中，基于其公共的已发布版本的当前状态。

### <a name="parsing"></a>分析

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|返回验证失败 | ✅ | ✅ | ✅ | ✅ | ✅ |
|分析未知的属性 | ✅ | ✅ | ✅ | ✅ | ✅ |

### <a name="card-rendering"></a>卡呈现

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|检查受支持的版本 | ✅ | ✅ | ✅ | ✅ | ✅  |
|呈现完整架构 | ✅ | ✅ | ✅ | ✅ | ✅ |
|呈现操作栏 | ✅ | ✅ | ✅ | ✅ | ✅ |
|忽略未知的元素 | ✅ | ✅ | ✅ | ✅ | ✅ |
|主机配置支持 | ✅ | ✅ | ✅ | ✅ | ✅ |
|本机平台样式设置 | ✅ | ✅ | ✅ | ✅ | ✅ |

### <a name="element-rendering"></a>元素呈现

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|间距和分隔符 | ✅ | ✅ | ✅ | ✅ | ✅ |
|[TextBlock 日期/时间格式](../authoring-cards/text-features.md#datetime-formatting-and-localization) | ✅ | ✅ | ✅ | ✅ | ✅ |
|[TextBlock Markdown 支持](../authoring-cards/text-features.md#markdown) | ✅* | ✅ | ✅ | ✅ | ✅ |
|输入所有内容完全支持 | ✅ | ✅ | ✅ | ✅ | ✅ |

\* 为了最小化库的大小并让使用方应用程序使用其首选的 Markdown 处理器，HTML 呈现器不包括内置的 Markdown 支持。 如果已加载，HTML 呈现器将但是自动使用 Markdown It。

### <a name="extensibility"></a>扩展性

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|重写元素呈现器 | ✅ | ✅ | ✅ | ✅ | ✅ |
|添加新元素的呈现器 | ✅ | ✅ | ✅ | ✅ | ✅ |
|删除元素呈现器 | ✅ | ✅ | ✅ | ✅ | ✅ |
|[重写/添加/删除操作呈现器](https://github.com/Microsoft/AdaptiveCards/issues/1671) | ✅ | ✅ | ❌ | ✅ | ✅ |

### <a name="actions"></a>操作

| 功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
| Action.OpenUrl 支持 | ✅ | ✅ | ✅ | ✅ | ✅  |
| Action.ShowCard 支持  | ✅ | ✅ | ✅ | ✅ | ✅ |
| Action.Submit 支持  | ✅ | ✅ | ✅ | ✅ | ✅  |
| selectAction 支持 | ✅ | ✅ | ✅ | ✅ | ✅ |

### <a name="events"></a>Events

|       功能        | HTML | .NET | UWP | iOS | Android | 
|----------------------------|------|------|-----|-----|---------|
| 元素可见性更改 |  ✅   |  ❌   |  ❌  |  ❌  | ❌ |

