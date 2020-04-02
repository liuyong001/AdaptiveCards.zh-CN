---
title: 动因和原则
author: matthidinger
ms.author: mahiding
ms.date: 5/14/2018
ms.topic: article
ms.openlocfilehash: 243ad63fc585c5afc3fa396b86ff6261e8a7ee93
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454810"
---
# <a name="motivations-and-principles"></a><span data-ttu-id="c00cb-102">动因和原则</span><span class="sxs-lookup"><span data-stu-id="c00cb-102">Motivations and Principles</span></span>

<span data-ttu-id="c00cb-103">下面是自适应卡片格式演变历程背后的动因和原则。</span><span class="sxs-lookup"><span data-stu-id="c00cb-103">Below are the motivations and principles govering the evolution of the Adaptive Card format.</span></span>

## <a name="motivations-behind-the-format"></a><span data-ttu-id="c00cb-104">格式背后的动因</span><span class="sxs-lookup"><span data-stu-id="c00cb-104">Motivations behind the format</span></span>

<span data-ttu-id="c00cb-105">2016 年初，Microsoft 的数个团队（包括 Outlook、Windows 和 Bot Framework）认识到，他们各自在为自己需要的某种功能（“卡片”）独立地设计解决方案，但他们需要的功能极为相似：</span><span class="sxs-lookup"><span data-stu-id="c00cb-105">In early 2016, several teams at Microsoft (including Outlook, Windows and the Bot Framework) came to the realization that they all wanted something extremely similar ("cards") and that each of them were designing their own solutions independently:</span></span>

- <span data-ttu-id="c00cb-106">Windows 当时已有自己的动态磁贴和通知格式</span><span class="sxs-lookup"><span data-stu-id="c00cb-106">Windows had its own Live Tiles and Notifications format</span></span>
-  <span data-ttu-id="c00cb-107">Bot Framework 使用一组预定义的卡片模板，供开发人员在发送机器人消息时从中进行选择</span><span class="sxs-lookup"><span data-stu-id="c00cb-107">The Bot framework was using a set of predefined card templates developers could choose from when sending Bot messages</span></span>
- <span data-ttu-id="c00cb-108">Outlook 为其可操作邮件功能使用自己的 MessageCard 格式</span><span class="sxs-lookup"><span data-stu-id="c00cb-108">Outlook was using its own MessageCard format for its Actionable Messages feature</span></span>

<span data-ttu-id="c00cb-109">同时，其他平台（例如 LINE、FaceBook Messenger、Slack 等）也在定义各自的专用“卡片”格式。</span><span class="sxs-lookup"><span data-stu-id="c00cb-109">At the same time, other platforms such as LINE, FaceBook Messenger, Slack and more were defining their own, proprietary "card" format.</span></span> <span data-ttu-id="c00cb-110">因此，一些 Microsoft 员工开始合作，共同定义一个符合以下条件的单一开放式卡片格式和一组 SDK：</span><span class="sxs-lookup"><span data-stu-id="c00cb-110">So a few Microsoft employees gathered up and started an effort to define a single, open card format and a set of SDKs that:</span></span>

- <span data-ttu-id="c00cb-111">方便在主机之间交换卡片</span><span class="sxs-lookup"><span data-stu-id="c00cb-111">Would facilitate the interchange of cards between hosts</span></span>
- <span data-ttu-id="c00cb-112">允许每个主机控制卡片的样式设置，确保视觉一致性</span><span class="sxs-lookup"><span data-stu-id="c00cb-112">Would allow each host to keep control over the styling of cards to ensure visual consistency</span></span>
- <span data-ttu-id="c00cb-113">尽量方便主机应用程序通过易用的 SDK 轻松显示卡片</span><span class="sxs-lookup"><span data-stu-id="c00cb-113">Would make it easy for a host application to display cards with minimum effort via ready-to-use SDKs</span></span>
- <span data-ttu-id="c00cb-114">此外还要方便第三方使用，这样才能最终被业界广泛采用</span><span class="sxs-lookup"><span data-stu-id="c00cb-114">And that would also provide value to third parties and eventually get adopted widely by the industry</span></span>

## <a name="principles-governing-adaptive-cards"></a><span data-ttu-id="c00cb-115">自适应卡片背后的原则</span><span class="sxs-lookup"><span data-stu-id="c00cb-115">Principles governing Adaptive Cards</span></span>

