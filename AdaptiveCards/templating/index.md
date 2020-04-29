---
title: 模板化概述
author: matthidinger
ms.author: mahiding
ms.date: 07/29/2019
ms.topic: article
ms.openlocfilehash: ab3a3f335b52a06dbb2219159e15e5033e715ba1
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82136163"
---
# <a name="adaptive-cards-templating-preview"></a><span data-ttu-id="b5ec7-102">自适应卡片模板化（预览）</span><span class="sxs-lookup"><span data-stu-id="b5ec7-102">Adaptive Cards Templating (Preview)</span></span>

<span data-ttu-id="b5ec7-103">我们很高兴与大家一起预览用于**创建**、**重复使用**和**共享**自适应卡片的新工具。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-103">We're excited to share a preview of new tools that will help you **create**, **reuse**, and **share** Adaptive Cards.</span></span> 

> [!IMPORTANT] 
> 
> <span data-ttu-id="b5ec7-104">这些功能为**预览版，可能会更改**。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-104">These features are **in preview and subject to change**.</span></span> <span data-ttu-id="b5ec7-105">我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-105">Your feedback is not only welcome, but  critical to ensure we deliver the features **you** need.</span></span>

## <a name="how-can-templating-help-you"></a><span data-ttu-id="b5ec7-106">模板化对你有什么帮助？</span><span class="sxs-lookup"><span data-stu-id="b5ec7-106">How can templating help you?</span></span>

<span data-ttu-id="b5ec7-107">模板化可以将自适应卡片中的**数据**与**布局**分开。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-107">Templating enables the separation of **data** from the **layout** in an Adaptive Card.</span></span> 

### <a name="it-helps-design-a-card-once-and-then-populate-it-with-real-data"></a><span data-ttu-id="b5ec7-108">只需设计卡片一次，然后为其填充实际数据即可</span><span class="sxs-lookup"><span data-stu-id="b5ec7-108">It helps design a card once, and then populate it with real data</span></span>

