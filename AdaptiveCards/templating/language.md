---
title: 自适应卡模板语言
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: 993618ed94eaea1a004c7893a5a3927c0d818cd6
ms.sourcegitcommit: a16f53ba10a8607deacde5c8cc78927cac58657c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68878894"
---
# <a name="adaptive-cards-template-language"></a><span data-ttu-id="9c6e6-102">自适应卡模板语言</span><span class="sxs-lookup"><span data-stu-id="9c6e6-102">Adaptive Cards Template Language</span></span>

<span data-ttu-id="9c6e6-103">模板化可将**数据**与自适应卡中的**布局**分离。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-103">Templating enables the separation of **data** from **layout** in your Adaptive Card.</span></span> <span data-ttu-id="9c6e6-104">模板语言是用于创作模板的语法。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-104">The template langauge is the syntax used to author a template.</span></span> 

> <span data-ttu-id="9c6e6-105">有关[自适应卡模板的概述](index.md), 请阅读此概述</span><span class="sxs-lookup"><span data-stu-id="9c6e6-105">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="9c6e6-106">这些功能**处于预览阶段, 可能会有所更改**。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-106">These features are **in preview and subject to change**.</span></span> <span data-ttu-id="9c6e6-107">你的反馈不仅是欢迎的, 而且确保我们能够提供**所**需的功能至关重要。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-107">Your feedback is not only welcome, but  critical to ensure we deliver the features **you** need.</span></span>

<span data-ttu-id="9c6e6-108">创作模板时, 可以使用`AdaptiveCard`有效负载或在运行时使用[模板化 sdk](sdk.md)来指定数据。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-108">When authoring a template you can specify the data inline with the `AdaptiveCard` payload, or at runtime using the [Templating SDKs](sdk.md).</span></span>

## <a name="specify-data-within-the-card"></a><span data-ttu-id="9c6e6-109">指定卡片内的数据</span><span class="sxs-lookup"><span data-stu-id="9c6e6-109">Specify data within the card</span></span>

<span data-ttu-id="9c6e6-110">若要直接在卡有效负载中提供数据, 只`$data`需将属性`AdaptiveCard`添加到 (见下文)。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-110">To provide data directly within the card payload, simply add a `$data` attribute to your `AdaptiveCard` (seen below).</span></span>

## <a name="binding-to-the-data"></a><span data-ttu-id="9c6e6-111">绑定到数据</span><span class="sxs-lookup"><span data-stu-id="9c6e6-111">Binding to the data</span></span>

<span data-ttu-id="9c6e6-112">您可以绑定到卡`body`或`actions`卡中的数据。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-112">You can bind to the data within the `body` or `actions` of the card.</span></span>

* <span data-ttu-id="9c6e6-113">绑定语法以开头`{` , 以`}`结尾。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-113">Binding syntax starts with `{` and ends with `}`.</span></span> <span data-ttu-id="9c6e6-114">例如,`{myProperty}`</span><span class="sxs-lookup"><span data-stu-id="9c6e6-114">E.g., `{myProperty}`</span></span>
* <span data-ttu-id="9c6e6-115">用点表示法访问子对象</span><span class="sxs-lookup"><span data-stu-id="9c6e6-115">Dot-notation to access sub-objects</span></span>
* <span data-ttu-id="9c6e6-116">索引器语法, 用于按键或数组中的项检索属性</span><span class="sxs-lookup"><span data-stu-id="9c6e6-116">Indexer syntax to retrieve properties by key or items in an array</span></span>
* <span data-ttu-id="9c6e6-117">对于深层层次结构的宽容 null 处理</span><span class="sxs-lookup"><span data-stu-id="9c6e6-117">Graceful null handling for deep hierarchies</span></span>
* <span data-ttu-id="9c6e6-118">*即将推出语法文档*</span><span class="sxs-lookup"><span data-stu-id="9c6e6-118">*Escape syntax documentation to come soon*</span></span>

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

