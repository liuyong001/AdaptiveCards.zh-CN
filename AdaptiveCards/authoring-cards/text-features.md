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
# <a name="text-features"></a><span data-ttu-id="1232d-102">文本功能</span><span class="sxs-lookup"><span data-stu-id="1232d-102">Text features</span></span>

<span data-ttu-id="1232d-103">`TextBlock` 提供了一些格式设置和本地化文本的高级的功能。</span><span class="sxs-lookup"><span data-stu-id="1232d-103">`TextBlock` offers some advanced features for formatting and localizing the text.</span></span>

## <a name="markdown"></a><span data-ttu-id="1232d-104">Markdown</span><span class="sxs-lookup"><span data-stu-id="1232d-104">Markdown</span></span>
<span data-ttu-id="1232d-105">若要支持内联标记，自适应卡支持**子集**的 Markdown 语法。</span><span class="sxs-lookup"><span data-stu-id="1232d-105">To support inline markup, Adaptive Cards support a **subset** of Markdown syntax.</span></span>

<span data-ttu-id="1232d-106">_支持_</span><span class="sxs-lookup"><span data-stu-id="1232d-106">_Supported_</span></span>

| <span data-ttu-id="1232d-107">文本样式</span><span class="sxs-lookup"><span data-stu-id="1232d-107">Text Style</span></span>      | <span data-ttu-id="1232d-108">Markdown</span><span class="sxs-lookup"><span data-stu-id="1232d-108">Markdown</span></span> |
|-----------------|-----|
| <span data-ttu-id="1232d-109">**加粗**</span><span class="sxs-lookup"><span data-stu-id="1232d-109">**Bold**</span></span>        | ```**Bold**``` |
| <span data-ttu-id="1232d-110">_斜体_</span><span class="sxs-lookup"><span data-stu-id="1232d-110">_Italic_</span></span>        | ```_Italic_``` |
| <span data-ttu-id="1232d-111">项目符号列表</span><span class="sxs-lookup"><span data-stu-id="1232d-111">Bullet list</span></span>     | ```- Item 1\r- Item 2\r- Item 3``` | 
| <span data-ttu-id="1232d-112">编号列表</span><span class="sxs-lookup"><span data-stu-id="1232d-112">Numbered list</span></span>   | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="1232d-113">超链接</span><span class="sxs-lookup"><span data-stu-id="1232d-113">Hyperlinks</span></span>      | ```[Title](url)``` |

<span data-ttu-id="1232d-114">_不支持_</span><span class="sxs-lookup"><span data-stu-id="1232d-114">_Not supported_</span></span>

* <span data-ttu-id="1232d-115">标头</span><span class="sxs-lookup"><span data-stu-id="1232d-115">Headers</span></span>
* <span data-ttu-id="1232d-116">表</span><span class="sxs-lookup"><span data-stu-id="1232d-116">Tables</span></span>
* <span data-ttu-id="1232d-117">映像</span><span class="sxs-lookup"><span data-stu-id="1232d-117">Images</span></span>
* <span data-ttu-id="1232d-118">不在上表中的任何内容</span><span class="sxs-lookup"><span data-stu-id="1232d-118">Anything not in the table above</span></span>

### <a name="markdown-example"></a><span data-ttu-id="1232d-119">Markdown 示例</span><span class="sxs-lookup"><span data-stu-id="1232d-119">Markdown Example</span></span>

<span data-ttu-id="1232d-120">下面有效负载中将会呈现如下：</span><span class="sxs-lookup"><span data-stu-id="1232d-120">The below payload would render something like this:</span></span>

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

## <a name="datetime-formatting-and-localization"></a><span data-ttu-id="1232d-122">日期/时间格式设置和本地化</span><span class="sxs-lookup"><span data-stu-id="1232d-122">Date/Time formatting and localization</span></span>

<span data-ttu-id="1232d-123">有时不会知道收到卡，因此，自适应卡提供的用户的时区`DATE()`和`TIME()`的格式设置函数，以自动对目标设备上的时间进行本地化。</span><span class="sxs-lookup"><span data-stu-id="1232d-123">Sometimes you won't know the timezone of the user receiving the card, so Adaptive Cards offers `DATE()` and `TIME()` formatting functions to automatically localize the time on the target device.</span></span>

