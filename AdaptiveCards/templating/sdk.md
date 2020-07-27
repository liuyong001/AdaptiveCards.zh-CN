---
title: 将 SDK 模板化
author: matthidinger
ms.author: mahiding
ms.date: 05/15/2020
ms.topic: article
ms.openlocfilehash: a8db2f5ef84203187ed1b9d0fc8dd3ce63ee3569
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417575"
---
# <a name="adaptive-card-templating-sdks"></a><span data-ttu-id="edae4-102">自适应卡片模板化 SDK</span><span class="sxs-lookup"><span data-stu-id="edae4-102">Adaptive Card Templating SDKs</span></span>

<span data-ttu-id="edae4-103">有了自适应卡片模板化 SDK，就可以轻松地使用任何受支持的平台上的实际数据来填充[卡片模板](language.md)。</span><span class="sxs-lookup"><span data-stu-id="edae4-103">The Adaptive Card Templating SDKs make it easy to populate a [card template](language.md) with real data on any supported platform.</span></span>

> <span data-ttu-id="edae4-104">有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)</span><span class="sxs-lookup"><span data-stu-id="edae4-104">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="edae4-105">**2020 年 5 月候选发布版本**中的**中断性变更**</span><span class="sxs-lookup"><span data-stu-id="edae4-105">**Breaking changes** in the **May 2020 Release Candidate**</span></span>
>
> <span data-ttu-id="edae4-106">我们正在努力工作，力求尽早发布模板，我们已经在做最后的冲刺了！</span><span class="sxs-lookup"><span data-stu-id="edae4-106">We've been hard at work getting templating released, and we're finally in the home stretch!</span></span> <span data-ttu-id="edae4-107">发布之前，我们需要进行一些小的中断性变更。</span><span class="sxs-lookup"><span data-stu-id="edae4-107">We had to make some minor breaking changes as we close on the release.</span></span>

## <a name="breaking-changes-as-of-may-2020"></a><span data-ttu-id="edae4-108">2020 年 5 月起的中断性变更</span><span class="sxs-lookup"><span data-stu-id="edae4-108">Breaking changes as of May 2020</span></span>

1. <span data-ttu-id="edae4-109">绑定语法已从 `{...}` 更改为 `${...}`。</span><span class="sxs-lookup"><span data-stu-id="edae4-109">The binding syntax changed from `{...}` to `${...}`.</span></span> 
    * <span data-ttu-id="edae4-110">例如：`"text": "Hello {name}"` 变为 `"text": "Hello ${name}"`</span><span class="sxs-lookup"><span data-stu-id="edae4-110">For Example: `"text": "Hello {name}"` becomes `"text": "Hello ${name}"`</span></span>
