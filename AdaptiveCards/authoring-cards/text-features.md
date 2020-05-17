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
# <a name="text-features"></a><span data-ttu-id="ad138-102">文本功能</span><span class="sxs-lookup"><span data-stu-id="ad138-102">Text features</span></span>

<span data-ttu-id="ad138-103">`TextBlock` 提供一些用于文本格式设置和本地化的高级功能。</span><span class="sxs-lookup"><span data-stu-id="ad138-103">`TextBlock` offers some advanced features for formatting and localizing the text.</span></span>

## <a name="markdown"></a><span data-ttu-id="ad138-104">Markdown</span><span class="sxs-lookup"><span data-stu-id="ad138-104">Markdown</span></span>
<span data-ttu-id="ad138-105">为了支持内联标记，自适应卡片支持**部分** Markdown 语法。</span><span class="sxs-lookup"><span data-stu-id="ad138-105">To support inline markup, Adaptive Cards support a **subset** of Markdown syntax.</span></span>

<span data-ttu-id="ad138-106">支持 </span><span class="sxs-lookup"><span data-stu-id="ad138-106">_Supported_</span></span>

| <span data-ttu-id="ad138-107">文本样式</span><span class="sxs-lookup"><span data-stu-id="ad138-107">Text Style</span></span>      | <span data-ttu-id="ad138-108">Markdown</span><span class="sxs-lookup"><span data-stu-id="ad138-108">Markdown</span></span> |
|-----------------|-----|
| <span data-ttu-id="ad138-109">**粗体**</span><span class="sxs-lookup"><span data-stu-id="ad138-109">**Bold**</span></span>        | ```**Bold**``` |
| <span data-ttu-id="ad138-110">_斜体_</span><span class="sxs-lookup"><span data-stu-id="ad138-110">_Italic_</span></span>        | ```_Italic_``` |
| <span data-ttu-id="ad138-111">项目符号列表</span><span class="sxs-lookup"><span data-stu-id="ad138-111">Bullet list</span></span>     | ```- Item 1\r- Item 2\r- Item 3``` | 
| <span data-ttu-id="ad138-112">编号列表</span><span class="sxs-lookup"><span data-stu-id="ad138-112">Numbered list</span></span>   | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="ad138-113">超链接</span><span class="sxs-lookup"><span data-stu-id="ad138-113">Hyperlinks</span></span>      | ```[Title](url)``` |

<span data-ttu-id="ad138-114">不支持 </span><span class="sxs-lookup"><span data-stu-id="ad138-114">_Not supported_</span></span>

* <span data-ttu-id="ad138-115">标头</span><span class="sxs-lookup"><span data-stu-id="ad138-115">Headers</span></span>
* <span data-ttu-id="ad138-116">表</span><span class="sxs-lookup"><span data-stu-id="ad138-116">Tables</span></span>
* <span data-ttu-id="ad138-117">映像</span><span class="sxs-lookup"><span data-stu-id="ad138-117">Images</span></span>
* <span data-ttu-id="ad138-118">不在上表中的任何内容</span><span class="sxs-lookup"><span data-stu-id="ad138-118">Anything not in the table above</span></span>

### <a name="markdown-example"></a><span data-ttu-id="ad138-119">Markdown 示例</span><span class="sxs-lookup"><span data-stu-id="ad138-119">Markdown Example</span></span>

<span data-ttu-id="ad138-120">下面的有效负载会呈现如下所示的内容：</span><span class="sxs-lookup"><span data-stu-id="ad138-120">The below payload would render something like this:</span></span>

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

## <a name="datetime-formatting-and-localization"></a><span data-ttu-id="ad138-122">日期/时间格式设置和本地化</span><span class="sxs-lookup"><span data-stu-id="ad138-122">Date/Time formatting and localization</span></span>

<span data-ttu-id="ad138-123">有时候，你不知道接收卡片的用户的时区，因此可以使用自适应卡片提供的 `DATE()` 和 `TIME()` 格式设置函数，在目标设备上自动完成时间的本地化。</span><span class="sxs-lookup"><span data-stu-id="ad138-123">Sometimes you won't know the timezone of the user receiving the card, so Adaptive Cards offers `DATE()` and `TIME()` formatting functions to automatically localize the time on the target device.</span></span>

