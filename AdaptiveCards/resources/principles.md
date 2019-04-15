---
title: 动机和原理
author: matthidinger
ms.author: mahiding
ms.date: 5/14/2018
ms.topic: article
ms.openlocfilehash: 78fe44463c4ddb832ba0cc72d456b6d21518bac4
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553149"
---
# <a name="motivations-and-principles"></a><span data-ttu-id="9fa16-102">动机和原理</span><span class="sxs-lookup"><span data-stu-id="9fa16-102">Motivations and Principles</span></span>

<span data-ttu-id="9fa16-103">下面是动机和原理 govering 自适应卡格式的发展方式。</span><span class="sxs-lookup"><span data-stu-id="9fa16-103">Below are the motivations and principles govering the evolution of the Adaptive Card format.</span></span>

## <a name="motivations-behind-the-format"></a><span data-ttu-id="9fa16-104">格式背后的动机</span><span class="sxs-lookup"><span data-stu-id="9fa16-104">Motivations behind the format</span></span>

<span data-ttu-id="9fa16-105">在 2016 年初，Microsoft （包括 Outlook、 Windows 和 Bot Framework） 的多个团队来自，它们都想要的工具非常类似 （"卡"） 和每个已单独设计他们自己的解决方案：</span><span class="sxs-lookup"><span data-stu-id="9fa16-105">In early 2016, several teams at Microsoft (including Outlook, Windows and the Bot Framework) came to the realization that they all wanted something extremely similar ("cards") and that each of them were designing their own solutions independently:</span></span>

- <span data-ttu-id="9fa16-106">Windows 具有其自己的动态磁贴和通知格式</span><span class="sxs-lookup"><span data-stu-id="9fa16-106">Windows had its own Live Tiles and Notifications format</span></span>
-  <span data-ttu-id="9fa16-107">智能机器人应用程序框架，它使用一组发送智能机器人应用程序消息时，开发人员可以选择从预定义的卡模板</span><span class="sxs-lookup"><span data-stu-id="9fa16-107">The Bot framework was using a set of predefined card templates developers could choose from when sending Bot messages</span></span>
- <span data-ttu-id="9fa16-108">Outlook 已使用其自己 MessageCard 的格式，对其可操作邮件功能</span><span class="sxs-lookup"><span data-stu-id="9fa16-108">Outlook was using its own MessageCard format for its Actionable Messages feature</span></span>

<span data-ttu-id="9fa16-109">在同一时间，如行、 FaceBook Messenger、 Slack 等其他平台定义其自身的、 专有"卡"格式。</span><span class="sxs-lookup"><span data-stu-id="9fa16-109">At the same time, other platforms such as LINE, FaceBook Messenger, Slack and more were defining their own, proprietary "card" format.</span></span> <span data-ttu-id="9fa16-110">因此几个 Microsoft 员工收集和启动为了定义单个，打开卡格式和了一组 Sdk 的：</span><span class="sxs-lookup"><span data-stu-id="9fa16-110">So a few Microsoft employees gathered up and started an effort to define a single, open card format and a set of SDKs that:</span></span>

- <span data-ttu-id="9fa16-111">将促进卡主机之间的交换</span><span class="sxs-lookup"><span data-stu-id="9fa16-111">Would facilitate the interchange of cards between hosts</span></span>
- <span data-ttu-id="9fa16-112">将允许每个主机保留的控制力的卡，以确保 visual 一致性</span><span class="sxs-lookup"><span data-stu-id="9fa16-112">Would allow each host to keep control over the styling of cards to ensure visual consistency</span></span>
- <span data-ttu-id="9fa16-113">可以轻松为主机应用程序，以显示具有通过随时可用的 Sdk 的最小精力卡</span><span class="sxs-lookup"><span data-stu-id="9fa16-113">Would make it easy for a host application to display cards with minimum effort via ready-to-use SDKs</span></span>
- <span data-ttu-id="9fa16-114">并且还会向第三方提供值并最终获得广泛的行业</span><span class="sxs-lookup"><span data-stu-id="9fa16-114">And that would also provide value to third parties and eventually get adopted widely by the industry</span></span>

## <a name="principles-governing-adaptive-cards"></a><span data-ttu-id="9fa16-115">用于控制自适应卡的原则</span><span class="sxs-lookup"><span data-stu-id="9fa16-115">Principles governing Adaptive Cards</span></span>