2. <span data-ttu-id="edae4-111">JavaScript API 不再包含 `EvaluationContext` 对象。</span><span class="sxs-lookup"><span data-stu-id="edae4-111">The JavaScript API no longer contains an `EvaluationContext` object.</span></span> <span data-ttu-id="edae4-112">只需将数据传递到 `expand` 函数。</span><span class="sxs-lookup"><span data-stu-id="edae4-112">Simply pass your data to the `expand` function.</span></span> <span data-ttu-id="edae4-113">有关完整的详细信息，请参阅 [SDK 页](sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="edae4-113">Please see the [SDK page](sdk.md) for full details.</span></span>
3. <span data-ttu-id="edae4-114">.NET API 经过了重新设计，以便更紧密地匹配 JavaScript API。</span><span class="sxs-lookup"><span data-stu-id="edae4-114">The .NET API was redesigned to more closely match the JavaScript API.</span></span> <span data-ttu-id="edae4-115">有关完整详细信息，请查看以下内容。</span><span class="sxs-lookup"><span data-stu-id="edae4-115">Please below for full details.</span></span>

## <a name="javascript"></a><span data-ttu-id="edae4-116">JavaScript</span><span class="sxs-lookup"><span data-stu-id="edae4-116">JavaScript</span></span>

<span data-ttu-id="edae4-117">可以通过 npm 和 CDN 获取 [adaptivecards-templating](https://www.npmjs.com/package/adaptivecards-templating) 库。</span><span class="sxs-lookup"><span data-stu-id="edae4-117">The [adaptivecards-templating](https://www.npmjs.com/package/adaptivecards-templating) library is available on npm and via CDN.</span></span> <span data-ttu-id="edae4-118">如需完整文档，请查看包链接。</span><span class="sxs-lookup"><span data-stu-id="edae4-118">See the package link for full documentation.</span></span>

### <a name="npm"></a><span data-ttu-id="edae4-119">npm</span><span class="sxs-lookup"><span data-stu-id="edae4-119">npm</span></span>

<span data-ttu-id="edae4-120">[![npm install](https://img.shields.io/npm/v/adaptivecards-templating.svg)](https://www.npmjs.com/package/adaptivecards-templating)</span><span class="sxs-lookup"><span data-stu-id="edae4-120">[![npm install](https://img.shields.io/npm/v/adaptivecards-templating.svg)](https://www.npmjs.com/package/adaptivecards-templating)</span></span>

```console
npm install adaptivecards-templating
```

### <a name="cdn"></a><span data-ttu-id="edae4-121">CDN</span><span class="sxs-lookup"><span data-stu-id="edae4-121">CDN</span></span>

```html
<script src="https://unpkg.com/adaptivecards-templating/dist/adaptivecards-templating.min.js"></script>
``` 


### <a name="usage"></a><span data-ttu-id="edae4-122">用法</span><span class="sxs-lookup"><span data-stu-id="edae4-122">Usage</span></span>

<span data-ttu-id="edae4-123">以下示例假定你还安装了 [adaptivecards](https://www.npmjs.com/package/adaptivecards) 库来呈现卡。</span><span class="sxs-lookup"><span data-stu-id="edae4-123">The sample below assumes you've also installed the [adaptivecards](https://www.npmjs.com/package/adaptivecards) library in order to render the card.</span></span> 

<span data-ttu-id="edae4-124">如果不打算呈现卡，可以删除 `parse` 和 `render` 代码。</span><span class="sxs-lookup"><span data-stu-id="edae4-124">If you don't plan on rendering the card then you can remove the `parse` and `render` code.</span></span> 

```js
import * as ACData from "adaptivecards-templating";
import * as AdaptiveCards from "adaptivecards";
 
// Define a template payload
var templatePayload = {
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "Hello ${name}!"
        }
    ]
};
 
// Create a Template instance from the template payload
var template = new ACData.Template(templatePayload);
 
// Expand the template with your `$root` data object.
// This binds it to the data and produces the final Adaptive Card payload
var cardPayload = template.expand({
   $root: {
      name: "Matt Hidinger"
   }
});
 
// OPTIONAL: Render the card (requires that the adaptivecards library be loaded)
var adaptiveCard = new AdaptiveCards.AdaptiveCard();
adaptiveCard.parse(cardPayload);
document.getElementById('exampleDiv').appendChild(adaptiveCard.render());
```

## <a name="net"></a><span data-ttu-id="edae4-125">.NET</span><span class="sxs-lookup"><span data-stu-id="edae4-125">.NET</span></span> 

> [!IMPORTANT] 
> 
> <span data-ttu-id="edae4-126">.NET 候选发布版本将于 5 月 23 日左右发布。</span><span class="sxs-lookup"><span data-stu-id="edae4-126">The .NET Release Candidate will be available around 05/23.</span></span> <span data-ttu-id="edae4-127">查找版本 `1.0.0-RC1`</span><span class="sxs-lookup"><span data-stu-id="edae4-127">Look for version `1.0.0-RC1`</span></span>
>

<span data-ttu-id="edae4-128">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Templating.svg)](https://www.nuget.org/packages/AdaptiveCards.Templating)</span><span class="sxs-lookup"><span data-stu-id="edae4-128">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.Templating.svg)](https://www.nuget.org/packages/AdaptiveCards.Templating)</span></span>

```console
dotnet add package AdaptiveCards.Templating
```

### <a name="usage"></a><span data-ttu-id="edae4-129">用法</span><span class="sxs-lookup"><span data-stu-id="edae4-129">Usage</span></span>

```cs
// Import the library 
using AdaptiveCards.Templating;
```

```cs
var templateJson = @"
{
    ""type"": ""AdaptiveCard"",
    ""version"": ""1.2"",
    ""body"": [
        {
            ""type"": ""TextBlock"",
            ""text"": ""Hello ${name}!""
        }
    ]
}";

// Create a Template instance from the template payload
AdaptiveCardTemplate template = new AdaptiveCardTemplate(templateJson);

// You can use any serializable object as your data
var myData = new
{
    Name = "Matt Hidinger"
};

// "Expand" the template - this generates the final Adaptive Card payload
string cardJson = template.Expand(myData);
```

### <a name="custom-functions"></a><span data-ttu-id="edae4-130">自定义函数</span><span class="sxs-lookup"><span data-stu-id="edae4-130">Custom Functions</span></span>

<span data-ttu-id="edae4-131">除了预生成函数外，还可以将自定义函数添加到自适应表达式库中。</span><span class="sxs-lookup"><span data-stu-id="edae4-131">Custom functions can be added to Adaptive Expression Library in addition to the prebuilt functions.</span></span>

<span data-ttu-id="edae4-132">下面的示例中添加了 stringFormat 自定义函数，并使用该函数设置字符串的格式。</span><span class="sxs-lookup"><span data-stu-id="edae4-132">In the below example, stringFormat custom function is added, and the funtion is used to format a string.</span></span>
```cs
string jsonTemplate = @"{
    ""type"": ""AdaptiveCard"",
    ""version"": ""1.0"",
    ""body"": [{
        ""type"": ""TextBlock"",
        ""text"": ""${stringFormat(strings.myName, person.firstName, person.lastName)}""
    }]
}";

string jsonData = @"{
    ""strings"": {
        ""myName"": ""My name is {0} {1}""
    },
    ""person"": {
        ""firstName"": ""Andrew"",
        ""lastName"": ""Leader""
    }
}";

AdaptiveCardTemplate template = new AdaptiveCardTemplate(jsonTemplate);

var context = new EvaluationContext
{
    Root = jsonData
};

// a custom function is added
AdaptiveExpressions.Expression.Functions.Add("stringFormat", (args) =>
{
    string formattedString = "";

    // argument is packed in sequential order as defined in the template
    // For example, suppose we have "${stringFormat(strings.myName, person.firstName, person.lastName)}"
    // args will have following entries
    // args[0]: strings.myName
    // args[1]: person.firstName
    // args[2]: strings.lastName
    if (args[0] != null && args[1] != null && args[2] != null) 
    {
        string formatString = args[0];
        string[] stringArguments = {args[1], args[2] };
        formattedString = string.Format(formatString, stringArguments);
    }
    return formattedString;
});

string cardJson = template.Expand(context);
```

## <a name="troubleshooting"></a><span data-ttu-id="edae4-133">疑难解答</span><span class="sxs-lookup"><span data-stu-id="edae4-133">Troubleshooting</span></span>
<span data-ttu-id="edae4-134">问：</span><span class="sxs-lookup"><span data-stu-id="edae4-134">Q.</span></span> <span data-ttu-id="edae4-135">我为什么会遇到 AdaptiveTemplateException ```expand()```？</span><span class="sxs-lookup"><span data-stu-id="edae4-135">Why am I running into an AdaptiveTemplateException calling ```expand()```?</span></span>   
<span data-ttu-id="edae4-136">A.</span><span class="sxs-lookup"><span data-stu-id="edae4-136">A.</span></span> <span data-ttu-id="edae4-137">如果错误消息类似于：“第 \<line number> 行的‘\<offending item>’中的‘$data :’对格式错误”。</span><span class="sxs-lookup"><span data-stu-id="edae4-137">If your error message looks like '\<offending item>' at line, '\<line number>' is **malformed for '$data : ' pair**".</span></span>   
<span data-ttu-id="edae4-138">请确保为 "$data" 提供的值是有效的 json，如数字、布尔值、对象和数组，或确保正确使用了自适应模板语言的语法，条目在数据上下文中的行号处。</span><span class="sxs-lookup"><span data-stu-id="edae4-138">Please ensure that value provided for "$data" is valid json such as number, boolean, object, and array, or follows correct syntax for Adaptive Template language,  and the entry exists in the data context at the line number.</span></span>

<span data-ttu-id="edae4-139">问：</span><span class="sxs-lookup"><span data-stu-id="edae4-139">Q.</span></span> <span data-ttu-id="edae4-140">我为什么会遇到 ArgumentNullException ```expand()```？</span><span class="sxs-lookup"><span data-stu-id="edae4-140">Why am I running into an ArgumentNullException calling ```expand()```?</span></span>   
<span data-ttu-id="edae4-141">A.</span><span class="sxs-lookup"><span data-stu-id="edae4-141">A.</span></span> <span data-ttu-id="edae4-142">如果错误消息类似于：“请检查是否设置了父数据上下文，或者为第 \<line number> 行的‘\<offending item>’输入一个非空值”。</span><span class="sxs-lookup"><span data-stu-id="edae4-142">If your error message looks like" **Check if parent data context is set, or please enter a non-null value for** '\<offending item>' at line, '\<line number>'".</span></span>   
<span data-ttu-id="edae4-143">它指示不存在所请求的数据绑定的数据上下文。</span><span class="sxs-lookup"><span data-stu-id="edae4-143">It indicates that there doesn't exist data context for the requested data binding.</span></span> <span data-ttu-id="edae4-144">请确保设置了根数据上下文，如果存在，请确保有数据上下文可用于行号所指示的当前绑定。</span><span class="sxs-lookup"><span data-stu-id="edae4-144">Please ensure that root data context is set, if exists, ensure that any data context is available for current binding as indicated by the line number.</span></span>

<span data-ttu-id="edae4-145">问：</span><span class="sxs-lookup"><span data-stu-id="edae4-145">Q.</span></span> <span data-ttu-id="edae4-146">RFC 3389 格式的日期/时间（例如“2017-02-14T06:08:00Z”）在与模板一起使用时为何不可用于 TIME/DATE 函数？</span><span class="sxs-lookup"><span data-stu-id="edae4-146">Why date/time in RFC 3389 format e.g "2017-02-14T06:08:00Z" when used with template doesn't works with TIME/DATE functions?</span></span>   
<span data-ttu-id="edae4-147">A.</span><span class="sxs-lookup"><span data-stu-id="edae4-147">A.</span></span> <span data-ttu-id="edae4-148">.NET SDK NuGet 版本 1.0.0-rc.0 具有此行为。</span><span class="sxs-lookup"><span data-stu-id="edae4-148">.NET sdk nuget version 1.0.0-rc.0 exhibits this behavior.</span></span> <span data-ttu-id="edae4-149">它已在后续版本中得到更正。</span><span class="sxs-lookup"><span data-stu-id="edae4-149">this behavior is corrected in the subsequent releases.</span></span> <span data-ttu-id="edae4-150">json.Net 反序列化程序的默认行为会更改日期/时间格式字符串，后续版本中已禁用该行为。</span><span class="sxs-lookup"><span data-stu-id="edae4-150">json.Net deserilizer's default behavior changes date/time format string, and it's disabled for the subsequent releases.</span></span> <span data-ttu-id="edae4-151">请使用 formatDateTime() 函数将日期/时间字符串的格式设置为 RFC 3389（如[本例](https://github.com/microsoft/AdaptiveCards/blob/db99ee07dadf317fe45e114a508e3de6e4325d0f/samples/Templates/Elements/Template.Functions.DateFunctions.json#L28)中所示），或者你可绕过 TIME/DATE 函数，只使用 formatDateTime()。</span><span class="sxs-lookup"><span data-stu-id="edae4-151">Please use formatDateTime() function to format the date/time string to RFC 3389 as seen in [this example](https://github.com/microsoft/AdaptiveCards/blob/db99ee07dadf317fe45e114a508e3de6e4325d0f/samples/Templates/Elements/Template.Functions.DateFunctions.json#L28), or you can bypass TIME/DATE functions, and just use formatDateTime().</span></span> <span data-ttu-id="edae4-152">要详细了解 formatDateTime()，请转到[此处](https://docs.microsoft.com/azure/bot-service/adaptive-expressions/adaptive-expressions-prebuilt-functions?view=azure-bot-service-4.0#date-and-time-functions)。</span><span class="sxs-lookup"><span data-stu-id="edae4-152">For more information on formatDateTime(), please go [here](https://docs.microsoft.com/azure/bot-service/adaptive-expressions/adaptive-expressions-prebuilt-functions?view=azure-bot-service-4.0#date-and-time-functions).</span></span>
