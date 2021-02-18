---
title: 自适应卡片模板语言
author: matthidinger
ms.author: mahiding
ms.date: 05/18/2020
ms.topic: article
ms.openlocfilehash: 3c451c62f9345fd4072e560cb001b1d77996e093
ms.sourcegitcommit: 0ed81e04d8cdcf8f8bf6f854edf53b7eb9f67d2a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532638"
---
# <a name="adaptive-cards-template-language"></a><span data-ttu-id="ab7e8-102">自适应卡片模板语言</span><span class="sxs-lookup"><span data-stu-id="ab7e8-102">Adaptive Cards Template Language</span></span>

<span data-ttu-id="ab7e8-103">模板化可以将自适应卡片中的 **数据** 与 **布局** 分开。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-103">Templating enables the separation of **data** from **layout** in your Adaptive Card.</span></span> <span data-ttu-id="ab7e8-104">模板语言是用于创作模板的语法。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-104">The template language is the syntax used to author a template.</span></span> 

> <span data-ttu-id="ab7e8-105">有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)</span><span class="sxs-lookup"><span data-stu-id="ab7e8-105">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="ab7e8-106">**2020 年 5 月候选发布版本** 中的 **中断性变更**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-106">**Breaking changes** in the **May 2020 Release Candidate**</span></span>
>
> <span data-ttu-id="ab7e8-107">我们正在努力工作，力求尽早发布模板，我们已经在做最后的冲刺了！</span><span class="sxs-lookup"><span data-stu-id="ab7e8-107">We've been hard at work getting templating released, and we're finally in the home stretch!</span></span> <span data-ttu-id="ab7e8-108">发布之前，我们需要进行一些小的中断性变更。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-108">We had to make some minor breaking changes as we close on the release.</span></span>

## <a name="breaking-changes-as-of-may-2020"></a><span data-ttu-id="ab7e8-109">2020 年 5 月起的中断性变更</span><span class="sxs-lookup"><span data-stu-id="ab7e8-109">Breaking changes as of May 2020</span></span>

1. <span data-ttu-id="ab7e8-110">绑定语法已从 `{...}` 更改为 `${...}`</span><span class="sxs-lookup"><span data-stu-id="ab7e8-110">The binding syntax changed from `{...}` to `${...}`</span></span>
    * <span data-ttu-id="ab7e8-111">例如：`"text": "Hello {name}"` 变为 `"text": "Hello ${name}"`</span><span class="sxs-lookup"><span data-stu-id="ab7e8-111">For Example: `"text": "Hello {name}"` becomes `"text": "Hello ${name}"`</span></span>
    
## <a name="binding-to-data"></a><span data-ttu-id="ab7e8-112">绑定到数据</span><span class="sxs-lookup"><span data-stu-id="ab7e8-112">Binding to data</span></span>

<span data-ttu-id="ab7e8-113">编写模板非常简单，只需要将卡片的“非静态”内容替换为“绑定表达式”即可。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-113">Writing a template is as simple as replacing the "non-static" content of your card with "binding expressions".</span></span>

### <a name="static-card-payload"></a><span data-ttu-id="ab7e8-114">静态卡片有效负载</span><span class="sxs-lookup"><span data-stu-id="ab7e8-114">Static card payload</span></span>

```json
{
   "type": "TextBlock",
   "text": "Matt"
}
```

### <a name="template-payload"></a><span data-ttu-id="ab7e8-115">模板有效负载</span><span class="sxs-lookup"><span data-stu-id="ab7e8-115">Template payload</span></span>

```json
{
   "type": "TextBlock",
   "text": "${firstName}"
}
```