1.  <span data-ttu-id="9fa16-116">**自适应卡_简单_并_声明性_卡格式**</span><span class="sxs-lookup"><span data-stu-id="9fa16-116">**Adaptive Card is a _simple_ and _declarative_ card format**</span></span>

    1.  <span data-ttu-id="9fa16-117">但并不作为 HTML 或 XAML 替换/替代方法</span><span class="sxs-lookup"><span data-stu-id="9fa16-117">It is not meant as an HTML or XAML replacement/alternative</span></span>
    2.  <span data-ttu-id="9fa16-118">没有**没有"代码背后"** 使用自适应卡</span><span class="sxs-lookup"><span data-stu-id="9fa16-118">There is **no "code behind"** with Adaptive Cards</span></span>
        1. <span data-ttu-id="9fa16-119">卡作者不能使用其有效负载，嵌入自定义/任意代码，因此自适应卡主机永远不需要运行第三方代码</span><span class="sxs-lookup"><span data-stu-id="9fa16-119">Card authors cannot embed custom/arbitrary code with their payloads, and as a result an Adaptive Card host never needs to run third party code</span></span>
        2. <span data-ttu-id="9fa16-120">仅通过声明性标记来实现动态性和交互性</span><span class="sxs-lookup"><span data-stu-id="9fa16-120">Dynamism and interactivity are achieved solely via declarative markup</span></span>
    3.  <span data-ttu-id="9fa16-121">这可确保生成适用于新的平台的自适应卡 SDK 所必需的工作保持合理</span><span class="sxs-lookup"><span data-stu-id="9fa16-121">This ensures that the effort necessary to build an Adaptive Card SDK for a new platform remains reasonable</span></span>

2.  <span data-ttu-id="9fa16-122">**自适应卡格式无法施加任何特定的基础技术的使用**</span><span class="sxs-lookup"><span data-stu-id="9fa16-122">**The Adaptive Card format can't impose the use of any particular underlying technology**</span></span>

    1.  <span data-ttu-id="9fa16-123">自适应卡格式不依赖于 JavaScript， C#，Python 或任何其他语言</span><span class="sxs-lookup"><span data-stu-id="9fa16-123">The Adaptive Card format does not rely on JavaScript, C#, Python or any other language</span></span>
    2.  <span data-ttu-id="9fa16-124">同样不会依赖于 HTML 或 XAML 或任何其他图形/UI 框架</span><span class="sxs-lookup"><span data-stu-id="9fa16-124">Similarly it doesn't rely on HTML or XAML or any other graphic/UI framework</span></span>
    3.  <span data-ttu-id="9fa16-125">这样一来，自适应卡可以在本机上呈现为任何平台，只要呈现器存在</span><span class="sxs-lookup"><span data-stu-id="9fa16-125">This way, Adaptive Cards can be rendered natively on any platform for as long as a renderer exists</span></span>

3.  <span data-ttu-id="9fa16-126">**自适应卡格式是_共享属性_**</span><span class="sxs-lookup"><span data-stu-id="9fa16-126">**The Adaptive Card format is a _shared property_**</span></span>

    1.  <span data-ttu-id="9fa16-127">以及其 Sdk 的格式是为开放源和驱动其发展社区</span><span class="sxs-lookup"><span data-stu-id="9fa16-127">Along with its SDKs, the format is to be open source and its evolution community driven</span></span>
    2.  <span data-ttu-id="9fa16-128">格式因此不负责也不会由任何一个团队</span><span class="sxs-lookup"><span data-stu-id="9fa16-128">The format is therefore not owned nor driven by any one team</span></span>

4.  <span data-ttu-id="9fa16-129">**自适应卡格式不是"只是为 Microsoft 的使用"设计**</span><span class="sxs-lookup"><span data-stu-id="9fa16-129">**The Adaptive Card format is not designed "just for Microsoft's use"**</span></span>

    1.  <span data-ttu-id="9fa16-130">而这被为了满足多种应用程序的需要和用例</span><span class="sxs-lookup"><span data-stu-id="9fa16-130">Instead it is designed to suit the needs of a wide variety of applications and use cases</span></span>

