---
title: 自适应卡片模板语言
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: 2c583f774451e60f825cd8fd2c38f2ea34c2f8de
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145397"
---
# <a name="adaptive-cards-template-language"></a><span data-ttu-id="77137-102">自适应卡片模板语言</span><span class="sxs-lookup"><span data-stu-id="77137-102">Adaptive Cards Template Language</span></span>

<span data-ttu-id="77137-103">模板化可以将自适应卡片中的**数据**与**布局**分开。</span><span class="sxs-lookup"><span data-stu-id="77137-103">Templating enables the separation of **data** from **layout** in your Adaptive Card.</span></span> <span data-ttu-id="77137-104">模板语言是用于创作模板的语法。</span><span class="sxs-lookup"><span data-stu-id="77137-104">The template langauge is the syntax used to author a template.</span></span> 

> <span data-ttu-id="77137-105">有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)</span><span class="sxs-lookup"><span data-stu-id="77137-105">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="77137-106">这些功能为**预览版，可能会更改**。</span><span class="sxs-lookup"><span data-stu-id="77137-106">These features are **in preview and subject to change**.</span></span> <span data-ttu-id="77137-107">我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。</span><span class="sxs-lookup"><span data-stu-id="77137-107">Your feedback is not only welcome, but  critical to ensure we deliver the features **you** need.</span></span>

<span data-ttu-id="77137-108">创作模板时，可以使用 `AdaptiveCard` 有效负载以内联方式指定数据，也可以在运行时使用[模板化 SDK](sdk.md) 来这样做。</span><span class="sxs-lookup"><span data-stu-id="77137-108">When authoring a template you can specify the data inline with the `AdaptiveCard` payload, or at runtime using the [Templating SDKs](sdk.md).</span></span>

## <a name="specify-data-within-the-card"></a><span data-ttu-id="77137-109">指定卡片中的数据</span><span class="sxs-lookup"><span data-stu-id="77137-109">Specify data within the card</span></span>

<span data-ttu-id="77137-110">若要直接在卡片有效负载中提供数据，只需将 `$data` 属性添加到 `AdaptiveCard` 即可（见下）。</span><span class="sxs-lookup"><span data-stu-id="77137-110">To provide data directly within the card payload, simply add a `$data` attribute to your `AdaptiveCard` (seen below).</span></span>

## <a name="binding-to-the-data"></a><span data-ttu-id="77137-111">绑定到数据</span><span class="sxs-lookup"><span data-stu-id="77137-111">Binding to the data</span></span>

<span data-ttu-id="77137-112">可以绑定到卡片的 `body` 或 `actions` 中的数据。</span><span class="sxs-lookup"><span data-stu-id="77137-112">You can bind to the data within the `body` or `actions` of the card.</span></span>

* <span data-ttu-id="77137-113">绑定语法以 `{` 开头，以 `}` 结尾。</span><span class="sxs-lookup"><span data-stu-id="77137-113">Binding syntax starts with `{` and ends with `}`.</span></span> <span data-ttu-id="77137-114">例如 `{myProperty}`</span><span class="sxs-lookup"><span data-stu-id="77137-114">E.g., `{myProperty}`</span></span>
* <span data-ttu-id="77137-115">用于访问子对象的点表示法</span><span class="sxs-lookup"><span data-stu-id="77137-115">Dot-notation to access sub-objects</span></span>
* <span data-ttu-id="77137-116">索引器语法，用于按键或数组中的项检索属性</span><span class="sxs-lookup"><span data-stu-id="77137-116">Indexer syntax to retrieve properties by key or items in an array</span></span>
* <span data-ttu-id="77137-117">针对深层次结构的常规 null 处理</span><span class="sxs-lookup"><span data-stu-id="77137-117">Graceful null handling for deep hierarchies</span></span>
* <span data-ttu-id="77137-118">即将发布的转义符语法文档 </span><span class="sxs-lookup"><span data-stu-id="77137-118">*Escape syntax documentation to come soon*</span></span>

