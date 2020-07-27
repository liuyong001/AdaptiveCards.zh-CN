---
title: 文本功能
author: matthidinger
ms.author: mahiding
ms.date: 06/18/2020
ms.topic: article
ms.openlocfilehash: d685007cb24e7fa8ef15b53ee5547708fba6b490
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417508"
---
# <a name="text-features"></a><span data-ttu-id="68357-102">文本功能</span><span class="sxs-lookup"><span data-stu-id="68357-102">Text features</span></span>

<span data-ttu-id="68357-103">[TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 提供用于文本格式设置和本地化的高级功能。</span><span class="sxs-lookup"><span data-stu-id="68357-103">[TextBlock](https://adaptivecards.io/explorer/TextBlock.html) offers advanced features for formatting and localizing the text.</span></span>

## <a name="markdown-commonmark-subset"></a><span data-ttu-id="68357-104">Markdown（Commonmark 子集）</span><span class="sxs-lookup"><span data-stu-id="68357-104">Markdown (Commonmark subset)</span></span>

<span data-ttu-id="68357-105">为了支持内联标记，自适应卡片支持部分 [Commonmark](https://commonmark.org/help/) Markdown 语法。</span><span class="sxs-lookup"><span data-stu-id="68357-105">To support inline markup, Adaptive Cards support a **subset** of the [Commonmark](https://commonmark.org/help/) Markdown syntax.</span></span>

> [!NOTE]
>
> <span data-ttu-id="68357-106">[RichTextBlock](https://adaptivecards.io/explorer/RichTextBlock.html) 不支持 Markdown，但它直接在 [TextRun](https://adaptivecards.io/explorer/TextRun.html) 中提供了大量文本配置选项</span><span class="sxs-lookup"><span data-stu-id="68357-106">[RichTextBlock](https://adaptivecards.io/explorer/RichTextBlock.html) does not support markdown, but offers a wide array of text configuration options directly within the the [TextRun](https://adaptivecards.io/explorer/TextRun.html)</span></span>

<span data-ttu-id="68357-107">支持</span><span class="sxs-lookup"><span data-stu-id="68357-107">_Supported_</span></span>

| <span data-ttu-id="68357-108">文本样式</span><span class="sxs-lookup"><span data-stu-id="68357-108">Text Style</span></span>      | <span data-ttu-id="68357-109">Markdown</span><span class="sxs-lookup"><span data-stu-id="68357-109">Markdown</span></span> |
|-----------------|-----|
| <span data-ttu-id="68357-110">**粗体**</span><span class="sxs-lookup"><span data-stu-id="68357-110">**Bold**</span></span>        | ```**Bold**``` |
| <span data-ttu-id="68357-111">_斜体_</span><span class="sxs-lookup"><span data-stu-id="68357-111">_Italic_</span></span>        | ```_Italic_``` |
| <span data-ttu-id="68357-112">项目符号列表</span><span class="sxs-lookup"><span data-stu-id="68357-112">Bullet list</span></span>     | ```- Item 1\r- Item 2\r- Item 3``` | 
| <span data-ttu-id="68357-113">编号列表</span><span class="sxs-lookup"><span data-stu-id="68357-113">Numbered list</span></span>   | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="68357-114">超链接</span><span class="sxs-lookup"><span data-stu-id="68357-114">Hyperlinks</span></span>      | ```[Title](url)``` |

<span data-ttu-id="68357-115">不支持</span><span class="sxs-lookup"><span data-stu-id="68357-115">_Not supported_</span></span>

* <span data-ttu-id="68357-116">标头</span><span class="sxs-lookup"><span data-stu-id="68357-116">Headers</span></span>
* <span data-ttu-id="68357-117">表</span><span class="sxs-lookup"><span data-stu-id="68357-117">Tables</span></span>
* <span data-ttu-id="68357-118">映像</span><span class="sxs-lookup"><span data-stu-id="68357-118">Images</span></span>
* <span data-ttu-id="68357-119">不在上表中的任何内容</span><span class="sxs-lookup"><span data-stu-id="68357-119">Anything not in the table above</span></span>

### <a name="markdown-example"></a><span data-ttu-id="68357-120">Markdown 示例</span><span class="sxs-lookup"><span data-stu-id="68357-120">Markdown Example</span></span>

<span data-ttu-id="68357-121">下面的有效负载会呈现如下所示的内容：</span><span class="sxs-lookup"><span data-stu-id="68357-121">The below payload would render something like this:</span></span>

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
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

## <a name="datetime-formatting-and-localization"></a><span data-ttu-id="68357-123">日期/时间格式设置和本地化</span><span class="sxs-lookup"><span data-stu-id="68357-123">Date/Time formatting and localization</span></span>

<span data-ttu-id="68357-124">有时候，你不知道接收卡片的用户的时区，因此可以使用自适应卡片提供的 `DATE()` 和 `TIME()` 格式设置函数，在目标设备上自动完成时间的本地化。</span><span class="sxs-lookup"><span data-stu-id="68357-124">Sometimes you won't know the timezone of the user receiving the card, so Adaptive Cards offers `DATE()` and `TIME()` formatting functions to automatically localize the time on the target device.</span></span>

### <a name="datetime-example"></a><span data-ttu-id="68357-125">日期/时间示例</span><span class="sxs-lookup"><span data-stu-id="68357-125">Date/Time Example</span></span>

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

<span data-ttu-id="68357-126">上面的卡会显示：</span><span class="sxs-lookup"><span data-stu-id="68357-126">The above card will display:</span></span> 

> <span data-ttu-id="68357-127">**Your package will arrive on Tue, Feb 14th, 2017 at 6:00 AM**</span><span class="sxs-lookup"><span data-stu-id="68357-127">**Your package will arrive on Tue, Feb 14th, 2017 at 6:00 AM**</span></span>

### <a name="datetime-function-rules"></a><span data-ttu-id="68357-128">日期/时间函数规则</span><span class="sxs-lookup"><span data-stu-id="68357-128">Date/Time function rules</span></span>

<span data-ttu-id="68357-129">为了在每个平台上恰当地解释日期/时间函数，必须应用一些规则。</span><span class="sxs-lookup"><span data-stu-id="68357-129">There are some rules to properly interpret the the date/time functions on every platform.</span></span> <span data-ttu-id="68357-130">如果规则得不到满足，则会向用户显示原始字符串，这不是大家希望的。</span><span class="sxs-lookup"><span data-stu-id="68357-130">If the rules aren't met then the raw string will be displayed to the user, and no one wants that.</span></span>

1. <span data-ttu-id="68357-131">**区分大小写**（必须全部大写）</span><span class="sxs-lookup"><span data-stu-id="68357-131">**CASE SENSITIVE** (must be all caps)</span></span>
1. <span data-ttu-id="68357-132">`{{`、`}}` 或括号之间**不能有空格**</span><span class="sxs-lookup"><span data-stu-id="68357-132">**NO SPACES** between the `{{`, `}}`, or parentheses</span></span>
1. <span data-ttu-id="68357-133">**严格的 [RFC 3389](https://tools.ietf.org/html/rfc3339) 格式设置**（参见下面的示例）</span><span class="sxs-lookup"><span data-stu-id="68357-133">**STRICT [RFC 3389](https://tools.ietf.org/html/rfc3339) FORMATTING** (See examples below)</span></span>
1. <span data-ttu-id="68357-134">**必须是**有效的日期和时间</span><span class="sxs-lookup"><span data-stu-id="68357-134">**MUST BE** a valid date and time</span></span>

### <a name="valid-formats"></a><span data-ttu-id="68357-135">有效格式</span><span class="sxs-lookup"><span data-stu-id="68357-135">Valid formats</span></span>

* `2017-02-14T06:08:00Z`
* `2017-02-14T06:08:00-07:00`
* `2017-02-14T06:08:00+07:00`

### <a name="date-formatting-param"></a><span data-ttu-id="68357-136">日期格式设置参数</span><span class="sxs-lookup"><span data-stu-id="68357-136">Date formatting param</span></span>

<span data-ttu-id="68357-137">对于日期，可以指定一个可选参数来设置输出格式。</span><span class="sxs-lookup"><span data-stu-id="68357-137">For dates, an optional param may be specified to format the output.</span></span>


|       <span data-ttu-id="68357-138">格式</span><span class="sxs-lookup"><span data-stu-id="68357-138">Format</span></span>        |            <span data-ttu-id="68357-139">示例</span><span class="sxs-lookup"><span data-stu-id="68357-139">Example</span></span>            |
|---------------------|-------------------------------|
| <span data-ttu-id="68357-140">`COMPACT`（默认）</span><span class="sxs-lookup"><span data-stu-id="68357-140">`COMPACT` (Default)</span></span> |          <span data-ttu-id="68357-141">“2/13/2017”</span><span class="sxs-lookup"><span data-stu-id="68357-141">"2/13/2017"</span></span>          |
|       `SHORT`       |     <span data-ttu-id="68357-142">“Mon, Feb 13th, 2017”</span><span class="sxs-lookup"><span data-stu-id="68357-142">"Mon, Feb 13th, 2017"</span></span>     |
|       `LONG`        | <span data-ttu-id="68357-143">“Monday, February 13th, 2017”</span><span class="sxs-lookup"><span data-stu-id="68357-143">"Monday, February 13th, 2017"</span></span> |

