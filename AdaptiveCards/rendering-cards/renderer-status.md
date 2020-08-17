---
title: 呈现器状态
author: matthidinger
ms.author: mahiding
ms.date: 10/12/2018
ms.topic: article
ms.openlocfilehash: 1042fd862990a79c77110ebdf5d804eadcc606ea
ms.sourcegitcommit: 19c08b1370305fb2965de0140c5e632356e78513
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879146"
---
# <a name="renderer-status"></a>呈现器状态
下面的表显示了每个呈现器的当前状态，具体取决于其公开发布的版本。

### <a name="parsing"></a>分析

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|返回验证失败 | ✅ | ✅ | ✅ | ✅ | ✅ |
|分析未知属性 | ✅ | ✅ | ✅ | ✅ | ✅ |

### <a name="card-rendering"></a>卡片呈现

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|查看支持的版本 | ✅ | ✅ | ✅ | ✅ | ✅  |
|呈现完整架构 | ✅ | ✅ | ✅ | ✅ | ✅ |
|呈现操作栏 | ✅ | ✅ | ✅ | ✅ | ✅ |
|忽略未知元素 | ✅ | ✅ | ✅ | ✅ | ✅ |
|Host Config 支持 | ✅ | ✅ | ✅ | ✅ | ✅ |
|本机平台样式设置 | ✅ | ✅ | ✅ | ✅ | ❌ |

### <a name="element-rendering"></a>元素呈现

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|间距和分隔符 | ✅ | ✅ | ✅ | ✅ | ✅ |
|[TextBlock 日期/时间格式设置](../authoring-cards/text-features.md#datetime-formatting-and-localization) | ✅ | ✅ | ✅ | ✅ | ✅ |
|[TextBlock Markdown 支持](../authoring-cards/text-features.md#markdown-commonmark-subset) | ✅* | ✅ | ✅ | ✅ | ✅ |
|输入验证和标签 | ❌ | ✅ | ✅ | ✅ | ✅ |


\* HTML 呈现器不包括内置的 Markdown 支持，目的是尽量减少库的大小，让资源耗用型应用程序使用其首选的 Markdown 处理器。 不过，HTML 呈现器会在 Markdown 已加载的情况下自动使用它。

### <a name="extensibility"></a>扩展性

|功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
|重写元素呈现器 | ✅ | ✅ | ✅ | ✅ | ✅ |
|添加新的元素呈现器 | ✅ | ✅ | ✅ | ✅ | ✅ |
|删除元素呈现器 | ✅ | ✅ | ✅ | ✅ | ✅ |
|[重写/添加/删除操作呈现器](https://github.com/Microsoft/AdaptiveCards/issues/1671) | ✅ | ✅ | ❌ | ✅ | ✅ |

### <a name="actions"></a>操作

| 功能 | HTML | .NET | UWP | iOS | Android |
|--- | --- | --- | --- | --- | --- | --- |
| Action.OpenUrl 支持 | ✅ | ✅ | ✅ | ✅ | ✅  |
| Action.ShowCard 支持  | ✅ | ✅ | ✅ | ✅ | ✅ |
| Action.Submit 支持  | ✅ | ✅ | ✅ | ✅ | ✅  |
| selectAction 支持 | ✅ | ✅ | ✅ | ✅ | ✅ |

### <a name="events"></a>事件

|       功能        | HTML | .NET | UWP | iOS | Android | 
|----------------------------|------|------|-----|-----|---------|
| 元素可见性已更改 |  ✅   |  ❌   |  ❌  |  ❌  | ❌ |