5.  <span data-ttu-id="9fa16-131">**_自适应卡 Working Group_控制格式的演变**</span><span class="sxs-lookup"><span data-stu-id="9fa16-131">**The _Adaptive Card Working Group_ governs the evolution of the format**</span></span>

    1.  <span data-ttu-id="9fa16-132">此工作组组成一组有成功的格式中都很深认识的 Microsoft 员工</span><span class="sxs-lookup"><span data-stu-id="9fa16-132">This working group is comprised of a set of Microsoft employees that are all deeply involved in the success of the format</span></span>
    2.  <span data-ttu-id="9fa16-133">工作组组织召开每周会议 （当前在星期一） 期间哪项功能的方案是已审阅和打开的问题是讨论和会审和跟踪对 vNext 工作项的整体进度</span><span class="sxs-lookup"><span data-stu-id="9fa16-133">The Working Group conducts weekly meetings (currently on Monday) during which feature proposals are reviewed, open issues are discussed and triaged and overall progress on vNext work items is tracked</span></span>
    3.  <span data-ttu-id="9fa16-134">使用组使用大型社区，包括内部的 Microsoft 团队的反馈来确定格式的不断发展</span><span class="sxs-lookup"><span data-stu-id="9fa16-134">The Working Group uses feedback from the community at large, including internal Microsoft teams, to decide how the format evolves</span></span>
        1. <span data-ttu-id="9fa16-135">任何人都可以加入工作组介绍如何在 GitHub （见下文） 中打开问题</span><span class="sxs-lookup"><span data-stu-id="9fa16-135">Anyone can participate in the working group through opening issues in GitHub (see below)</span></span>
        2. <span data-ttu-id="9fa16-136">实际使用的自适应卡 framework （作为主机或作为卡作者） 中取得 root 权限的问题/功能请求格式的前景，才能充分发挥</span><span class="sxs-lookup"><span data-stu-id="9fa16-136">Issues/feature requests rooted in actual usage of the Adaptive Cards framework (either as a host or as a card author) have the most impact on the future of the format</span></span>
    4.  <span data-ttu-id="9fa16-137">待批准建议的新功能的工作组：</span><span class="sxs-lookup"><span data-stu-id="9fa16-137">To be approved by the Working Group, proposed new features:</span></span>
        1. <span data-ttu-id="9fa16-138">必须根据真实用例作出</span><span class="sxs-lookup"><span data-stu-id="9fa16-138">Must be justified by real life use cases</span></span>
        2. <span data-ttu-id="9fa16-139">必须具有的功能规范</span><span class="sxs-lookup"><span data-stu-id="9fa16-139">Must have a functional specification</span></span>
    5.  <span data-ttu-id="9fa16-140">已批准的新功能添加到积压工作，然后将其视为 vnext</span><span class="sxs-lookup"><span data-stu-id="9fa16-140">Approved new feature are added to the backlog and considered for vNext</span></span>
        1. <span data-ttu-id="9fa16-141">用于优化新功能的条件包括的功能使的方案，其复杂性/可维护性和的详细信息的广度</span><span class="sxs-lookup"><span data-stu-id="9fa16-141">The criteria used to prioritize new features include the breadth of scenarios the feature enables, its complexity/maintainability and more</span></span>
        2. <span data-ttu-id="9fa16-142">如有疑问，保持其状态 ！</span><span class="sxs-lookup"><span data-stu-id="9fa16-142">When in doubt, keep it out!</span></span> <span data-ttu-id="9fa16-143">它是要简单得多比以永久生存，使用了错误的操作的更高版本引入了一个设计良好的功能。</span><span class="sxs-lookup"><span data-stu-id="9fa16-143">It's a lot easier to introduce a well designed feature later than to live with a mistake forever.</span></span>
    6.  <span data-ttu-id="9fa16-144">在所有受支持的 Sdk 中实现的所有新功能</span><span class="sxs-lookup"><span data-stu-id="9fa16-144">All new features are implemented in all supported SDKs</span></span>
    7.  <span data-ttu-id="9fa16-145">记录了所有新功能并与发布的 samples 文件夹中的测试卡</span><span class="sxs-lookup"><span data-stu-id="9fa16-145">All new features are documented and associated with a test card published in the samples folder</span></span>
    8.  <span data-ttu-id="9fa16-146">新版本的格式和 Sdk 经过 beta 阶段</span><span class="sxs-lookup"><span data-stu-id="9fa16-146">New versions of the format and SDKs go through a beta phase</span></span>
    9.  <span data-ttu-id="9fa16-147">自适应卡架构和 SDK 版本的发布计划驱动的质量，而非日期</span><span class="sxs-lookup"><span data-stu-id="9fa16-147">The release schedule for Adaptive Card schema and SDK versions is driven by quality, not date</span></span>

