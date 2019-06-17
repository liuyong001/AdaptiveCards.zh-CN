---
title: 自适应卡片概述
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 8d9e30d4e188a1f0a9d10a9a4821f78b9b3b2f57
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67134210"
---
# <a name="adaptive-cards-overview"></a><span data-ttu-id="d6a2c-102">自适应卡片概述</span><span class="sxs-lookup"><span data-stu-id="d6a2c-102">Adaptive Cards Overview</span></span> 

<span data-ttu-id="d6a2c-103">自适应卡片是一种开放的卡片交换格式，可以让开发人员通过常见且一致的方式交换 UI 内容。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-103">Adaptive Cards are an open card exchange format enabling developers to exchange UI content in a common and consistent way.</span></span>

<video controls width="100%" poster="./content/videoposter.png">
    <source src="https://adaptivecardsblob.blob.core.windows.net/assets/AdaptiveCardsOverviewVideo.mp4" type="video/mp4">
</video>

## <a name="how-they-work"></a><span data-ttu-id="d6a2c-104">工作原理</span><span class="sxs-lookup"><span data-stu-id="d6a2c-104">How they work</span></span>

<span data-ttu-id="d6a2c-105">[**卡片作者**](authoring-cards/getting-started.md)一文将卡片内容描述为简单的 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-105">[**Card Authors**](authoring-cards/getting-started.md) describe their content as a simple JSON object.</span></span> <span data-ttu-id="d6a2c-106">该内容随后可以在[**主机应用程序**](rendering-cards/getting-started.md)中以本机方式呈现，自动适应主机的外观。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-106">That content can then be rendered natively inside a [**Host Application**](rendering-cards/getting-started.md), automatically adapting to the look and feel of the Host.</span></span>

<span data-ttu-id="d6a2c-107">例如，Contoso 机器人可以通过 Bot Framework 创作一张自适应卡片。将该卡片发送到 Skype 时，它看起来就像一张 Skype 卡片。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-107">For example, Contoso Bot can author an Adaptive Card through the Bot Framework, and when delivered to Skype, it will look and feel like a Skype card.</span></span> <span data-ttu-id="d6a2c-108">将这个相同的有效负载发送到 Microsoft Teams 时，它看起来就像 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-108">When that same payload is sent to Microsoft Teams, it will look and feel like Microsoft Teams.</span></span> <span data-ttu-id="d6a2c-109">当更多的主机应用开始支持自适应卡片时，这个相同的有效负载会自动在这些应用程序中启用，但其外观就像完全是该应用原生的一样。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-109">As more host apps start to support Adaptive Cards, that same payload will automatically light up inside these applications, yet still feel entirely native to the app.</span></span>

<span data-ttu-id="d6a2c-110">这有利于用户，因为他们会感到一切都很熟悉。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-110">Users win because everything feels familiar.</span></span> <span data-ttu-id="d6a2c-111">这有利于主机应用，因为它们可以控制用户体验。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-111">Host apps win because they control the user experience.</span></span> <span data-ttu-id="d6a2c-112">这有利于卡片作者，因为他们不需任何额外的工作就可以推广其内容。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-112">And Card Authors win because their content gets broader reach without any additional work.</span></span>

## <a name="goals"></a><span data-ttu-id="d6a2c-113">目标</span><span class="sxs-lookup"><span data-stu-id="d6a2c-113">Goals</span></span> 

<span data-ttu-id="d6a2c-114">自适应卡片的目标是：</span><span class="sxs-lookup"><span data-stu-id="d6a2c-114">The goals for adaptive cards are:</span></span>

* <span data-ttu-id="d6a2c-115">**可移植** - 移植到任何应用、设备和 UI 框架</span><span class="sxs-lookup"><span data-stu-id="d6a2c-115">**Portable** - To any app, device, and UI framework</span></span>
* <span data-ttu-id="d6a2c-116">**开放** - 库和架构采取开源和共享的形式</span><span class="sxs-lookup"><span data-stu-id="d6a2c-116">**Open** - Libraries and schema are open source and shared</span></span>
* <span data-ttu-id="d6a2c-117">**低成本** - 易于定义，易于使用</span><span class="sxs-lookup"><span data-stu-id="d6a2c-117">**Low cost** - Easy to define, easy to consume</span></span>
* <span data-ttu-id="d6a2c-118">**表达性强** - 其目标是开发人员希望生成的长尾内容</span><span class="sxs-lookup"><span data-stu-id="d6a2c-118">**Expressive** - Targeted at the long tail of content that developers want to produce</span></span>
* <span data-ttu-id="d6a2c-119">**纯声明性** - 不需要代码，也不允许使用代码</span><span class="sxs-lookup"><span data-stu-id="d6a2c-119">**Purely declarative** - No code is needed or allowed</span></span>
* <span data-ttu-id="d6a2c-120">**自动调整样式** - 根据主机应用程序 UX 和品牌准则进行调整</span><span class="sxs-lookup"><span data-stu-id="d6a2c-120">**Automatically styled** - To the Host application UX and brand guidelines</span></span>

