---
title: 文本功能
author: matthidinger
ms.author: mahiding
ms.date: 11/09/2017
ms.topic: article
ms.openlocfilehash: ac8ec0c48e06377ebd17f1b31abe463c48809fe3
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553609"
---
# <a name="text-features"></a>文本功能

`TextBlock` 提供了一些格式设置和本地化文本的高级的功能。

## <a name="markdown"></a>Markdown
若要支持内联标记，自适应卡支持**子集**的 Markdown 语法。

_支持_

| 文本样式      | Markdown |
|-----------------|-----|
| **加粗**        | ```**Bold**``` |
| _斜体_        | ```_Italic_``` |
| 项目符号列表     | ```- Item 1\r- Item 2\r- Item 3``` | 
| 编号列表   | ```1. Green\r2. Orange\r3. Blue``` |
| 超链接      | ```[Title](url)``` |

_不支持_

* 标头
* 表
* 映像
* 不在上表中的任何内容

### <a name="markdown-example"></a>Markdown 示例

下面有效负载中将会呈现如下：

![markdown 屏幕快照](media/text-features/markdown.png)

```json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

## <a name="datetime-formatting-and-localization"></a>日期/时间格式设置和本地化

有时不会知道收到卡，因此，自适应卡提供的用户的时区`DATE()`和`TIME()`的格式设置函数，以自动对目标设备上的时间进行本地化。

### <a name="datetime-example"></a>日期/时间的示例

```json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "Your package will arrive on {{DATE(2017-02-14T06:00:00Z, SHORT)}} at {{TIME(2017-02-14T06:00:00Z)}}",
            "wrap": true
        }
    ]
}
```

上述卡将显示： 

> **在上午 6:00，你的包将到达 2017 年 2 月 14，日，星期二**

### <a name="datetime-function-rules"></a>日期/时间函数规则

有一些规则来正确地解释每个平台上的日期/时间函数。 如果原始字符串将显示给用户，并且没有人愿意，则不符合规则。

1. **区分大小写**（必须为全部大写）
1. **不能含有空格**之间`{{`， `}}`，或括号
1. **严格[RFC 3389](https://tools.ietf.org/html/rfc3339)格式**（请参阅下面的示例）
1. **必须为**有效的日期和时间

### <a name="valid-formats"></a>有效格式

* `2017-02-14T06:08:00Z`
* `2017-02-14T06:08:00-07:00`
* `2017-02-14T06:08:00+07:00`

### <a name="date-formatting-param"></a>日期格式设置参数

对于日期，可以指定可选参数来设置输出格式。


|       格式        |            示例            |
|---------------------|-------------------------------|
| `COMPACT` （默认值） |          "2/13/2017"          |
|       `SHORT`       |     "星期一，2 月 13日，2017"     |
|       `LONG`        | "星期一，2017 年 2 月 13 日" |