* <span data-ttu-id="ab7e8-116">任何存在静态内容的地方几乎都可以放置绑定表达式</span><span class="sxs-lookup"><span data-stu-id="ab7e8-116">Binding expressions can be placed just about anywhere that static content can be</span></span>
* <span data-ttu-id="ab7e8-117">绑定语法以 `${` 开头，以 `}` 结尾。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-117">The binding syntax starts with `${` and ends with `}`.</span></span> <span data-ttu-id="ab7e8-118">例如 `${myProperty}`</span><span class="sxs-lookup"><span data-stu-id="ab7e8-118">E.g., `${myProperty}`</span></span>
* <span data-ttu-id="ab7e8-119">使用点表示法访问对象层次结构的子对象。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-119">Use *Dot-notation* to access sub-objects of an object hierarchy.</span></span> <span data-ttu-id="ab7e8-120">例如 `${myParent.myChild}`</span><span class="sxs-lookup"><span data-stu-id="ab7e8-120">E.g., `${myParent.myChild}`</span></span>
* <span data-ttu-id="ab7e8-121">采用正常的 null 处理方式，可确保在访问对象图中的 null 属性时不会收到异常</span><span class="sxs-lookup"><span data-stu-id="ab7e8-121">Graceful null handling ensures you won't get exceptions if you access a null property in an object graph</span></span>
* <span data-ttu-id="ab7e8-122">使用索引器语法，按键或数组中的项检索属性。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-122">Use *Indexer syntax* to retrieve properties by key or items in an array.</span></span> <span data-ttu-id="ab7e8-123">例如 `${myArray[0]}`</span><span class="sxs-lookup"><span data-stu-id="ab7e8-123">E.g., `${myArray[0]}`</span></span>

## <a name="providing-the-data"></a><span data-ttu-id="ab7e8-124">提供数据</span><span class="sxs-lookup"><span data-stu-id="ab7e8-124">Providing the data</span></span>

<span data-ttu-id="ab7e8-125">有了模板后，需要提供数据，以得到完整的模板。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-125">Now that you have a template, you'll want to provide the data that makes it complete.</span></span> <span data-ttu-id="ab7e8-126">有两个选项可用来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="ab7e8-126">You have two options to do this:</span></span>

1. <span data-ttu-id="ab7e8-127">**选项 A：在模板有效负载内执行内联**。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-127">**Option A: Inline within the template payload**.</span></span> <span data-ttu-id="ab7e8-128">可以在 `AdaptiveCard` 模板负载中以内联方式提供数据。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-128">You can provide the data inline within the `AdaptiveCard` template payload.</span></span> <span data-ttu-id="ab7e8-129">为此，只需将 `$data` 特性添加到根 `AdaptiveCard` 对象即可。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-129">To do so, simply add a `$data` attribute to the root `AdaptiveCard` object.</span></span>
2. <span data-ttu-id="ab7e8-130">**选项 B：作为单独的数据对象提供**。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-130">**Option B: As a separate data object**.</span></span> <span data-ttu-id="ab7e8-131">如果选择此选项，则在运行时向[模板化 SDK](sdk.md) 提供两个单独的对象：`template` 和 `data`。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-131">With this option you provide two separate objects to the [Templating SDK](sdk.md) at runtime: the `template` and the `data`.</span></span> <span data-ttu-id="ab7e8-132">这是更常见的方法，因为通常的情况是创建一个模板，然后在以后提供动态数据。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-132">This will be the more common approach, since typically you will create a template and want to provide dynamic data later.</span></span>

### <a name="option-a-inline-data"></a><span data-ttu-id="ab7e8-133">选项 A：内联数据</span><span class="sxs-lookup"><span data-stu-id="ab7e8-133">Option A: Inline data</span></span>

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
            "text": "Hi ${employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: ${employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: ${employee.peers[0].name}, ${employee.peers[1].name}, ${employee.peers[2].name}"
        }
    ]
}
```

### <a name="option-b-separating-the-template-from-the-data"></a><span data-ttu-id="ab7e8-134">选项 B：将模板与数据分离</span><span class="sxs-lookup"><span data-stu-id="ab7e8-134">Option B: Separating the template from the data</span></span>

<span data-ttu-id="ab7e8-135">另外，还可以创建一个可反复使用的不含数据的卡片“模板”（可能性更高）。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-135">Alternatively (and more likely), you'll create a re-usable card template without including the data.</span></span> <span data-ttu-id="ab7e8-136">此模板可以存储为文件并添加到源代码管理中。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-136">This template could be stored as a file and added to source control.</span></span>

<span data-ttu-id="ab7e8-137">**EmployeeCardTemplate.json**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-137">**EmployeeCardTemplate.json**</span></span>

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Hi ${employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: ${employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: ${employee.peers[0].name}, ${employee.peers[1].name}, ${employee.peers[2].name}"
        }
    ]
}
```