### <a name="datetime-example"></a><span data-ttu-id="1232d-124">日期/时间的示例</span><span class="sxs-lookup"><span data-stu-id="1232d-124">Date/Time Example</span></span>

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

<span data-ttu-id="1232d-125">上述卡将显示：</span><span class="sxs-lookup"><span data-stu-id="1232d-125">The above card will display:</span></span> 

> <span data-ttu-id="1232d-126">**在上午 6:00，你的包将到达 2017 年 2 月 14，日，星期二**</span><span class="sxs-lookup"><span data-stu-id="1232d-126">**Your package will arrive on Tue, Feb 14th, 2017 at 6:00 AM**</span></span>

### <a name="datetime-function-rules"></a><span data-ttu-id="1232d-127">日期/时间函数规则</span><span class="sxs-lookup"><span data-stu-id="1232d-127">Date/Time function rules</span></span>

<span data-ttu-id="1232d-128">有一些规则来正确地解释每个平台上的日期/时间函数。</span><span class="sxs-lookup"><span data-stu-id="1232d-128">There are some rules to properly interpret the the date/time functions on every platform.</span></span> <span data-ttu-id="1232d-129">如果原始字符串将显示给用户，并且没有人愿意，则不符合规则。</span><span class="sxs-lookup"><span data-stu-id="1232d-129">If the rules aren't met then the raw string will be displayed to the user, and no one wants that.</span></span>

1. <span data-ttu-id="1232d-130">**区分大小写**（必须为全部大写）</span><span class="sxs-lookup"><span data-stu-id="1232d-130">**CASE SENSITIVE** (must be all caps)</span></span>
1. <span data-ttu-id="1232d-131">**不能含有空格**之间`{{`， `}}`，或括号</span><span class="sxs-lookup"><span data-stu-id="1232d-131">**NO SPACES** between the `{{`, `}}`, or parentheses</span></span>
1. <span data-ttu-id="1232d-132">**严格[RFC 3389](https://tools.ietf.org/html/rfc3339)格式**（请参阅下面的示例）</span><span class="sxs-lookup"><span data-stu-id="1232d-132">**STRICT [RFC 3389](https://tools.ietf.org/html/rfc3339) FORMATTING** (See examples below)</span></span>
1. <span data-ttu-id="1232d-133">**必须为**有效的日期和时间</span><span class="sxs-lookup"><span data-stu-id="1232d-133">**MUST BE** a valid date and time</span></span>

### <a name="valid-formats"></a><span data-ttu-id="1232d-134">有效格式</span><span class="sxs-lookup"><span data-stu-id="1232d-134">Valid formats</span></span>

* `2017-02-14T06:08:00Z`
* `2017-02-14T06:08:00-07:00`
* `2017-02-14T06:08:00+07:00`

### <a name="date-formatting-param"></a><span data-ttu-id="1232d-135">日期格式设置参数</span><span class="sxs-lookup"><span data-stu-id="1232d-135">Date formatting param</span></span>

<span data-ttu-id="1232d-136">对于日期，可以指定可选参数来设置输出格式。</span><span class="sxs-lookup"><span data-stu-id="1232d-136">For dates, an optional param may be specified to format the output.</span></span>


|       <span data-ttu-id="1232d-137">格式</span><span class="sxs-lookup"><span data-stu-id="1232d-137">Format</span></span>        |            <span data-ttu-id="1232d-138">示例</span><span class="sxs-lookup"><span data-stu-id="1232d-138">Example</span></span>            |
|---------------------|-------------------------------|
| <span data-ttu-id="1232d-139">`COMPACT` （默认值）</span><span class="sxs-lookup"><span data-stu-id="1232d-139">`COMPACT` (Default)</span></span> |          <span data-ttu-id="1232d-140">"2/13/2017"</span><span class="sxs-lookup"><span data-stu-id="1232d-140">"2/13/2017"</span></span>          |
|       `SHORT`       |     <span data-ttu-id="1232d-141">"星期一，2 月 13日，2017"</span><span class="sxs-lookup"><span data-stu-id="1232d-141">"Mon, Feb 13th, 2017"</span></span>     |
|       `LONG`        | <span data-ttu-id="1232d-142">"星期一，2017 年 2 月 13 日"</span><span class="sxs-lookup"><span data-stu-id="1232d-142">"Monday, February 13th, 2017"</span></span> |