## <a name="separating-the-template-from-the-data"></a><span data-ttu-id="9c6e6-119">将模板与数据分离</span><span class="sxs-lookup"><span data-stu-id="9c6e6-119">Separating the template from the data</span></span>

<span data-ttu-id="9c6e6-120">另外, 您还可以创建一个重新使用的卡 "模板", 而不包含数据。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-120">Alternatively (and more likely), you will create a re-usable card "template" without including the data.</span></span> <span data-ttu-id="9c6e6-121">此模板可以存储为文件并添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-121">This template could be stored as a file and added to source control.</span></span>

<span data-ttu-id="9c6e6-122">**EmployeeCardTemplate**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-122">**EmployeeCardTemplate.json**</span></span>

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

<span data-ttu-id="9c6e6-123">然后, 使用[模板化 sdk](sdk.md)加载它并在运行时提供数据。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-123">Then load it up and provide the data at runtime using the [Templating SDKs](sdk.md).</span></span>

<span data-ttu-id="9c6e6-124">**JavaScript 示例**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-124">**JavaScript example**</span></span>

<span data-ttu-id="9c6e6-125">使用[adaptivecards 模板](https://npmjs.com/package/adaptivecards-templating)包。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-125">Using the [adaptivecards-templating](https://npmjs.com/package/adaptivecards-templating) package.</span></span>

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

## <a name="designer-support"></a><span data-ttu-id="9c6e6-126">设计器支持</span><span class="sxs-lookup"><span data-stu-id="9c6e6-126">Designer Support</span></span>

<span data-ttu-id="9c6e6-127">自适应卡设计器已更新为支持模板化。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-127">The Adaptive Card Designer has been updated to support templating.</span></span> 

> <span data-ttu-id="9c6e6-128">试用以下位置的 "vnext" 预览版: **[https://vnext.adaptivecards.io/designer](https://vnext.adaptivecards.io/designer)**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-128">Try out a "vnext" preview at: **[https://vnext.adaptivecards.io/designer](https://vnext.adaptivecards.io/designer)**</span></span>

<span data-ttu-id="9c6e6-129">[![影像](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](http://vnext.adaptivecards.io/designer)</span><span class="sxs-lookup"><span data-stu-id="9c6e6-129">[![image](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](http://vnext.adaptivecards.io/designer)</span></span>

 
<span data-ttu-id="9c6e6-130">此 "vnext" URL 将产生 bug, 并将频繁部署。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-130">This "vnext" URL is going to have bugs and will deploy frequently.</span></span> <span data-ttu-id="9c6e6-131">**清除缓存**以确保具有最新版本, 如果发现 bug, 请告诉我们!</span><span class="sxs-lookup"><span data-stu-id="9c6e6-131">**Clear your cache** to make sure you have the latest, and if you find bugs please let us know!</span></span>

* <span data-ttu-id="9c6e6-132">**示例数据编辑器**-在此处指定示例数据, 以在 "预览模式" 中查看数据绑定卡。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-132">**Sample Data Editor** - Specify sample data here to view the data-bound card when in "Preview Mode."</span></span> <span data-ttu-id="9c6e6-133">此窗格中有一个小按钮, 用于填充现有示例数据中的数据结构。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-133">There is a small button in this pane to populate the Data Structure from the existing sample data.</span></span>
* <span data-ttu-id="9c6e6-134">**数据结构**-这是示例数据的结构。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-134">**Data Structure** - This is the structure of your sample data.</span></span> <span data-ttu-id="9c6e6-135">可以将字段拖到设计图面上以创建对它们的绑定</span><span class="sxs-lookup"><span data-stu-id="9c6e6-135">Fields can be dragged onto the design surface to create a binding to them</span></span> 
* <span data-ttu-id="9c6e6-136">**预览模式**-按工具栏按钮, 在编辑体验和示例数据预览体验之间切换</span><span class="sxs-lookup"><span data-stu-id="9c6e6-136">**Preview Mode** - Press the toolbar button to toggle between the edit-experience and the sample-data-preview experience</span></span>
* <span data-ttu-id="9c6e6-137">**打开示例**-单击此按钮以打开各种示例负载</span><span class="sxs-lookup"><span data-stu-id="9c6e6-137">**Open Sample** - click this button to open various sample payloads</span></span>

## <a name="advanced-binding"></a><span data-ttu-id="9c6e6-138">高级绑定</span><span class="sxs-lookup"><span data-stu-id="9c6e6-138">Advanced binding</span></span>

### <a name="binding-scopes"></a><span data-ttu-id="9c6e6-139">绑定范围</span><span class="sxs-lookup"><span data-stu-id="9c6e6-139">Binding scopes</span></span>

<span data-ttu-id="9c6e6-140">有几个保留关键字可用于访问各种绑定范围。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-140">There are a few reserved keywords to access various binding scopes.</span></span> 

<span data-ttu-id="9c6e6-141">*注意:* 并非所有这些都是在预览版中实现的。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-141">*Note:* not all of these are implemented in the preview.</span></span>

```json
{
    "{<property>}": "Implicitly binds to `$data.<property>`",
    "$data": "The current data object",
    "$root": "The root data object. Useful when iterating to escape to parent object",
    "$index": "The current index when iterating",
    "$host": "Access properties of the host *(not working yet)*"
}
```

### <a name="assigning-a-data-context-to-elements"></a><span data-ttu-id="9c6e6-142">将数据上下文分配给元素</span><span class="sxs-lookup"><span data-stu-id="9c6e6-142">Assigning a data context to elements</span></span>

<span data-ttu-id="9c6e6-143">若要为任何元素分配 "数据上下文", 请`$data`将属性添加到元素。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-143">To assign a "data context" to any element add a `$data` attribute to the element.</span></span>

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

## <a name="repeating-items-in-an-array"></a><span data-ttu-id="9c6e6-144">数组中的重复项</span><span class="sxs-lookup"><span data-stu-id="9c6e6-144">Repeating items in an array</span></span>

<span data-ttu-id="9c6e6-145">此部分是 "暗幻"。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-145">This part is a bit of "dark magic".</span></span> <span data-ttu-id="9c6e6-146">欢迎提供反馈。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-146">Feedback welcome.</span></span>

* <span data-ttu-id="9c6e6-147">如果对象`$data`的属性设置为**数组**, 则**将为数组中的每个项重复该对象本身。**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-147">If the objects' `$data` property is set to an **array**, then the **object itself will be repeated for each item in the array.**</span></span> 
* <span data-ttu-id="9c6e6-148">由于它是重复的, `$data`因此在属性绑定中使用的范围限定为数组中的**单个项**。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-148">As it is being repeated, `$data` used in property bindings are scoped to the **individual item** within the array.</span></span>

<span data-ttu-id="9c6e6-149">例如, `TextBlock`下面将重复三次, 因为`$data`它是一个数组。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-149">For example, the `TextBlock` below will be repeated 3 times since it's `$data` is an array.</span></span> <span data-ttu-id="9c6e6-150">请注意`text`属性如何绑定到数组内`name`单个对象的属性。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-150">Notice how the `text` property is bound to the `name` property of an individual object within the array.</span></span> 

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

<span data-ttu-id="9c6e6-151">**导致:**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-151">**Resulting in:**</span></span>

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

## <a name="functions"></a><span data-ttu-id="9c6e6-152">Functions</span><span class="sxs-lookup"><span data-stu-id="9c6e6-152">Functions</span></span>

<span data-ttu-id="9c6e6-153">无需一些 helper 函数即可完成任何模板化语言。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-153">No templating language is complete without some helper functions.</span></span> <span data-ttu-id="9c6e6-154">我们将提供一组可在每个 SDK 上使用的标准函数。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-154">We will provide a standard set of functions that work on every SDK.</span></span> 

<span data-ttu-id="9c6e6-155">此处的语法仍在无线上, 因此请立即回来查看, 但以下是我们所计划的入门:</span><span class="sxs-lookup"><span data-stu-id="9c6e6-155">The syntax here is still up in the air so please check back soon, but here's a start of what we're planning:</span></span>

### <a name="string-functions"></a><span data-ttu-id="9c6e6-156">字符串函数</span><span class="sxs-lookup"><span data-stu-id="9c6e6-156">String functions</span></span>

* <span data-ttu-id="9c6e6-157">substr</span><span class="sxs-lookup"><span data-stu-id="9c6e6-157">substr</span></span>
* <span data-ttu-id="9c6e6-158">indexOf *(尚未工作)*</span><span class="sxs-lookup"><span data-stu-id="9c6e6-158">indexOf *(not working yet)*</span></span>
* <span data-ttu-id="9c6e6-159">toUpper *(尚未工作)*</span><span class="sxs-lookup"><span data-stu-id="9c6e6-159">toUpper *(not working yet)*</span></span>
* <span data-ttu-id="9c6e6-160">toLower *(尚未工作)*</span><span class="sxs-lookup"><span data-stu-id="9c6e6-160">toLower *(not working yet)*</span></span>

### <a name="number-functions"></a><span data-ttu-id="9c6e6-161">Number 函数</span><span class="sxs-lookup"><span data-stu-id="9c6e6-161">Number functions</span></span>

* <span data-ttu-id="9c6e6-162">格式 (货币、小数点等) *(尚未工作)*</span><span class="sxs-lookup"><span data-stu-id="9c6e6-162">Formatting (currency, decimal, etc) *(not working yet)*</span></span>

### <a name="date-functions"></a><span data-ttu-id="9c6e6-163">日期函数</span><span class="sxs-lookup"><span data-stu-id="9c6e6-163">Date functions</span></span>

* <span data-ttu-id="9c6e6-164">正在分析众所周知的日期字符串格式 *(尚未处理)*</span><span class="sxs-lookup"><span data-stu-id="9c6e6-164">Parsing well-known date string formats *(not working yet)*</span></span>
* <span data-ttu-id="9c6e6-165">格式众所周知的日期/时间表示形式 *(尚未处理)*</span><span class="sxs-lookup"><span data-stu-id="9c6e6-165">Formatting for well-known date/time representations *(not working yet)*</span></span>

### <a name="conditional-functions"></a><span data-ttu-id="9c6e6-166">条件函数</span><span class="sxs-lookup"><span data-stu-id="9c6e6-166">Conditional functions</span></span>

* <span data-ttu-id="9c6e6-167">if (*expression*, *trueValue*, *falseValue*)</span><span class="sxs-lookup"><span data-stu-id="9c6e6-167">if(*expression*, *trueValue*, *falseValue*)</span></span>

<span data-ttu-id="9c6e6-168">**`if`实例**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-168">**`if` example**</span></span>

```json
{
    "type": "TextBlock",
    "color": "if(priceChange >= 0, 'good', 'attention')"
}
```

### <a name="data-manipulation"></a><span data-ttu-id="9c6e6-169">数据操作</span><span class="sxs-lookup"><span data-stu-id="9c6e6-169">Data manipulation</span></span>

* <span data-ttu-id="9c6e6-170">JSON。分析-分析 JSON 字符串的能力</span><span class="sxs-lookup"><span data-stu-id="9c6e6-170">JSON.parse - ability to parse a JSON string</span></span> 

<span data-ttu-id="9c6e6-171">**`JSON.parse`实例**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-171">**`JSON.parse` example**</span></span>

<span data-ttu-id="9c6e6-172">这是一个 Azure DevOps 响应, 其中`message`的属性为 JSON 序列化字符串。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-172">This is an Azure DevOps response where the `message` property is a JSON-serialized string.</span></span> <span data-ttu-id="9c6e6-173">若要访问字符串中的值, 需要在模板中使用`JSON.parse`函数。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-173">In order to access values within the string, we need to use the `JSON.parse` function in our template.</span></span>

<span data-ttu-id="9c6e6-174">**数据**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-174">**Data**</span></span> 

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

<span data-ttu-id="9c6e6-175">**使用情况**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-175">**Usage**</span></span>

```json
{
    "type": "TextBlock",
    "text": "{JSON.parse(message).releaseName}"
}
```

<span data-ttu-id="9c6e6-176">**导致**</span><span class="sxs-lookup"><span data-stu-id="9c6e6-176">**Resulting In**</span></span>

```json
{
    "type": "TextBlock",
    "text": "Release-104"
}
```

### <a name="custom-functions"></a><span data-ttu-id="9c6e6-177">自定义函数</span><span class="sxs-lookup"><span data-stu-id="9c6e6-177">Custom functions</span></span>

<span data-ttu-id="9c6e6-178">我们希望确保主机可以添加自定义功能, 这意味着, 如果不支持某个函数, 我们需要提供对回退支持的可靠支持。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-178">We want to make sure Hosts can add custom functions, which means we need robust support for fallback support if a function isn't supported.</span></span> <span data-ttu-id="9c6e6-179">我们仍在评估这一点。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-179">We are still evaluating this.</span></span>

## <a name="conditional-layout"></a><span data-ttu-id="9c6e6-180">条件布局</span><span class="sxs-lookup"><span data-stu-id="9c6e6-180">Conditional layout</span></span>

<span data-ttu-id="9c6e6-181">若要在满足条件时删除整个元素, 请使用`$when`属性。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-181">To drop an entire element if a condition is met, use the `$when` property.</span></span> <span data-ttu-id="9c6e6-182">如果`$when`计算结果`false`为, 则不会向用户显示该元素。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-182">If `$when` evaluates to `false` the element will not appear to the user.</span></span>

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

### <a name="composing-templates"></a><span data-ttu-id="9c6e6-183">撰写模板</span><span class="sxs-lookup"><span data-stu-id="9c6e6-183">Composing templates</span></span>

<span data-ttu-id="9c6e6-184">当前不支持组合模板 "部件"。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-184">Currently there is no support for composing template "parts" together.</span></span> <span data-ttu-id="9c6e6-185">但我们会探索选项, 希望不久就能分享。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-185">But we are exploring options and hope to share more soon.</span></span> <span data-ttu-id="9c6e6-186">这里欢迎你的想法!</span><span class="sxs-lookup"><span data-stu-id="9c6e6-186">Any thoughts here welcome!</span></span>


## <a name="examples"></a><span data-ttu-id="9c6e6-187">示例</span><span class="sxs-lookup"><span data-stu-id="9c6e6-187">Examples</span></span>

<span data-ttu-id="9c6e6-188">到目前为止, 我们仅创建了有限数量的示例, 但请查看此处以开始使用。</span><span class="sxs-lookup"><span data-stu-id="9c6e6-188">We only have a limited amount of samples created so far, but take a look here to get started.</span></span>

* <span data-ttu-id="9c6e6-189">通过单击 "**打开示例**" 在[设计器](http://vnext.adaptivecards.io/designer)中加载示例</span><span class="sxs-lookup"><span data-stu-id="9c6e6-189">Load samples within the [designer](http://vnext.adaptivecards.io/designer) by clicking **Open Sample**</span></span>
* <span data-ttu-id="9c6e6-190">或者只是直接[浏览它们的目录](https://github.com/Microsoft/AdaptiveCards/tree/js/template-engine/samples/v2.0/Scenarios)</span><span class="sxs-lookup"><span data-stu-id="9c6e6-190">Or just [browse a directory of them](https://github.com/Microsoft/AdaptiveCards/tree/js/template-engine/samples/v2.0/Scenarios) directly</span></span>
