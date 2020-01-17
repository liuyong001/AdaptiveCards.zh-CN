---
title: RenderedAdaptiveCard 类-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 608b28638ce6ed0a218cfc8dbbe73f22de1ab8cb
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145991"
---
# <a name="renderedadaptivecard"></a>RenderedAdaptiveCard

```csharp
public class RenderedAdaptiveCard : Java.Lang.Object
```

**命名空间**

```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.Renderer
```

### <a name="summary"></a>摘要

| 属性 | |
| ---- | --- |
| AdaptiveCard | 呈现的自适应卡的逻辑表示形式。 |
| 输入 | 输入元素的字典和用户添加的信息。 |
| “查看” | 呈现过程的视觉效果。 |
| 警告 | 呈现过程中生成的警告的列表。 |

&nbsp;

| 公共方法 | |
| --- | ---- |
| ```void``` | [```AddWarning AdaptiveCards.Rendering.Xamarin.Android.Renderer.AdaptiveWarning warning)```](#addwarning) |

## <a name="public-methods"></a>公共方法

---

### <a id="addwarning"></a>AddWarning
<p style='text-align:right'>在版本0.1 中添加</p>

```csharp
public void AddWarning (AdaptiveWarning warning)

```

向警告列表添加警告。

| 参数 | |
| --- | --- |
| 警告 | ```AdaptiveCards.Rendering.Xamarin.Android.Renderer.AdaptiveWarning``` |