<span data-ttu-id="b5ec7-109">目前不可能使用[自适应卡片设计器](https://adaptivecards.io/designer)来创建卡片并使用该 JSON 为有效负载填充**动态内容**。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-109">Today it's impossible to create a card using the [Adaptive Card Designer](https://adaptivecards.io/designer) and use that JSON to populate the payload with **dynamic content**.</span></span> <span data-ttu-id="b5ec7-110">为此，必须编写自定义代码来构建 JSON 字符串，或使用对象模型 SDK 来构建表示卡片的 OM 并将其序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-110">In order to achieve this you must write custom code to build a JSON string, or use the Object Model SDKs to build an OM representing your card and serialize it to JSON.</span></span> <span data-ttu-id="b5ec7-111">不管什么情况，设计器执行的是一次性单向操作，一旦将卡片设计转换为代码，就不容易在以后调整它。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-111">In either case the Designer is a one-time one-way operation and doesn't make it easy to tweak the card design later once you've converted it to code.</span></span>

### <a name="it-makes-transmissions-over-the-wire-smaller"></a><span data-ttu-id="b5ec7-112">降低通过网络传输的数据的大小</span><span class="sxs-lookup"><span data-stu-id="b5ec7-112">It makes transmissions over the wire smaller</span></span>

<span data-ttu-id="b5ec7-113">想象一下，如果可以**直接在客户端上**将模板和数据组合在一起，会是一种什么情景。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-113">Imagine a world where a template and data can be combined **directly on the client**.</span></span> <span data-ttu-id="b5ec7-114">这意味着，如果多次使用同一模板，或者要使用新数据来更新它，只需将新数据发送到设备即可，设备可以反复使用同一模板。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-114">This means if you use the same template multiple times, or want to update it with new data, you just need to send new data to the device and it can re-use the same template over and over.</span></span>

### <a name="it-helps-you-create-a-great-looking-card-from-just-the-data-you-provide"></a><span data-ttu-id="b5ec7-115">直接使用所提供的数据创建外观优美的卡片</span><span class="sxs-lookup"><span data-stu-id="b5ec7-115">It helps you create a great looking card from just the data you provide</span></span>

<span data-ttu-id="b5ec7-116">我们都认为自适应卡片很好，而如果你不需为需要显示给用户的所有内容编写自适应卡片，那不是好上加好吗？</span><span class="sxs-lookup"><span data-stu-id="b5ec7-116">We think Adaptive Cards are great, but what if you didn't have to write an Adaptive Card for everything you want to display to a user?</span></span> <span data-ttu-id="b5ec7-117">有了模板服务（在下面介绍），我们就可以让所有人都能贡献、发现和共享模板，不管使用什么类型的数据。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-117">With a template service (described below) we can create a world where everyone can contribute, discover, and share templates over any type of data.</span></span> 

<span data-ttu-id="b5ec7-118">可以在自己的项目内和组织中共享，也可以在整个 Internet 中共享。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-118">Share within your own projects, your organization, or with the entire internet.</span></span>

### <a name="ai-and-other-services-could-improve-user-experiences"></a><span data-ttu-id="b5ec7-119">AI 和其他服务可以改善用户体验</span><span class="sxs-lookup"><span data-stu-id="b5ec7-119">AI and other services could improve user experiences</span></span>

<span data-ttu-id="b5ec7-120">将数据与内容分开，AI 和其他服务就可以针对我们在卡片中看到的数据进行“推断”，提高用户工作效率，或者帮助我们找到所要的东西。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-120">By separating data from content it opens a door for AI and other services to  "reason" over the data in the cards we see and enhance user productivity or help us find things.</span></span>

## <a name="what-is-adaptive-cards-templating"></a><span data-ttu-id="b5ec7-121">什么是自适应卡片模板化？</span><span class="sxs-lookup"><span data-stu-id="b5ec7-121">What is Adaptive Cards Templating?</span></span>

<span data-ttu-id="b5ec7-122">它包含 3 个主要组件：</span><span class="sxs-lookup"><span data-stu-id="b5ec7-122">It's comprised of 3 major components:</span></span>

1. <span data-ttu-id="b5ec7-123">**[模板语言](language.md)** ：是用于创作模板的语法。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-123">The **[Template Language](language.md)** is the syntax used for authoring a template.</span></span> <span data-ttu-id="b5ec7-124">设计器甚至包含“示例数据”，让你在设计时预览模板。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-124">The Designer even lets you preview your templates at design time by including "sample data".</span></span>
2. <span data-ttu-id="b5ec7-125">**[模板化 SDK](sdk.md)** ：将存在于所有受支持的自适应卡片平台上。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-125">The **[Templating SDK's](sdk.md)** will exist on all supported Adaptive Card platforms.</span></span> <span data-ttu-id="b5ec7-126">可以通过这些 SDK 在后端或者直接在客户端为模板填充实际数据。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-126">These SDKs allow you to populate a template with real data, on the back-end or directly on the client.</span></span> 
3. <span data-ttu-id="b5ec7-127">**[模板服务](service.md)** ：是一项概念证明服务，允许任何人查找、贡献以及共享一组已知的模板。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-127">The **[Template Service](service.md)** is a proof-of-concept service that allows anyone to find, contribute to, and share a set of well-known templates.</span></span>

## <a name="template-language"></a><span data-ttu-id="b5ec7-128">模板语言</span><span class="sxs-lookup"><span data-stu-id="b5ec7-128">Template Language</span></span>

<span data-ttu-id="b5ec7-129">模板语言是用于创作自适应卡片模板的语法。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-129">The template langauge is the syntax used to author an Adaptive Card template.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="b5ec7-130">打开一个新的标签页，按以下示例操作</span><span class="sxs-lookup"><span data-stu-id="b5ec7-130">Follow along with the example below by opening up a new tab to</span></span>
>
> **https://adaptivecards.io/designer**
> 
> <span data-ttu-id="b5ec7-131">单击“预览模式”按钮，在设计模式和预览模式之间切换。 </span><span class="sxs-lookup"><span data-stu-id="b5ec7-131">Click the **Preview Mode** button to toggle between design-mode and preview-mode.</span></span>

![设计器屏幕截图](content/2019-08-01-13-58-27.png)

<span data-ttu-id="b5ec7-133">新更新的设计器添加了相关支持，允许用户创作模板，并提供用于在设计时预览卡片的**示例数据**。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-133">The newly updated Designer adds support for authoring templates and providing **Sample Data** to preview the card at design-time.</span></span>

<span data-ttu-id="b5ec7-134">请将以下示例粘贴到“卡片有效负载编辑器”窗格中： </span><span class="sxs-lookup"><span data-stu-id="b5ec7-134">Paste the example below into the **Card Payload Editor** pane:</span></span> 

<span data-ttu-id="b5ec7-135">**EmployeeCardTemplate.json**</span><span class="sxs-lookup"><span data-stu-id="b5ec7-135">**EmployeeCardTemplate.json**</span></span>

```json
{
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "ColumnSet",
            "style": "accent",
            "bleed": true,
            "columns": [
                {
                    "type": "Column",
                    "width": "auto",
                    "items": [
                        {
                            "type": "Image",
                            "url": "{photo}",
                            "altText": "Profile picture",
                            "size": "Small",
                            "style": "Person"
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "TextBlock",
                            "text": "Hi {name}!",
                            "size": "Medium"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Here's a bit about your org...",
                            "spacing": "None"
                        }
                    ]
                }
            ]
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: **{manager.name}**"
        },
        {
            "type": "TextBlock",
            "text": "Your peers are:"
        },
        {
            "type": "FactSet",
            "facts": [
                {
                    "$data": "{peers}",
                    "title": "{name}",
                    "value": "{title}"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="b5ec7-136">然后，将以下 JSON 数据粘贴到**示例数据编辑器**中。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-136">Then paste the JSON data below into the **Sample Data Editor**.</span></span> 

<span data-ttu-id="b5ec7-137">**示例数据**可以让你了解卡片在运行时（此时会传递实际数据）的具体外观。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-137">**Sample Data** helps you see exactly how your card will appear at runtime when passed actual data.</span></span>

<span data-ttu-id="b5ec7-138">**EmployeeData**</span><span class="sxs-lookup"><span data-stu-id="b5ec7-138">**EmployeeData**</span></span>

```json
{
    "name": "Matt",
    "photo": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
    "manager": {
        "name": "Thomas",
        "title": "PM Lead"
    },
    "peers": [
        {
            "name": "Lei",
            "title": "Sr Program Manager"
        },
        {
            "name": "Andrew",
            "title": "Program Manager II"
        },
        {
            "name": "Mary Anne",
            "title": "Program Manager"
        }
    ]
}
```

<span data-ttu-id="b5ec7-139">单击“预览模式”按钮。 </span><span class="sxs-lookup"><span data-stu-id="b5ec7-139">Click the **Preview Mode** button.</span></span> <span data-ttu-id="b5ec7-140">此时会看到卡片按上面提供的示例数据进行呈现。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-140">You should see the card render according to the sample data provided above.</span></span> <span data-ttu-id="b5ec7-141">可以随意调整示例数据，观察卡片进行实时更新。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-141">Feel free to make tweaks to the sample data and watch the card update in realtime.</span></span>

<span data-ttu-id="b5ec7-142">**祝贺**，你刚刚创作了你的第一个自适应卡片模板！</span><span class="sxs-lookup"><span data-stu-id="b5ec7-142">**Congratulations**, you just authored your first Adaptive Card Template!</span></span> <span data-ttu-id="b5ec7-143">接下来，让我们了解如何为模板填充实际数据。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-143">Next let's learn how to populate the template with real data.</span></span>

> <span data-ttu-id="b5ec7-144">详细了解[目标语言](language.md)</span><span class="sxs-lookup"><span data-stu-id="b5ec7-144">Learn more about the [template language](language.md)</span></span>

## <a name="sdk-support"></a><span data-ttu-id="b5ec7-145">SDK 支持</span><span class="sxs-lookup"><span data-stu-id="b5ec7-145">SDK support</span></span>

<span data-ttu-id="b5ec7-146">有了模板化 SDK，就可以为模板填充实际数据。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-146">The Templating SDKs make it possible to populate a template with real-data.</span></span>

> [!NOTE]
>
> <span data-ttu-id="b5ec7-147">在初始预览版中，我们只有有限的一组 SDK 可用。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-147">During the initial preview we only have a limited set of SDKs available.</span></span> <span data-ttu-id="b5ec7-148">正式发布后，每个受支持的自适应卡片平台都会有模板化库。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-148">When we release there will be templating libraries for every supported Adaptive Cards platform.</span></span>

<span data-ttu-id="b5ec7-149">平台</span><span class="sxs-lookup"><span data-stu-id="b5ec7-149">Platform</span></span> | <span data-ttu-id="b5ec7-150">安装</span><span class="sxs-lookup"><span data-stu-id="b5ec7-150">Install</span></span> | <span data-ttu-id="b5ec7-151">文档</span><span class="sxs-lookup"><span data-stu-id="b5ec7-151">Documentation</span></span>
--- | --- | ---
<span data-ttu-id="b5ec7-152">JavaScript</span><span class="sxs-lookup"><span data-stu-id="b5ec7-152">JavaScript</span></span> | `npm install adaptivecards-templating` | [<span data-ttu-id="b5ec7-153">文档</span><span class="sxs-lookup"><span data-stu-id="b5ec7-153">Documentation</span></span>](https://www.npmjs.com/package/adaptivecards-templating)
<span data-ttu-id="b5ec7-154">.NET</span><span class="sxs-lookup"><span data-stu-id="b5ec7-154">.NET</span></span> | `nuget install AdaptiveCards.Templating` | [<span data-ttu-id="b5ec7-155">文档</span><span class="sxs-lookup"><span data-stu-id="b5ec7-155">Documentation</span></span>](https://docs.microsoft.com/adaptive-cards/templating/sdk#net)

### <a name="javascript-example"></a><span data-ttu-id="b5ec7-156">JavaScript 示例</span><span class="sxs-lookup"><span data-stu-id="b5ec7-156">JavaScript Example</span></span>

<span data-ttu-id="b5ec7-157">以下 JavaScript 演示了将要用来为模板填充数据的常规模式。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-157">The JavaScript below shows the general pattern that will be used to populate a template with data.</span></span>

```js
var template = new ACData.Template({ 
    // EmployeeCardTemplate goes here
});

var dataContext = new ACData.EvaluationContext();
dataContext.$root = {
    // Data goes here
};

var card = template.expand(dataContext);
// Now you have an AdaptiveCard ready to render!
```

> <span data-ttu-id="b5ec7-158">详细了解[模板化 SDK](sdk.md)</span><span class="sxs-lookup"><span data-stu-id="b5ec7-158">Learn more about the [templating SDKs](sdk.md)</span></span>

## <a name="template-service"></a><span data-ttu-id="b5ec7-159">模板服务</span><span class="sxs-lookup"><span data-stu-id="b5ec7-159">Template Service</span></span>

<span data-ttu-id="b5ec7-160">自适应卡片模板服务是一项概念证明服务，允许任何人查找、贡献以及共享一组已知的模板。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-160">The Adaptive Cards Template Service is a proof-of-concept service that allows anyone to find, contribute to, and share a set of well-known templates.</span></span>

<span data-ttu-id="b5ec7-161">如果你要显示一些数据，但不想为其编写自定义的自适应卡片，则可使用此服务。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-161">It's useful if you want to display some data but don't want to bother writing a custom Adaptive Card for it.</span></span>

<span data-ttu-id="b5ec7-162">获取模板的 API 相当直观，但此服务实际上提供很多功能，包括分析数据并查找合适模板的功能。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-162">The API to get a template is straight-forward enough, but the service actually offers much more, including the ability to analyze your data and find a template that might work for you.</span></span>

`HTTP GET https://templates.adaptivecards.io/graph.microsoft.com/Profile.json`

<span data-ttu-id="b5ec7-163">所有模板都是存储在 GitHub 存储库中的平面 JSON 文件，因此任何人都可以为其贡献内容，就像为任何其他的开源代码贡献内容一样。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-163">All templates are flat JSON files stored in a GitHub repo so anyone can contribute to them like any other open source code.</span></span>

> <span data-ttu-id="b5ec7-164">详细了解[卡片模板服务](service.md)</span><span class="sxs-lookup"><span data-stu-id="b5ec7-164">Learn more about the [card template Service](service.md)</span></span>

## <a name="whats-next-and-sending-feedback"></a><span data-ttu-id="b5ec7-165">后续内容和发送反馈</span><span class="sxs-lookup"><span data-stu-id="b5ec7-165">What's next and sending feedback</span></span>

<span data-ttu-id="b5ec7-166">我们已经实现了模板化并将呈现方式与数据进行了分离，这离我们“建立一个生态系统，以常规且一致的方式交换卡片内容”的目标更进了一步。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-166">Templating and the separation of presentation from data takes us a whole lot closer toward our mission: "an ecosystem for exchanging card content in a common and consistent way".</span></span>

<span data-ttu-id="b5ec7-167">我们会尽快分享更多内容。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-167">We're eager to share more as soon as we can.</span></span> <span data-ttu-id="b5ec7-168">在此期间，请通过 [GitHub](https://github.com/microsoft/AdaptiveCards) 提供反馈，或者向 **[@MattHidinger](https://twitter.com/matthidinger)** / **#AdaptiveCards** 发送推文。</span><span class="sxs-lookup"><span data-stu-id="b5ec7-168">In the meantime please give feedback here, [GitHub](https://github.com/microsoft/AdaptiveCards), or Twitter **[@MattHidinger](https://twitter.com/matthidinger)**/**#AdaptiveCards**.</span></span> 