1.  <span data-ttu-id="c00cb-116">**自适应卡片是一种简单的声明性卡片格式**  </span><span class="sxs-lookup"><span data-stu-id="c00cb-116">**Adaptive Card is a _simple_ and _declarative_ card format**</span></span>

    1.  <span data-ttu-id="c00cb-117">它不是用来替代 HTML 或 XAML，也不充当其备用选项</span><span class="sxs-lookup"><span data-stu-id="c00cb-117">It is not meant as an HTML or XAML replacement/alternative</span></span>
    2.  <span data-ttu-id="c00cb-118">自适应卡片**没有“代码隐藏”**</span><span class="sxs-lookup"><span data-stu-id="c00cb-118">There is **no "code behind"** with Adaptive Cards</span></span>
        1. <span data-ttu-id="c00cb-119">卡片作者不能在有效负载中嵌入自定义代码/任意代码，因此自适应卡片主机不需运行第三方代码</span><span class="sxs-lookup"><span data-stu-id="c00cb-119">Card authors cannot embed custom/arbitrary code with their payloads, and as a result an Adaptive Card host never needs to run third party code</span></span>
        2. <span data-ttu-id="c00cb-120">完全通过声明性标记来实现动态性和交互性</span><span class="sxs-lookup"><span data-stu-id="c00cb-120">Dynamism and interactivity are achieved solely via declarative markup</span></span>
    3.  <span data-ttu-id="c00cb-121">这样可确保不用太费劲即可为新平台构建自适应卡片 SDK</span><span class="sxs-lookup"><span data-stu-id="c00cb-121">This ensures that the effort necessary to build an Adaptive Card SDK for a new platform remains reasonable</span></span>

2.  <span data-ttu-id="c00cb-122">**自适应卡片格式不能强制要求使用任何特定的基础技术**</span><span class="sxs-lookup"><span data-stu-id="c00cb-122">**The Adaptive Card format can't impose the use of any particular underlying technology**</span></span>

    1.  <span data-ttu-id="c00cb-123">自适应卡片格式不依赖于 JavaScript、C#、Python 或任何其他语言</span><span class="sxs-lookup"><span data-stu-id="c00cb-123">The Adaptive Card format does not rely on JavaScript, C#, Python or any other language</span></span>
    2.  <span data-ttu-id="c00cb-124">同样，它不依赖于 HTML、XAML 或任何其他图形/UI 框架</span><span class="sxs-lookup"><span data-stu-id="c00cb-124">Similarly it doesn't rely on HTML or XAML or any other graphic/UI framework</span></span>
    3.  <span data-ttu-id="c00cb-125">这样，只要存在呈现器，自适应卡片就可以在任何平台上进行本机呈现</span><span class="sxs-lookup"><span data-stu-id="c00cb-125">This way, Adaptive Cards can be rendered natively on any platform for as long as a renderer exists</span></span>

3.  <span data-ttu-id="c00cb-126">**自适应卡片格式是一种共享属性** </span><span class="sxs-lookup"><span data-stu-id="c00cb-126">**The Adaptive Card format is a _shared property_**</span></span>

    1.  <span data-ttu-id="c00cb-127">此格式及其 SDK 都是开源的，由社区推动其发展</span><span class="sxs-lookup"><span data-stu-id="c00cb-127">Along with its SDKs, the format is to be open source and its evolution community driven</span></span>
    2.  <span data-ttu-id="c00cb-128">因此，此格式不由任何单一团队拥有，其发展不由任何单一团队推动</span><span class="sxs-lookup"><span data-stu-id="c00cb-128">The format is therefore not owned nor driven by any one team</span></span>

4.  <span data-ttu-id="c00cb-129">**自适应卡片格式不是“专为 Microsoft”而设计**</span><span class="sxs-lookup"><span data-stu-id="c00cb-129">**The Adaptive Card format is not designed "just for Microsoft's use"**</span></span>

    1.  <span data-ttu-id="c00cb-130">相反，我们在设计它时已考虑到要让它满足各种应用程序和用例的需求</span><span class="sxs-lookup"><span data-stu-id="c00cb-130">Instead it is designed to suit the needs of a wide variety of applications and use cases</span></span>