### <a name="datetime-example"></a><span data-ttu-id="ad138-124">日期/时间示例</span><span class="sxs-lookup"><span data-stu-id="ad138-124">Date/Time Example</span></span>

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

<span data-ttu-id="ad138-125">上面的卡会显示：</span><span class="sxs-lookup"><span data-stu-id="ad138-125">The above card will display:</span></span> 

> <span data-ttu-id="ad138-126">**Your package will arrive on Tue, Feb 14th, 2017 at 6:00 AM**</span><span class="sxs-lookup"><span data-stu-id="ad138-126">**Your package will arrive on Tue, Feb 14th, 2017 at 6:00 AM**</span></span>

### <a name="datetime-function-rules"></a><span data-ttu-id="ad138-127">日期/时间函数规则</span><span class="sxs-lookup"><span data-stu-id="ad138-127">Date/Time function rules</span></span>

<span data-ttu-id="ad138-128">为了在每个平台上恰当地解释日期/时间函数，必须应用一些规则。</span><span class="sxs-lookup"><span data-stu-id="ad138-128">There are some rules to properly interpret the the date/time functions on every platform.</span></span> <span data-ttu-id="ad138-129">如果规则得不到满足，则会向用户显示原始字符串，这不是大家希望的。</span><span class="sxs-lookup"><span data-stu-id="ad138-129">If the rules aren't met then the raw string will be displayed to the user, and no one wants that.</span></span>

1. <span data-ttu-id="ad138-130">**区分大小写**（必须全部大写）</span><span class="sxs-lookup"><span data-stu-id="ad138-130">**CASE SENSITIVE** (must be all caps)</span></span>
1. <span data-ttu-id="ad138-131">`{{`、`}}` 或括号之间**不能有空格**</span><span class="sxs-lookup"><span data-stu-id="ad138-131">**NO SPACES** between the `{{`, `}}`, or parentheses</span></span>
1. <span data-ttu-id="ad138-132">**严格的 [RFC 3389](https://tools.ietf.org/html/rfc3339) 格式设置**（参见下面的示例）</span><span class="sxs-lookup"><span data-stu-id="ad138-132">**STRICT [RFC 3389](https://tools.ietf.org/html/rfc3339) FORMATTING** (See examples below)</span></span>
1. <span data-ttu-id="ad138-133">**必须是**有效的日期和时间</span><span class="sxs-lookup"><span data-stu-id="ad138-133">**MUST BE** a valid date and time</span></span>

### <a name="valid-formats"></a><span data-ttu-id="ad138-134">有效格式</span><span class="sxs-lookup"><span data-stu-id="ad138-134">Valid formats</span></span>

* `2017-02-14T06:08:00Z`
* `2017-02-14T06:08:00-07:00`
* `2017-02-14T06:08:00+07:00`

### <a name="date-formatting-param"></a><span data-ttu-id="ad138-135">日期格式设置参数</span><span class="sxs-lookup"><span data-stu-id="ad138-135">Date formatting param</span></span>

<span data-ttu-id="ad138-136">对于日期，可以指定一个可选参数来设置输出格式。</span><span class="sxs-lookup"><span data-stu-id="ad138-136">For dates, an optional param may be specified to format the output.</span></span>


|       <span data-ttu-id="ad138-137">格式</span><span class="sxs-lookup"><span data-stu-id="ad138-137">Format</span></span>        |            <span data-ttu-id="ad138-138">示例</span><span class="sxs-lookup"><span data-stu-id="ad138-138">Example</span></span>            |
|---------------------|-------------------------------|
| <span data-ttu-id="ad138-139">`COMPACT`（默认）</span><span class="sxs-lookup"><span data-stu-id="ad138-139">`COMPACT` (Default)</span></span> |          <span data-ttu-id="ad138-140">“2/13/2017”</span><span class="sxs-lookup"><span data-stu-id="ad138-140">"2/13/2017"</span></span>          |
|       `SHORT`       |     <span data-ttu-id="ad138-141">“Mon, Feb 13th, 2017”</span><span class="sxs-lookup"><span data-stu-id="ad138-141">"Mon, Feb 13th, 2017"</span></span>     |
|       `LONG`        | <span data-ttu-id="ad138-142">“Monday, February 13th, 2017”</span><span class="sxs-lookup"><span data-stu-id="ad138-142">"Monday, February 13th, 2017"</span></span> |

