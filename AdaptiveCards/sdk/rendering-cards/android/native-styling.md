---
title: 本机样式设置 - Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: 8d5dd9bbf17800c55aae1d416b7e6d80ac697b25
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417603"
---
# <a name="native-styling---android"></a>本机样式设置 - Android

Android 呈现器不支持本机样式设置。v1.2 引入了对某些属性的样式设置的支持：

## <a name="action-sentiment"></a>操作情绪

操作情绪包括在 **v1.2** 中。虽然该版本不像其他版本那样支持许多样式，但可以对带有“破坏性”情绪或“正面”情绪的操作进行样式设置，只需实现一个有效的样式并将以下行添加到项目的 styles.xml 中即可****

```styles.xml
 <item name="adaptiveActionDestructive">@style/adaptiveActionDestructive</item>
 <item name="adaptiveActionPositive">@style/adaptiveActionPositive</item>
```

## <a name="inline-action"></a>内联操作

可以通过带内联操作的文本输入为要呈现的操作进行样式设置。 这样可以将操作的样式设置为按钮 (adaptiveInlineAction) 或图像 (adaptiveInlineActionImage)

```styles.xml
 <item name="adaptiveInlineAction">@style/adaptiveInlineAction</item>
 <item name="adaptiveInlineActionImage">@style/adaptiveInlineActionImage</item>
```

> [!IMPORTANT]
> 必须保留所有项目名称，如此处所示，因为呈现器会查找这些具体的名称

## <a name="actionshowcard"></a>Action.ShowCard

ShowCard 可以通过将样式添加到 styles.xml 中的主题来进行样式化。

```styles.xml
 <item name="adaptiveShowCardAction">@style/adaptiveShowCardAction</item>
```