5.  <span data-ttu-id="c00cb-131"> **自适应卡片工作组负责控制格式的演变**</span><span class="sxs-lookup"><span data-stu-id="c00cb-131">**The _Adaptive Card Working Group_ governs the evolution of the format**</span></span>

    1.  <span data-ttu-id="c00cb-132">此工作组的成员是许多对格式的成功做出了很大贡献的 Microsoft 员工</span><span class="sxs-lookup"><span data-stu-id="c00cb-132">This working group is comprised of a set of Microsoft employees that are all deeply involved in the success of the format</span></span>
    2.  <span data-ttu-id="c00cb-133">工作组每周召开一次会议（目前的会议时间为周一），审核功能建议、讨论和会审未决问题，并会对 vNext 工作项目的总体进展进行跟踪</span><span class="sxs-lookup"><span data-stu-id="c00cb-133">The Working Group conducts weekly meetings (currently on Monday) during which feature proposals are reviewed, open issues are discussed and triaged and overall progress on vNext work items is tracked</span></span>
    3.  <span data-ttu-id="c00cb-134">工作组会根据社区（包括 Microsoft 内部团队）的普遍反馈来决定格式如何改进</span><span class="sxs-lookup"><span data-stu-id="c00cb-134">The Working Group uses feedback from the community at large, including internal Microsoft teams, to decide how the format evolves</span></span>
        1. <span data-ttu-id="c00cb-135">任何人都可以在 GitHub 中提出问题，以这种方式参与工作组的工作（见下）</span><span class="sxs-lookup"><span data-stu-id="c00cb-135">Anyone can participate in the working group through opening issues in GitHub (see below)</span></span>
        2. <span data-ttu-id="c00cb-136">植根于自适应卡片框架的实际使用的问题/功能请求（不管你是以主机用户身份还是以卡片作者身份提出此类请求）将会对格式的未来造成最深远的影响</span><span class="sxs-lookup"><span data-stu-id="c00cb-136">Issues/feature requests rooted in actual usage of the Adaptive Cards framework (either as a host or as a card author) have the most impact on the future of the format</span></span>
    4.  <span data-ttu-id="c00cb-137">若要获得工作组的批准，建议的新功能要符合以下条件：</span><span class="sxs-lookup"><span data-stu-id="c00cb-137">To be approved by the Working Group, proposed new features:</span></span>
        1. <span data-ttu-id="c00cb-138">必须满足实际使用需求</span><span class="sxs-lookup"><span data-stu-id="c00cb-138">Must be justified by real life use cases</span></span>
        2. <span data-ttu-id="c00cb-139">必须有一个功能规范</span><span class="sxs-lookup"><span data-stu-id="c00cb-139">Must have a functional specification</span></span>
    5.  <span data-ttu-id="c00cb-140">批准的新功能会添加到待处理工作中，考虑用于 vNext</span><span class="sxs-lookup"><span data-stu-id="c00cb-140">Approved new feature are added to the backlog and considered for vNext</span></span>
        1. <span data-ttu-id="c00cb-141">用于确定新功能优先级的标准包括：此功能支持的方案的广泛性、其复杂性/可维护性，等等</span><span class="sxs-lookup"><span data-stu-id="c00cb-141">The criteria used to prioritize new features include the breadth of scenarios the feature enables, its complexity/maintainability and more</span></span>
        2. <span data-ttu-id="c00cb-142">疑则不用！</span><span class="sxs-lookup"><span data-stu-id="c00cb-142">When in doubt, keep it out!</span></span> <span data-ttu-id="c00cb-143">与其因为贸然行动而引入难以纠正的错误，不如晚一点推出设计完善的功能。</span><span class="sxs-lookup"><span data-stu-id="c00cb-143">It's a lot easier to introduce a well designed feature later than to live with a mistake forever.</span></span>
    6.  <span data-ttu-id="c00cb-144">所有新功能都会在所有受支持的 SDK 中实施</span><span class="sxs-lookup"><span data-stu-id="c00cb-144">All new features are implemented in all supported SDKs</span></span>
    7.  <span data-ttu-id="c00cb-145">所有新功能都会进行记录，并与在 Samples 文件夹中发布的测试卡片相关联</span><span class="sxs-lookup"><span data-stu-id="c00cb-145">All new features are documented and associated with a test card published in the samples folder</span></span>
    8.  <span data-ttu-id="c00cb-146">新版格式和 SDK 都会经历一个 Beta 阶段</span><span class="sxs-lookup"><span data-stu-id="c00cb-146">New versions of the format and SDKs go through a beta phase</span></span>
    9.  <span data-ttu-id="c00cb-147">自适应卡片架构和 SDK 版本的发布计划取决于质量而不是日期</span><span class="sxs-lookup"><span data-stu-id="c00cb-147">The release schedule for Adaptive Card schema and SDK versions is driven by quality, not date</span></span>