## <a name="for-card-authors"></a><span data-ttu-id="d6a2c-121">面向卡片作者</span><span class="sxs-lookup"><span data-stu-id="d6a2c-121">For Card Authors</span></span>
<span data-ttu-id="d6a2c-122">对卡片作者来说，自适应卡片具有以下优点：</span><span class="sxs-lookup"><span data-stu-id="d6a2c-122">Adaptive Cards are great for card authors:</span></span>

* <span data-ttu-id="d6a2c-123">**一种架构** - 只有一种格式，可以将创建卡片的成本降至最低，同时又可以尽量扩大能够使用该卡片的场所。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-123">**One schema** - You get a single format, minimizing the cost of creating a card and maximizing the number of places it can be used.</span></span>
* <span data-ttu-id="d6a2c-124">**更丰富的表达** - 内容可以与你要表达的意思更接近，因为你的表达方式更丰富。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-124">**Richer expression** - Your content can more closely align with want you want to say because you have a richer palette to paint with.</span></span>
* <span data-ttu-id="d6a2c-125">**广泛的覆盖面** - 内容将适用于更广泛的应用程序集，而你不需学习新架构。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-125">**Broad reach** - Your content will work across a broader set of applications without you having to learn new schemas.</span></span>
* <span data-ttu-id="d6a2c-126">**输入控件** - 卡片可以包含输入控件，用于从查看卡片的用户处收集信息。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-126">**Input controls** - Your card can include input controls for gathering information from the user that is viewing the card.</span></span>
* <span data-ttu-id="d6a2c-127">**更好的工具** - 开放的卡片生态系统意味着更好的可供所有人共享的工具。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-127">**Better tooling** - An open card ecosystem means better tooling that is shared by everyone.</span></span>

## <a name="for-experience-owners"></a><span data-ttu-id="d6a2c-128">面向体验所有者</span><span class="sxs-lookup"><span data-stu-id="d6a2c-128">For Experience Owners</span></span>
<span data-ttu-id="d6a2c-129">如果你是应用开发人员，希望探索第三方内容的生态系统，则会喜欢自适应卡片，原因在于：</span><span class="sxs-lookup"><span data-stu-id="d6a2c-129">If you are an app developer who wants to tap into an ecosystem of third-party content you will love Adaptive Cards because:</span></span>

* <span data-ttu-id="d6a2c-130">**一致的用户体验** - 可以保证为用户提供一致的体验，因为你拥有所呈现卡片的样式。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-130">**Consistent user experience** - You guarantee a consistent experience for your users, because you own the style of the rendered card.</span></span>
* <span data-ttu-id="d6a2c-131">**本机性能** - 可以获得本机性能，因为它直接以 UI 框架为目标。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-131">**Native performance** - You get native performance as it targets your UI framework directly.</span></span>
* <span data-ttu-id="d6a2c-132">**安全** - 内容在安全的有效负载中传送，因此不需将 UI 框架开放给原始的标记和脚本。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-132">**Safe** - Content is delivered in safe payloads so you don't have to open up your UI framework to raw markup and scripting.</span></span>
* <span data-ttu-id="d6a2c-133">**易于实现** - 获得现成的库以后，即可将其轻松集成到支持的任何平台上。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-133">**Easy to implement** - You get off the shelf libraries to easily integrate on any platform you support</span></span> 
* <span data-ttu-id="d6a2c-134">**免费文档** - 可以节省时间，因为不需创造、实现和记录专有架构。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-134">**Free documentation** - You save time because you don't have to invent, implement, and document a proprietary schema.</span></span>
* <span data-ttu-id="d6a2c-135">**共享工具** - 可以节省时间，因为不需创建自定义工具。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-135">**Shared tooling** - You save time because you don't have to create custom tooling.</span></span>

## <a name="core-design-principles"></a><span data-ttu-id="d6a2c-136">核心设计原则</span><span class="sxs-lookup"><span data-stu-id="d6a2c-136">Core Design Principles</span></span> 