```json
{
    "type": "AdaptiveCard",
    "$data": {
        "employee": {
            "name": "Matt",
            "manager": { "name": "Thomas" },
            "peers": [{
                "name": "Andrew" 
            }, { 
                "name": "Lei"
            }, { 
                "name": "Mary Anne"
            }, { 
                "name": "Adam"
            }]
        }
    },
    "body": [
        {
            "type": "TextBlock",
            "text": "Hi {employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: {employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: {employee.peers[0].name}, {employee.peers[1].name}, {employee.peers[2].name}"
        }
    ]
}
```

## <a name="separating-the-template-from-the-data"></a><span data-ttu-id="77137-119">将模板与数据分离</span><span class="sxs-lookup"><span data-stu-id="77137-119">Separating the template from the data</span></span>

<span data-ttu-id="77137-120">另外，还可以创建一个可反复使用的不含数据的卡片“模板”（可能性更高）。</span><span class="sxs-lookup"><span data-stu-id="77137-120">Alternatively (and more likely), you will create a re-usable card "template" without including the data.</span></span> <span data-ttu-id="77137-121">此模板可以存储为文件并添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="77137-121">This template could be stored as a file and added to source control.</span></span>

<span data-ttu-id="77137-122">**EmployeeCardTemplate.json**</span><span class="sxs-lookup"><span data-stu-id="77137-122">**EmployeeCardTemplate.json**</span></span>

```json
{
    "type": "AdaptivCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Hi {employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: {employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: {employee.peers[0].name}, {employee.peers[1].name}, {employee.peers[2].name}"
        }
    ]
}
```

<span data-ttu-id="77137-123">然后，将其加载并使用 [模板化 SDK](sdk.md) 在运行时提供数据。</span><span class="sxs-lookup"><span data-stu-id="77137-123">Then load it up and provide the data at runtime using the [Templating SDKs](sdk.md).</span></span>

<span data-ttu-id="77137-124">**JavaScript 示例**</span><span class="sxs-lookup"><span data-stu-id="77137-124">**JavaScript example**</span></span>