<span data-ttu-id="ab7e8-138">然后，将其加载并使用 [模板化 SDK](sdk.md) 在运行时提供数据。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-138">Then load it up and provide the data at runtime using the [Templating SDKs](sdk.md).</span></span>

<span data-ttu-id="ab7e8-139">**JavaScript 示例**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-139">**JavaScript example**</span></span>

<span data-ttu-id="ab7e8-140">使用 [adaptivecards-templating](https://npmjs.com/package/adaptivecards-templating) 包。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-140">Using the [adaptivecards-templating](https://npmjs.com/package/adaptivecards-templating) package.</span></span>

```js
var template = new ACData.Template({ 
    // EmployeeCardTemplate goes here
});

// Specify data at runtime
var card = template.expand({
    $root: {
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
    }
});

// Now you have an AdaptiveCard ready to render!
```

## <a name="designer-support"></a><span data-ttu-id="ab7e8-141">设计器支持</span><span class="sxs-lookup"><span data-stu-id="ab7e8-141">Designer Support</span></span>

<span data-ttu-id="ab7e8-142">自适应卡片设计器已更新为支持模板化。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-142">The Adaptive Card Designer has been updated to support templating.</span></span> 

> <span data-ttu-id="ab7e8-143">试用网址： **[https://adaptivecards.io/designer](https://adaptivecards.io/designer)**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-143">Try it out at: **[https://adaptivecards.io/designer](https://adaptivecards.io/designer)**</span></span>

<span data-ttu-id="ab7e8-144">[![图像](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](https://adaptivecards.io/designer)</span><span class="sxs-lookup"><span data-stu-id="ab7e8-144">[![image](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](https://adaptivecards.io/designer)</span></span>

* <span data-ttu-id="ab7e8-145">**示例数据编辑器** - 在此处指定示例数据，以便在“预览模式”下查看数据绑定卡片。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-145">**Sample Data Editor** - Specify sample data here to view the data-bound card when in "Preview Mode."</span></span> <span data-ttu-id="ab7e8-146">此窗格中有一个小按钮，用于填充现有示例数据中的“数据结构”。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-146">There is a small button in this pane to populate the Data Structure from the existing sample data.</span></span>
* <span data-ttu-id="ab7e8-147">**预览模式** - 按工具栏按钮即可在编辑体验和示例数据预览体验之间切换</span><span class="sxs-lookup"><span data-stu-id="ab7e8-147">**Preview Mode** - Press the toolbar button to toggle between the edit-experience and the sample-data-preview experience</span></span>
* <span data-ttu-id="ab7e8-148">**打开示例** - 单击此按钮即可打开各种示例有效负载</span><span class="sxs-lookup"><span data-stu-id="ab7e8-148">**Open Sample** - click this button to open various sample payloads</span></span>

## <a name="advanced-binding"></a><span data-ttu-id="ab7e8-149">高级绑定</span><span class="sxs-lookup"><span data-stu-id="ab7e8-149">Advanced binding</span></span>

### <a name="binding-scopes"></a><span data-ttu-id="ab7e8-150">绑定范围</span><span class="sxs-lookup"><span data-stu-id="ab7e8-150">Binding scopes</span></span>

<span data-ttu-id="ab7e8-151">可以通过几个保留关键字来访问各种绑定范围。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-151">There are a few reserved keywords to access various binding scopes.</span></span> 

```json
{
    "${<property>}": "Implicitly binds to `$data.<property>`",
    "$data": "The current data object",
    "$root": "The root data object. Useful when iterating to escape to parent object",
    "$index": "The current index when iterating"
}
```

### <a name="assigning-a-data-context-to-elements"></a><span data-ttu-id="ab7e8-152">将数据上下文分配给元素</span><span class="sxs-lookup"><span data-stu-id="ab7e8-152">Assigning a data context to elements</span></span>

<span data-ttu-id="ab7e8-153">若要为任意元素分配“数据上下文”，请将 `$data` 属性添加到该元素。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-153">To assign a "data context" to any element add a `$data` attribute to the element.</span></span>

```json
{
    "type": "Container",
    "$data": "${mySubObject}",
    "items": [
        {
            "type": "TextBlock",
            "text": "This TextBlock is now scoped directly to 'mySubObject': ${mySubObjectProperty}"
        },
        {
            "type": "TextBlock",
            "text": "To break-out and access the root data, use: ${$root}"
        }
    ]
}
```

## <a name="repeating-items-in-an-array"></a><span data-ttu-id="ab7e8-154">数组中的重复项</span><span class="sxs-lookup"><span data-stu-id="ab7e8-154">Repeating items in an array</span></span>

* <span data-ttu-id="ab7e8-155">如果将某个自适应卡片元素的 `$data` 属性绑定到 **数组**，则 **会针对数组中的每个项重复元素本身。**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-155">If an Adaptive Card element's `$data` property is bound to an **array**, then the **element itself will be repeated for each item in the array.**</span></span> 
* <span data-ttu-id="ab7e8-156">在属性值中使用的任何绑定表达式 (`${myProperty}`) 的作用域都将是数组中的 **单个项**。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-156">Any binding expressions (`${myProperty}`) used in property values will be scoped to the **individual item** within the array.</span></span>
* <span data-ttu-id="ab7e8-157">如果绑定到字符串数组，请使用 `${$data}` 访问单个字符串元素。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-157">If binding to an array of strings, use `${$data}` to access the individual string element.</span></span> <span data-ttu-id="ab7e8-158">例如 `"text": "${$data}"`</span><span class="sxs-lookup"><span data-stu-id="ab7e8-158">E.g., `"text": "${$data}"`</span></span>

<span data-ttu-id="ab7e8-159">举例来说，下面的 `TextBlock` 会重复 3 次，因为其 `$data` 是数组。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-159">For example, the `TextBlock` below will be repeated 3 times since it's `$data` is an array.</span></span> <span data-ttu-id="ab7e8-160">请注意 `text` 属性如何绑定到数组内单个对象的 `name` 属性。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-160">Notice how the `text` property is bound to the `name` property of an individual object within the array.</span></span> 

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
            "text": "${name}"
        }
    ]
}
```

<span data-ttu-id="ab7e8-161">**结果：**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-161">**Resulting in:**</span></span>

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

## <a name="built-in-functions"></a><span data-ttu-id="ab7e8-162">内置函数</span><span class="sxs-lookup"><span data-stu-id="ab7e8-162">Built-in functions</span></span>

<span data-ttu-id="ab7e8-163">如果没有一整套丰富的帮助程序函数，则任何模板化语言都不是完整的。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-163">No templating language is complete without a rich suite of helper functions.</span></span> <span data-ttu-id="ab7e8-164">自适应卡模板化建立在[自适应表达式语言](/azure/bot-service/bot-builder-concept-adaptive-expressions) (AEL) 的基础之上，后者是声明可在许多不同平台上进行计算的表达式的开放性标准。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-164">Adaptive Card Templating is built on top of the [Adaptive Expression Language](/azure/bot-service/bot-builder-concept-adaptive-expressions) (AEL), which is an open standard for declaring expressions that can be evaluated on many different platforms.</span></span> <span data-ttu-id="ab7e8-165">而且它是“逻辑应用”的一个适当超集，因此可以使用与 Power Automate 等类似的语法。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-165">And it's a proper superset of "Logic Apps", so you can use similar syntax as Power Automate, etc.</span></span>

<span data-ttu-id="ab7e8-166">**这只是一小部分内置函数的示例。**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-166">**This is just a small sampling of the built-in functions.**</span></span>

<span data-ttu-id="ab7e8-167">查看[自适应表达式语言预生成函数](/azure/bot-service/bot-builder-concept-adaptive-expressions?view=azure-bot-service-4.0)的完整列表。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-167">Check out the full list of [Adaptive Expression Language Pre-built functions](/azure/bot-service/bot-builder-concept-adaptive-expressions?view=azure-bot-service-4.0).</span></span>

### <a name="conditional-evaluation"></a><span data-ttu-id="ab7e8-168">条件计算</span><span class="sxs-lookup"><span data-stu-id="ab7e8-168">Conditional evaluation</span></span>

* <span data-ttu-id="ab7e8-169">if(*表达式*, *trueValue*, *falseValue*)</span><span class="sxs-lookup"><span data-stu-id="ab7e8-169">if(*expression*, *trueValue*, *falseValue*)</span></span>

<span data-ttu-id="ab7e8-170">**`if` 示例**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-170">**`if` example**</span></span>

```json
{
    "type": "TextBlock",
    "color": "${if(priceChange >= 0, 'good', 'attention')}"
}
```

### <a name="parsing-json"></a><span data-ttu-id="ab7e8-171">分析 JSON</span><span class="sxs-lookup"><span data-stu-id="ab7e8-171">Parsing JSON</span></span>

* <span data-ttu-id="ab7e8-172">json(*jsonString*) - 分析 JSON 字符串</span><span class="sxs-lookup"><span data-stu-id="ab7e8-172">json(*jsonString*) - Parse a JSON string</span></span>

<span data-ttu-id="ab7e8-173">**`json` 示例**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-173">**`json` example**</span></span>

<span data-ttu-id="ab7e8-174">这是 Azure DevOps 响应，其中的 `message` 属性是一个 JSON 序列化字符串。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-174">This is an Azure DevOps response where the `message` property is a JSON-serialized string.</span></span> <span data-ttu-id="ab7e8-175">若要访问字符串中的值，需要在模板中使用 `json` 函数。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-175">In order to access values within the string, we need to use the `json` function in our template.</span></span>

<span data-ttu-id="ab7e8-176">**数据**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-176">**Data**</span></span> 

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

<span data-ttu-id="ab7e8-177">**用法**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-177">**Usage**</span></span>

```json
{
    "type": "TextBlock",
    "text": "${json(message).releaseName}"
}
```

<span data-ttu-id="ab7e8-178">**结果**</span><span class="sxs-lookup"><span data-stu-id="ab7e8-178">**Resulting In**</span></span>

```json
{
    "type": "TextBlock",
    "text": "Release-104"
}
```

### <a name="custom-functions"></a><span data-ttu-id="ab7e8-179">自定义函数</span><span class="sxs-lookup"><span data-stu-id="ab7e8-179">Custom functions</span></span>

<span data-ttu-id="ab7e8-180">[模板化 SDK](sdk.md) 中通过 API 支持自定义函数。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-180">Custom functions are supported via APIs in the [Templating SDKs](sdk.md).</span></span> 

## <a name="conditional-layout-with-when"></a><span data-ttu-id="ab7e8-181">使用 `$when` 的条件布局</span><span class="sxs-lookup"><span data-stu-id="ab7e8-181">Conditional layout with `$when`</span></span>

<span data-ttu-id="ab7e8-182">若要在满足条件时删除整个元素，请使用 `$when` 属性。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-182">To drop an entire element if a condition is met, use the `$when` property.</span></span> <span data-ttu-id="ab7e8-183">如果 `$when` 的计算结果为 `false`，则此元素不会显示给用户。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-183">If `$when` evaluates to `false` the element will not appear to the user.</span></span>

```json
{
    "type": "AdaptiveCard",
    "$data": {
        "price": "35"
    },
    "body": [
        {
            "type": "TextBlock",
            "$when": "${price > 30}",
            "text": "This thing is pricy!",
            "color": "attention",
        },
         {
            "type": "TextBlock",
            "$when": "${price <= 30}",
            "text": "Dang, this thing is cheap!",
            "color": "good"
        }
    ]
}
```

### <a name="composing-templates"></a><span data-ttu-id="ab7e8-184">组合模板</span><span class="sxs-lookup"><span data-stu-id="ab7e8-184">Composing templates</span></span>

<span data-ttu-id="ab7e8-185">目前不支持将模板“部件”组合到一起。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-185">Currently there is no support for composing template "parts" together.</span></span> <span data-ttu-id="ab7e8-186">但是，我们会探索相关选项，希望不久就能为大家提供更多此方面的内容。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-186">But we are exploring options and hope to share more soon.</span></span> <span data-ttu-id="ab7e8-187">欢迎你在此提供自己的想法！</span><span class="sxs-lookup"><span data-stu-id="ab7e8-187">Any thoughts here welcome!</span></span>

## <a name="examples"></a><span data-ttu-id="ab7e8-188">示例</span><span class="sxs-lookup"><span data-stu-id="ab7e8-188">Examples</span></span>

<span data-ttu-id="ab7e8-189">请浏览更新的[“示例”页](https://adaptivecards.io/samples)，其中包含各种新的模板化卡片。</span><span class="sxs-lookup"><span data-stu-id="ab7e8-189">Browse the updated [Samples page](https://adaptivecards.io/samples) to explore all sorts of new templated cards.</span></span>