<span data-ttu-id="d6a2c-137">自适应卡片遵循一系列[指导原则](resources/principles.md)，这些原则可以让设计保持正轨。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-137">Adaptive Cards are driven by a set of [guiding principles](resources/principles.md) that have been useful for keeping the design on track.</span></span> 

### <a name="semantic-instead-of-pixel-perfect"></a><span data-ttu-id="d6a2c-138">追求语义价值而非像素完美</span><span class="sxs-lookup"><span data-stu-id="d6a2c-138">Semantic instead of pixel-perfect</span></span>
<span data-ttu-id="d6a2c-139">我们一直致力于追求语义价值和概念，而不是单纯的像素完美布局。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-139">We have striven as much as possible for semantic values and concepts as opposed to pure pixel-perfect layout.</span></span> <span data-ttu-id="d6a2c-140">语义表达式的示例显示在颜色、大小和元素中，例如 FactSet 和 ImageSet。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-140">Examples of semantic expression show up in colors, sizes, and in elements like FactSet and ImageSet.</span></span> <span data-ttu-id="d6a2c-141">这样主机应用程序就可以在实际外观方面进行更好的决策。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-141">These all allow the host application to make better decisions about the actual look and feel.</span></span>

### <a name="card-authors-own-the-content-host-app-owns-the-look-and-feel"></a><span data-ttu-id="d6a2c-142">卡片作者拥有内容，主机应用拥有外观</span><span class="sxs-lookup"><span data-stu-id="d6a2c-142">Card Authors own the content, Host App owns the look and feel</span></span>
<span data-ttu-id="d6a2c-143">卡片作者拥有其所要表达的内容，而显示内容的应用程序则拥有卡片在应用程序上下文中呈现的外观。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-143">The card authors own what they want to say, but the application displaying it owns the look and feel of the card in the context of their application.</span></span>

### <a name="keep-it-simple-but-expressive"></a><span data-ttu-id="d6a2c-144">在保持简单的同时增强表达能力</span><span class="sxs-lookup"><span data-stu-id="d6a2c-144">Keep it simple, but expressive</span></span>
<span data-ttu-id="d6a2c-145">我们希望自适应卡片表达能力强且通用，但我们并不想要构建一个 UI 框架。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-145">We want Adaptive Cards to be expressive and general purpose, but we don't want to build a UI framework.</span></span>  <span data-ttu-id="d6a2c-146">我们的目标是创建一个“具有足够表达力”的中间层，这与 Markdown 是相同的，后者对于文档来说具有足够的表达力。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-146">The goal is to create an intermediate layer which is "expressive enough" in the same way Markdown is expressive enough for documents.</span></span>

<span data-ttu-id="d6a2c-147">Markdown 的目标也是在保持简单的同时增强表达能力，可以轻松地对文档内容进行一致的描述。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-147">By focusing on keeping it simple and expressive, Markdown created an easy and consistent description of document content.</span></span>  <span data-ttu-id="d6a2c-148">我们相信，自适应卡片同样可以通过简单但表达力强的方式来描述卡片内容。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-148">In the same way, we believe that Adaptive Cards can create a simple, expressive means of describing card content.</span></span>

### <a name="when-in-doubt-keep-it-out"></a><span data-ttu-id="d6a2c-149">疑则不用</span><span class="sxs-lookup"><span data-stu-id="d6a2c-149">When in doubt, keep it out</span></span>
<span data-ttu-id="d6a2c-150">如果对某样功能没有把握，可以稍后添加相关内容，不必忍受其中的错误。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-150">It is easier to add later then it is to live with a mistake.</span></span> <span data-ttu-id="d6a2c-151">如果我们发现自己在争论是否应添加某项内容，则可以选择暂时不用它。通常情况下，与其使用我们不希望支持的旧属性，不如以后再添加相关内容。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-151">If we found ourselves debating whether we should add something or not, we opted to leave it out.  It is always easier to add a property than to live with a legacy we wish we didn't have to support.</span></span>


## <a name="build-2018-session"></a><span data-ttu-id="d6a2c-152">Build 2018 会议</span><span class="sxs-lookup"><span data-stu-id="d6a2c-152">Build 2018 Session</span></span>

<span data-ttu-id="d6a2c-153">在 Build 2018 进行的以下研讨会介绍了自适应卡片在机器人、Cortana、Outlook 和 Windows 中的应用。</span><span class="sxs-lookup"><span data-stu-id="d6a2c-153">The following session at Build 2018 showcases Adaptive Cards in Bots, Cortana, Outlook, and Windows.</span></span> 

<iframe src="https://medius.studios.ms/Embed/Video/BRK2401?SFYT=true" width="960" height="540" allowFullScreen frameBorder="0"></iframe>