<span data-ttu-id="77137-125">使用 [adaptivecards-templating](https://npmjs.com/package/adaptivecards-templating) 包。</span><span class="sxs-lookup"><span data-stu-id="77137-125">Using the [adaptivecards-templating](https://npmjs.com/package/adaptivecards-templating) package.</span></span>

```js
var template = new ACData.Template({ 
    // EmployeeCardTemplate goes here
});

// Specify data at runtime
var dataContext = new ACData.EvaluationContext();
dataContext.$root = {
    "employee": {
        "name": "Matt",
        "manager": { "name": "Thomas" },
        "peers": [{
            "name": "Andrew" 
        }, { 
            "name": "Lei"
        }, { 
            "name": "Mary Anne"
        }, { 
            "name": "Adam"
        }]
    }
};

var card = template.expand(dataContext);
// Now you have an AdaptiveCard ready to render!
```

## <a name="designer-support"></a><span data-ttu-id="77137-126">设计器支持</span><span class="sxs-lookup"><span data-stu-id="77137-126">Designer Support</span></span>

<span data-ttu-id="77137-127">自适应卡片设计器已更新为支持模板化。</span><span class="sxs-lookup"><span data-stu-id="77137-127">The Adaptive Card Designer has been updated to support templating.</span></span> 

> <span data-ttu-id="77137-128">试用网址： **[https://adaptivecards.io/designer](https://adaptivecards.io/designer)**</span><span class="sxs-lookup"><span data-stu-id="77137-128">Try it out at: **[https://adaptivecards.io/designer](https://adaptivecards.io/designer)**</span></span>

<span data-ttu-id="77137-129">[![图像](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](https://adaptivecards.io/designer)</span><span class="sxs-lookup"><span data-stu-id="77137-129">[![image](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](https://adaptivecards.io/designer)</span></span>

* <span data-ttu-id="77137-130">**示例数据编辑器** - 在此处指定示例数据，以便在“预览模式”下查看数据绑定卡片。</span><span class="sxs-lookup"><span data-stu-id="77137-130">**Sample Data Editor** - Specify sample data here to view the data-bound card when in "Preview Mode."</span></span> <span data-ttu-id="77137-131">此窗格中有一个小按钮，用于填充现有示例数据中的“数据结构”。</span><span class="sxs-lookup"><span data-stu-id="77137-131">There is a small button in this pane to populate the Data Structure from the existing sample data.</span></span>
* <span data-ttu-id="77137-132">**数据结构** - 这是示例数据的结构。</span><span class="sxs-lookup"><span data-stu-id="77137-132">**Data Structure** - This is the structure of your sample data.</span></span> <span data-ttu-id="77137-133">可以将字段拖到设计图面上，以便创建一个绑定，将内容绑定到这些字段</span><span class="sxs-lookup"><span data-stu-id="77137-133">Fields can be dragged onto the design surface to create a binding to them</span></span> 
* <span data-ttu-id="77137-134">**预览模式** - 按工具栏按钮即可在编辑体验和示例数据预览体验之间切换</span><span class="sxs-lookup"><span data-stu-id="77137-134">**Preview Mode** - Press the toolbar button to toggle between the edit-experience and the sample-data-preview experience</span></span>
* <span data-ttu-id="77137-135">**打开示例** - 单击此按钮即可打开各种示例有效负载</span><span class="sxs-lookup"><span data-stu-id="77137-135">**Open Sample** - click this button to open various sample payloads</span></span>

## <a name="advanced-binding"></a><span data-ttu-id="77137-136">高级绑定</span><span class="sxs-lookup"><span data-stu-id="77137-136">Advanced binding</span></span>

### <a name="binding-scopes"></a><span data-ttu-id="77137-137">绑定范围</span><span class="sxs-lookup"><span data-stu-id="77137-137">Binding scopes</span></span>

<span data-ttu-id="77137-138">可以通过几个保留关键字来访问各种绑定范围。</span><span class="sxs-lookup"><span data-stu-id="77137-138">There are a few reserved keywords to access various binding scopes.</span></span> 

<span data-ttu-id="77137-139"> 注意：在预览版中，并非所有这些都得到了实现。</span><span class="sxs-lookup"><span data-stu-id="77137-139">*Note:* not all of these are implemented in the preview.</span></span>

```json
{
    "{<property>}": "Implicitly binds to `$data.<property>`",
    "$data": "The current data object",
    "$root": "The root data object. Useful when iterating to escape to parent object",
    "$index": "The current index when iterating",
    "$host": "Access properties of the host *(not working yet)*"
}
```

### <a name="assigning-a-data-context-to-elements"></a><span data-ttu-id="77137-140">将数据上下文分配给元素</span><span class="sxs-lookup"><span data-stu-id="77137-140">Assigning a data context to elements</span></span>

<span data-ttu-id="77137-141">若要为任意元素分配“数据上下文”，请将 `$data` 属性添加到该元素。</span><span class="sxs-lookup"><span data-stu-id="77137-141">To assign a "data context" to any element add a `$data` attribute to the element.</span></span>

```json
{
    "type": "Container",
    "$data": "{mySubObject}",
    "items": [
        {
            "type": "TextBlock",
            "text": "This TextBlock is now scoped directly to 'mySubObject': {mySubObjectProperty}"
        },
        {
            "type": "TextBlock",
            "text": "To break-out and access the root data, use: {$root}"
        }
    ]
}
```

## <a name="repeating-items-in-an-array"></a><span data-ttu-id="77137-142">数组中的重复项</span><span class="sxs-lookup"><span data-stu-id="77137-142">Repeating items in an array</span></span>

<span data-ttu-id="77137-143">此部分有点“晦涩”。</span><span class="sxs-lookup"><span data-stu-id="77137-143">This part is a bit of "dark magic".</span></span> <span data-ttu-id="77137-144">欢迎反馈。</span><span class="sxs-lookup"><span data-stu-id="77137-144">Feedback welcome.</span></span>

* <span data-ttu-id="77137-145">如果将某个自适应卡片元素的 `$data` 属性绑定到**数组**，则**会针对数组中的每个项重复元素本身。**</span><span class="sxs-lookup"><span data-stu-id="77137-145">If an Adaptive Card element's `$data` property is bound to an **array**, then the **element itself will be repeated for each item in the array.**</span></span> 
* <span data-ttu-id="77137-146">在属性值中使用的任何绑定表达式 (`{myProperty}`) 的作用域都将是数组中的**单个项**。</span><span class="sxs-lookup"><span data-stu-id="77137-146">Any binding expressions (`{myProperty}`) used in property values will be scoped to the **individual item** within the array.</span></span>
* <span data-ttu-id="77137-147">如果绑定到字符串数组，请使用 `{$data}` 访问单个字符串元素。</span><span class="sxs-lookup"><span data-stu-id="77137-147">If binding to an array of strings, use `{$data}` to access the individual string element.</span></span> <span data-ttu-id="77137-148">例如 `"text": "{$data}"`</span><span class="sxs-lookup"><span data-stu-id="77137-148">E.g., `"text": "{$data}"`</span></span>

<span data-ttu-id="77137-149">举例来说，下面的 `TextBlock` 会重复 3 次，因为其 `$data` 是数组。</span><span class="sxs-lookup"><span data-stu-id="77137-149">For example, the `TextBlock` below will be repeated 3 times since it's `$data` is an array.</span></span> <span data-ttu-id="77137-150">请注意 `text` 属性如何绑定到数组内单个对象的 `name` 属性。</span><span class="sxs-lookup"><span data-stu-id="77137-150">Notice how the `text` property is bound to the `name` property of an individual object within the array.</span></span> 

```json
{
    "type": "Container",
    "items": [
        {
            "type": "TextBlock",
            "$data": [
                { "name": "Matt" }, 
                { "name": "David" }, 
                { "name": "Thomas" }
            ],
            "text": "{name}"
        }
    ]
}
```

<span data-ttu-id="77137-151">**结果：**</span><span class="sxs-lookup"><span data-stu-id="77137-151">**Resulting in:**</span></span>

```json
{
    "type": "Container",
    "items": [ 
        {
            "type": "TextBlock",
            "text": "Matt"
        },
        {
            "type": "TextBlock",
            "text": "David"
        }
        {
            "type": "TextBlock",
            "text": "Thomas"
        }
    ]
}
```

## <a name="functions"></a><span data-ttu-id="77137-152">功能</span><span class="sxs-lookup"><span data-stu-id="77137-152">Functions</span></span>

<span data-ttu-id="77137-153">如果没有帮助程序函数，则任何模板化语言都不是完整的。</span><span class="sxs-lookup"><span data-stu-id="77137-153">No templating language is complete without some helper functions.</span></span> <span data-ttu-id="77137-154">我们会提供一组可在每个 SDK 上使用的标准函数。</span><span class="sxs-lookup"><span data-stu-id="77137-154">We will provide a standard set of functions that work on every SDK.</span></span> 

<span data-ttu-id="77137-155">此处的语法仍未确定，因此请稍后回来查看。不过，下面是我们所计划内容的开头：</span><span class="sxs-lookup"><span data-stu-id="77137-155">The syntax here is still up in the air so please check back soon, but here's a start of what we're planning:</span></span>

### <a name="string-functions"></a><span data-ttu-id="77137-156">字符串函数</span><span class="sxs-lookup"><span data-stu-id="77137-156">String functions</span></span>

* <span data-ttu-id="77137-157">substr</span><span class="sxs-lookup"><span data-stu-id="77137-157">substr</span></span>
* <span data-ttu-id="77137-158">indexOf（尚不能使用） </span><span class="sxs-lookup"><span data-stu-id="77137-158">indexOf *(not working yet)*</span></span>
* <span data-ttu-id="77137-159">toUpper（尚不能使用） </span><span class="sxs-lookup"><span data-stu-id="77137-159">toUpper *(not working yet)*</span></span>
* <span data-ttu-id="77137-160">toLower（尚不能使用） </span><span class="sxs-lookup"><span data-stu-id="77137-160">toLower *(not working yet)*</span></span>

### <a name="number-functions"></a><span data-ttu-id="77137-161">数值函数</span><span class="sxs-lookup"><span data-stu-id="77137-161">Number functions</span></span>

* <span data-ttu-id="77137-162">格式化（货币、小数等）（尚不能使用） </span><span class="sxs-lookup"><span data-stu-id="77137-162">Formatting (currency, decimal, etc) *(not working yet)*</span></span>

### <a name="date-functions"></a><span data-ttu-id="77137-163">日期函数</span><span class="sxs-lookup"><span data-stu-id="77137-163">Date functions</span></span>

* <span data-ttu-id="77137-164">分析众所周知的日期字符串格式（尚不能使用） </span><span class="sxs-lookup"><span data-stu-id="77137-164">Parsing well-known date string formats *(not working yet)*</span></span>
* <span data-ttu-id="77137-165">针对众所周知的日期/时间表示方式进行格式设置（尚不能使用） </span><span class="sxs-lookup"><span data-stu-id="77137-165">Formatting for well-known date/time representations *(not working yet)*</span></span>

### <a name="conditional-functions"></a><span data-ttu-id="77137-166">条件函数</span><span class="sxs-lookup"><span data-stu-id="77137-166">Conditional functions</span></span>

* <span data-ttu-id="77137-167">if(*表达式*, *trueValue*, *falseValue*)</span><span class="sxs-lookup"><span data-stu-id="77137-167">if(*expression*, *trueValue*, *falseValue*)</span></span>

<span data-ttu-id="77137-168">**`if` 示例**</span><span class="sxs-lookup"><span data-stu-id="77137-168">**`if` example**</span></span>

```json
{
    "type": "TextBlock",
    "color": "{if(priceChange >= 0, 'good', 'attention')}"
}
```

### <a name="data-manipulation"></a><span data-ttu-id="77137-169">数据操作</span><span class="sxs-lookup"><span data-stu-id="77137-169">Data manipulation</span></span>

* <span data-ttu-id="77137-170">JSON.parse - 分析 JSON 字符串的功能</span><span class="sxs-lookup"><span data-stu-id="77137-170">JSON.parse - ability to parse a JSON string</span></span> 

<span data-ttu-id="77137-171">**`JSON.parse` 示例**</span><span class="sxs-lookup"><span data-stu-id="77137-171">**`JSON.parse` example**</span></span>

<span data-ttu-id="77137-172">这是 Azure DevOps 响应，其中的 `message` 属性是一个 JSON 序列化字符串。</span><span class="sxs-lookup"><span data-stu-id="77137-172">This is an Azure DevOps response where the `message` property is a JSON-serialized string.</span></span> <span data-ttu-id="77137-173">若要访问字符串中的值，需要在模板中使用 `JSON.parse` 函数。</span><span class="sxs-lookup"><span data-stu-id="77137-173">In order to access values within the string, we need to use the `JSON.parse` function in our template.</span></span>

<span data-ttu-id="77137-174">**数据**</span><span class="sxs-lookup"><span data-stu-id="77137-174">**Data**</span></span> 

```json
{
    "id": "1291525457129548",
    "status": 4,
    "author": "Matt Hidinger",
    "message": "{\"type\":\"Deployment\",\"buildId\":\"9542982\",\"releaseId\":\"129\",\"buildNumber\":\"20180504.3\",\"releaseName\":\"Release-104\",\"repoProvider\":\"GitHub\"}",
    "start_time": "2018-05-04T18:05:33.3087147Z",
    "end_time": "2018-05-04T18:05:33.3087147Z"
}
```

<span data-ttu-id="77137-175">**用法**</span><span class="sxs-lookup"><span data-stu-id="77137-175">**Usage**</span></span>

```json
{
    "type": "TextBlock",
    "text": "{JSON.parse(message).releaseName}"
}
```

<span data-ttu-id="77137-176">**结果**</span><span class="sxs-lookup"><span data-stu-id="77137-176">**Resulting In**</span></span>

```json
{
    "type": "TextBlock",
    "text": "Release-104"
}
```

### <a name="custom-functions"></a><span data-ttu-id="77137-177">自定义函数</span><span class="sxs-lookup"><span data-stu-id="77137-177">Custom functions</span></span>

<span data-ttu-id="77137-178">我们希望确保主机可以添加自定义函数。这意味着，如果某个函数不受支持，我们需要提供对回退支持的可靠支持。</span><span class="sxs-lookup"><span data-stu-id="77137-178">We want to make sure Hosts can add custom functions, which means we need robust support for fallback support if a function isn't supported.</span></span> <span data-ttu-id="77137-179">我们仍在对此进行评估。</span><span class="sxs-lookup"><span data-stu-id="77137-179">We are still evaluating this.</span></span>

## <a name="conditional-layout"></a><span data-ttu-id="77137-180">条件布局</span><span class="sxs-lookup"><span data-stu-id="77137-180">Conditional layout</span></span>

<span data-ttu-id="77137-181">若要在满足条件时删除整个元素，请使用 `$when` 属性。</span><span class="sxs-lookup"><span data-stu-id="77137-181">To drop an entire element if a condition is met, use the `$when` property.</span></span> <span data-ttu-id="77137-182">如果 `$when` 的计算结果为 `false`，则此元素不会显示给用户。</span><span class="sxs-lookup"><span data-stu-id="77137-182">If `$when` evaluates to `false` the element will not appear to the user.</span></span>

```json
{
    "type": "AdaptiveCard",
    "$data": {
        "price": "35"
    },
    "body": [
        {
            "type": "TextBlock",
            "$when": "{price > 30}",
            "text": "This thing is pricy!",
            "color": "attention",
        },
         {
            "type": "TextBlock",
            "$when": "{price <= 30}",
            "text": "Dang, this thing is cheap!",
            "color": "good"
        }
    ]
}
```

### <a name="composing-templates"></a><span data-ttu-id="77137-183">组合模板</span><span class="sxs-lookup"><span data-stu-id="77137-183">Composing templates</span></span>

<span data-ttu-id="77137-184">目前不支持将模板“部件”组合到一起。</span><span class="sxs-lookup"><span data-stu-id="77137-184">Currently there is no support for composing template "parts" together.</span></span> <span data-ttu-id="77137-185">但是，我们会探索相关选项，希望不久就能为大家提供更多此方面的内容。</span><span class="sxs-lookup"><span data-stu-id="77137-185">But we are exploring options and hope to share more soon.</span></span> <span data-ttu-id="77137-186">欢迎你在此提供自己的想法！</span><span class="sxs-lookup"><span data-stu-id="77137-186">Any thoughts here welcome!</span></span>


## <a name="examples"></a><span data-ttu-id="77137-187">示例</span><span class="sxs-lookup"><span data-stu-id="77137-187">Examples</span></span>

<span data-ttu-id="77137-188">请浏览更新的[“示例”页](https://adaptivecards.io/samples)，其中包含各种新的模板化卡片。</span><span class="sxs-lookup"><span data-stu-id="77137-188">Browse the updated [Samples page](https://adaptivecards.io/samples) to explore all sorts of new templated cards.</span></span>