6.  <span data-ttu-id="9fa16-148">**互操作性**</span><span class="sxs-lookup"><span data-stu-id="9fa16-148">**Interoperability**</span></span>
    1.  <span data-ttu-id="9fa16-149">卡编写根据有案可稽的格式 （例如未使用的任何特定于宿主的扩展） 将在任何自适应卡支持的主机中正确呈现</span><span class="sxs-lookup"><span data-stu-id="9fa16-149">Cards authored in accordance with the documented format (e.g. not using any host-specific extensions) will render properly in any Adaptive Card-capable host</span></span>
    2.  <span data-ttu-id="9fa16-150">此原则的唯一例外是：</span><span class="sxs-lookup"><span data-stu-id="9fa16-150">The only exceptions to this principles are:</span></span>
        1.  <span data-ttu-id="9fa16-151">一些主机可能不允许交互，因此不会呈现输入，也不操作</span><span class="sxs-lookup"><span data-stu-id="9fa16-151">Some hosts might not allow interactivity, and will therefore not render inputs nor actions</span></span>
        2.  <span data-ttu-id="9fa16-152">Action.Submit 操作的执行是自行决定的主机，并不是所有主机一定正确地都处理所有 Action.Submit 负载。</span><span class="sxs-lookup"><span data-stu-id="9fa16-152">Execution of Action.Submit actions is at the discretion of the host, and not all hosts will necessarily properly handle all Action.Submit payloads.</span></span> <span data-ttu-id="9fa16-153">此外，，某些主机可能不会支持 Action.Submit</span><span class="sxs-lookup"><span data-stu-id="9fa16-153">Furthermore, some hosts might not support Action.Submit at all</span></span>

7.  <span data-ttu-id="9fa16-154">**格式必须是可扩展**</span><span class="sxs-lookup"><span data-stu-id="9fa16-154">**The format needs to be extensible**</span></span>

    1.  <span data-ttu-id="9fa16-155">主机应具有自由地添加对自定义元素或对超出的格式是支持的自定义操作的支持</span><span class="sxs-lookup"><span data-stu-id="9fa16-155">Hosts should have the freedom of adding support for custom elements or custom actions that go beyond what the format is capable of</span></span>
    2.  <span data-ttu-id="9fa16-156">这是特别重要的操作，因为不同的主机不一定支持同一组操作</span><span class="sxs-lookup"><span data-stu-id="9fa16-156">This is particularly important for actions, as various hosts don't necessarily support the same set of actions</span></span>
    3.  <span data-ttu-id="9fa16-157">这些附加选项是自行决定主机</span><span class="sxs-lookup"><span data-stu-id="9fa16-157">These additions are at the discretion of the host</span></span>
        1. <span data-ttu-id="9fa16-158">它们不是*de facto*添加到自适应卡规范</span><span class="sxs-lookup"><span data-stu-id="9fa16-158">They are not a *de facto* addition to the Adaptive Card specification</span></span>
        2. <span data-ttu-id="9fa16-159">在这种情况下，它们使使用它们的有效负载与主流的自适应卡格式不兼容</span><span class="sxs-lookup"><span data-stu-id="9fa16-159">As such, they make a payload that uses them incompatible with the mainstream Adaptive Card format</span></span>
        3. <span data-ttu-id="9fa16-160">但是，它们可以是提供给工作组和所述入点 #5 作为格式的未来版本的新功能建议</span><span class="sxs-lookup"><span data-stu-id="9fa16-160">They can however be presented to the Working Group and proposed as new features for a future version of the format, as described in point #5</span></span>

8.  <span data-ttu-id="9fa16-161">**卡作者拥有内容、 托管应用程序拥有外观和感觉**</span><span class="sxs-lookup"><span data-stu-id="9fa16-161">**Card authors own the content, host apps own the look and feel**</span></span>

    1.  <span data-ttu-id="9fa16-162">主机应用施加其样式，因此卡看起来和感觉像它们是本机应用程序的体验的扩展</span><span class="sxs-lookup"><span data-stu-id="9fa16-162">Host apps impose their styling so cards look and feel like they are native extensions of the app's experience</span></span>
    2.  <span data-ttu-id="9fa16-163">卡作者仍可以指定样式，但只能通过语义的颜色、 大小等表达式。</span><span class="sxs-lookup"><span data-stu-id="9fa16-163">Card authors can still specify styling, but only via semantic expressions of colors, sizes, etc.</span></span>

9.  <span data-ttu-id="9fa16-164">**Sdk 将提供针对最流行的开发人员平台**</span><span class="sxs-lookup"><span data-stu-id="9fa16-164">**SDKs will be provided for the most popular developer platforms**</span></span>

    1.  <span data-ttu-id="9fa16-165">Sdk 可以轻松地呈现中的任何主机的自适应卡负载</span><span class="sxs-lookup"><span data-stu-id="9fa16-165">SDKs make it easy to render Adaptive Card payloads in any host</span></span>
    2.  <span data-ttu-id="9fa16-166">这可确保的门槛是低可能会同时适用于第三方开发人员和 Microsoft 团队</span><span class="sxs-lookup"><span data-stu-id="9fa16-166">This ensures the barrier to entry is as low as can be both for third party developers and Microsoft teams</span></span>