6.  <span data-ttu-id="c00cb-148">**互操作性**</span><span class="sxs-lookup"><span data-stu-id="c00cb-148">**Interoperability**</span></span>
    1.  <span data-ttu-id="c00cb-149">遵循记录的格式（例如，不使用任何特定于主机的扩展）创作的卡片可以在任何支持自适应卡片的主机中正确呈现</span><span class="sxs-lookup"><span data-stu-id="c00cb-149">Cards authored in accordance with the documented format (e.g. not using any host-specific extensions) will render properly in any Adaptive Card-capable host</span></span>
    2.  <span data-ttu-id="c00cb-150">此原则的唯一例外是：</span><span class="sxs-lookup"><span data-stu-id="c00cb-150">The only exceptions to this principles are:</span></span>
        1.  <span data-ttu-id="c00cb-151">某些主机可能不允许交互操作，因此不呈现输入和操作</span><span class="sxs-lookup"><span data-stu-id="c00cb-151">Some hosts might not allow interactivity, and will therefore not render inputs nor actions</span></span>
        2.  <span data-ttu-id="c00cb-152">是否执行 Action.Submit 操作取决于主机，并非所有主机都必然能够正确处理所有 Action.Submit 有效负载。</span><span class="sxs-lookup"><span data-stu-id="c00cb-152">Execution of Action.Submit actions is at the discretion of the host, and not all hosts will necessarily properly handle all Action.Submit payloads.</span></span> <span data-ttu-id="c00cb-153">另外，某些主机可能根本就不支持 Action.Submit</span><span class="sxs-lookup"><span data-stu-id="c00cb-153">Furthermore, some hosts might not support Action.Submit at all</span></span>

7.  <span data-ttu-id="c00cb-154">**格式必须能够扩展**</span><span class="sxs-lookup"><span data-stu-id="c00cb-154">**The format needs to be extensible**</span></span>

    1.  <span data-ttu-id="c00cb-155">主机应该能够自由地添加对自定义元素或自定义操作的支持，以便实现格式未提供的功能</span><span class="sxs-lookup"><span data-stu-id="c00cb-155">Hosts should have the freedom of adding support for custom elements or custom actions that go beyond what the format is capable of</span></span>
    2.  <span data-ttu-id="c00cb-156">这对于操作来说尤其重要，因为不同的主机不一定支持同一组操作</span><span class="sxs-lookup"><span data-stu-id="c00cb-156">This is particularly important for actions, as various hosts don't necessarily support the same set of actions</span></span>
    3.  <span data-ttu-id="c00cb-157">是否进行此类添加操作取决于主机</span><span class="sxs-lookup"><span data-stu-id="c00cb-157">These additions are at the discretion of the host</span></span>
        1. <span data-ttu-id="c00cb-158">它们不会以既成事实的方式添加到自适应卡片规范中 </span><span class="sxs-lookup"><span data-stu-id="c00cb-158">They are not a *de facto* addition to the Adaptive Card specification</span></span>
        2. <span data-ttu-id="c00cb-159">因此，使用它们的有效负载会与主流的自适应卡片格式不兼容</span><span class="sxs-lookup"><span data-stu-id="c00cb-159">As such, they make a payload that uses them incompatible with the mainstream Adaptive Card format</span></span>
        3. <span data-ttu-id="c00cb-160">不过，可以将它们提供给工作组，作为适合未来版本格式的新功能进行提交，详见第 5 条原则中的说明</span><span class="sxs-lookup"><span data-stu-id="c00cb-160">They can however be presented to the Working Group and proposed as new features for a future version of the format, as described in point #5</span></span>

8.  <span data-ttu-id="c00cb-161">**卡片作者提供内容，主机应用呈现外观**</span><span class="sxs-lookup"><span data-stu-id="c00cb-161">**Card authors own the content, host apps own the look and feel**</span></span>

    1.  <span data-ttu-id="c00cb-162">主机应用强制实施其样式设置，因此卡片的外观给人的感觉就像应用体验的自然延伸</span><span class="sxs-lookup"><span data-stu-id="c00cb-162">Host apps impose their styling so cards look and feel like they are native extensions of the app's experience</span></span>
    2.  <span data-ttu-id="c00cb-163">卡片作者仍然可以指定样式设置，但只能通过颜色、大小等方面的语义表达式来进行。</span><span class="sxs-lookup"><span data-stu-id="c00cb-163">Card authors can still specify styling, but only via semantic expressions of colors, sizes, etc.</span></span>

9.  <span data-ttu-id="c00cb-164">**将会为最常用的开发人员平台提供 SDK**</span><span class="sxs-lookup"><span data-stu-id="c00cb-164">**SDKs will be provided for the most popular developer platforms**</span></span>

    1.  <span data-ttu-id="c00cb-165">有了 SDK，就可以方便地在任何主机中呈现自适应卡片有效负载</span><span class="sxs-lookup"><span data-stu-id="c00cb-165">SDKs make it easy to render Adaptive Card payloads in any host</span></span>
    2.  <span data-ttu-id="c00cb-166">这样可确保尽量降低第三方开发人员和 Microsoft 团队的进入门槛</span><span class="sxs-lookup"><span data-stu-id="c00cb-166">This ensures the barrier to entry is as low as can be both for third party developers and Microsoft teams</span></span>
