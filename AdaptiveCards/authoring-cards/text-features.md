---
title: 文本功能
author: matthidinger
ms.author: mahiding
ms.date: 11/09/2017
ms.topic: article
ms.openlocfilehash: f7ea40b80df4d976c0a8a86b15254018fdf2fac6
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "77454870"
---
# <a name="text-features"></a>文本功能

`TextBlock` 提供一些用于文本格式设置和本地化的高级功能。

## <a name="markdown"></a>Markdown
为了支持内联标记，自适应卡片支持**部分** Markdown 语法。

支持 

| 文本样式      | Markdown |
|-----------------|-----|
| **粗体**        | ```**Bold**``` |
| _斜体_        | ```_Italic_``` |
| 项目符号列表     | ```- Item 1\r- Item 2\r- Item 3``` | 
| 编号列表   | ```1. Green\r2. Orange\r3. Blue``` |
| 超链接      | ```[Title](url)``` |

不支持 

* 标头
* 表
* 映像
* 不在上表中的任何内容

### <a name="markdown-example"></a>Markdown 示例

下面的有效负载会呈现如下所示的内容：

![markdown 屏幕截图](media/text-features/markdown.png)

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

有时候，你不知道接收卡片的用户的时区，因此可以使用自适应卡片提供的 `DATE()` 和 `TIME()` 格式设置函数，在目标设备上自动完成时间的本地化。

### <a name="datetime-example"></a>日期/时间示例

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

上面的卡会显示： 

> **Your package will arrive on Tue, Feb 14th, 2017 at 6:00 AM**

### <a name="datetime-function-rules"></a>日期/时间函数规则

为了在每个平台上恰当地解释日期/时间函数，必须应用一些规则。 如果规则得不到满足，则会向用户显示原始字符串，这不是大家希望的。

1. **区分大小写**（必须全部大写）
1. **、** 或括号之间`{{`不能有空格`}}`
1. **严格的 [RFC 3389](https://tools.ietf.org/html/rfc3339) 格式设置**（参见下面的示例）
1. **必须是**有效的日期和时间

### <a name="valid-formats"></a>有效格式

* `2017-02-14T06:08:00Z`
* `2017-02-14T06:08:00-07:00`
* `2017-02-14T06:08:00+07:00`

### <a name="date-formatting-param"></a>日期格式设置参数

对于日期，可以指定一个可选参数来设置输出格式。


|       格式        |            示例            |
|---------------------|-------------------------------|
| `COMPACT`（默认） |          “2/13/2017”          |
|       `SHORT`       |     “Mon, Feb 13th, 2017”     |
|       `LONG`        | “Monday, February 13th, 2017” |

