---
title: 本机样式-iOS SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: f9ed839a19ac778381fa36361ad37e95b7ab5e08
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76727468"
---
# <a name="native-styling---ios"></a>本机样式-iOS

使用 XIB 进行精细的样式设置。

存在以下 Xib

| XIB | 사용 패턴 |
|---|---|
| ACRButton. xib | 按钮 |
| ACRCellForCompactMode. xib   | ChoiceSet compact 模式|
| ACRDatePicker. xib | DatePicker 的输入日期 |
| ACRDateTextField. xib  | 输入的文本字段。日期 |
| ACRInputTableView. xib   | 输入的容器 |
| ACRLabelView. xib  | TextBlock |
| ACRPickerView. xib | ChoiceSet |
| ACRQuickActionMultilineView. xib  | Multilines 的快速操作 |
| ACRQuickActionView. xib | 快速操作 |
| ACRTextField. xib | 입력 |

可以通过 XCode IB 编辑 XIB。
将 Xib 编辑为规范后。
从终端
```
ibtool --compile name.nib name.xib 
```

例如，若要对按钮进行样式
```
ibtool --compile ACRButton.nib ACRButton.xib 
```

然后，可以在 AdaptiveCards 替换生成的笔尖文件
