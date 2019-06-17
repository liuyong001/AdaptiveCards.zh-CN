---
title: Adaptive Cards Roadmap
author: matthidinger
ms.author: mahiding
ms.date: 05/16/2018
ms.topic: article
ms.openlocfilehash: f879c164b3471347ba8fa058827b3d79b09be4cd
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67138000"
---
# <a name="future-work"></a><span data-ttu-id="81e71-102">将来的工作</span><span class="sxs-lookup"><span data-stu-id="81e71-102">Future work</span></span>

<span data-ttu-id="81e71-103">虽然我们已定义自适应卡的极好进度，就仍有很多工作要做。</span><span class="sxs-lookup"><span data-stu-id="81e71-103">While we have made excellent progress defining adaptive cards, there is still lots of work to do.</span></span> <span data-ttu-id="81e71-104">我们希望是，通过等 botness，和 Slack 等很好的合作伙伴和 Kik 活跃的开发人员社区，我们可以创建一个强大的生态系统的跨平台卡。</span><span class="sxs-lookup"><span data-stu-id="81e71-104">Our hope is that through active developer communities like botness, and great partners like Slack and Kik, we can create a great ecosystem of cross-platform cards.</span></span>

## <a name="roadmap"></a><span data-ttu-id="81e71-105">路线图</span><span class="sxs-lookup"><span data-stu-id="81e71-105">Roadmap</span></span>

<span data-ttu-id="81e71-106">您可以看到我们[当前 （非最终） 路线图此处](https://portal.productboard.com/adaptivecards/1-adaptive-cards-portal/tabs/1-backlog)。</span><span class="sxs-lookup"><span data-stu-id="81e71-106">You can see our [current (non-final) roadmap here](https://portal.productboard.com/adaptivecards/1-adaptive-cards-portal/tabs/1-backlog).</span></span> <span data-ttu-id="81e71-107">请注意，此处上的所有内容可能会发生更改，并且并不保证数据传送。</span><span class="sxs-lookup"><span data-stu-id="81e71-107">Note that anything on here is subject to change, and is not a guarantee of shipping.</span></span>

## <a name="future-ideas"></a><span data-ttu-id="81e71-108">将来的想法</span><span class="sxs-lookup"><span data-stu-id="81e71-108">Future ideas</span></span>

<span data-ttu-id="81e71-109">以下是我们有了，只需在灵感阶段中的一些将来观点。</span><span class="sxs-lookup"><span data-stu-id="81e71-109">The following are some future ideas we have, which are simply in the brainstorm stage.</span></span> <span data-ttu-id="81e71-110">如果您感兴趣的这些任何，让我们知道在注释中。</span><span class="sxs-lookup"><span data-stu-id="81e71-110">If you're interested in any of these, let us know in a comment.</span></span>

### <a name="great-looking-cards-from-data"></a><span data-ttu-id="81e71-111">从数据的绝佳美观卡</span><span class="sxs-lookup"><span data-stu-id="81e71-111">Great looking Cards from Data</span></span>

<span data-ttu-id="81e71-112">我们知道已有他们的卡背后的明确定义数据的许多卡作者。</span><span class="sxs-lookup"><span data-stu-id="81e71-112">We know many card authors already have well-defined data behind their cards.</span></span> <span data-ttu-id="81e71-113">我们的计划就是浏览将允许卡生成的模板化模型 （服务器端或客户端） 根据数据和定义完善且可自定义模板的存储库。</span><span class="sxs-lookup"><span data-stu-id="81e71-113">Our plan is to explore a templating model that would allow cards to be generated (server side or client side) based on the data and a repository of well-defined and customizable templates.</span></span>

### <a name="make-cards-responsive"></a><span data-ttu-id="81e71-114">使卡响应</span><span class="sxs-lookup"><span data-stu-id="81e71-114">Make cards responsive</span></span>

<span data-ttu-id="81e71-115">卡布局应为被动变为可用空间。</span><span class="sxs-lookup"><span data-stu-id="81e71-115">Card layouts should be reactive to available space.</span></span> <span data-ttu-id="81e71-116">自适应卡是适应不同的设备，用户体验样式和 ui 框架，但它们不是被动尚未。</span><span class="sxs-lookup"><span data-stu-id="81e71-116">Adaptive cards are adaptable to different devices, ux styles and and ui frameworks, but they are not reactive yet.</span></span> <span data-ttu-id="81e71-117">必须允许卡生成者提供对呈现库的必要提示，以便它们可以智能地更改可维护的卡片的意图的方式布局元素上定义其他属性。</span><span class="sxs-lookup"><span data-stu-id="81e71-117">Additional properties must be defined on elements which allow card producers to provide the necessary hints to the rendering libraries so that they can intelligently change the layout in a way which maintains the intent of the card.</span></span>

### <a name="responsive-exploration"></a><span data-ttu-id="81e71-118">响应式探索</span><span class="sxs-lookup"><span data-stu-id="81e71-118">Responsive exploration</span></span>

* <span data-ttu-id="81e71-119">添加**重要性**属性用于批注的内容的重要性。</span><span class="sxs-lookup"><span data-stu-id="81e71-119">Add an **importance** property which annotates importance of content.</span></span> <span data-ttu-id="81e71-120">可以删除不太重要的内容以适应可用空间</span><span class="sxs-lookup"><span data-stu-id="81e71-120">Less important content can be dropped to fit available space</span></span>
* <span data-ttu-id="81e71-121">添加**约束**并**策略**描述如何做出反应时不能满足约束的属性。</span><span class="sxs-lookup"><span data-stu-id="81e71-121">Add **constraints** and **policy** properties describing how to react when constraints can't be met.</span></span> 
  * <span data-ttu-id="81e71-122">隐藏的内容或内容折叠到小的大小。</span><span class="sxs-lookup"><span data-stu-id="81e71-122">Hide content or collapse content to smaller size.</span></span>
  * <span data-ttu-id="81e71-123">添加的阈值，超出时，更改`columnSet`到轮播的列。</span><span class="sxs-lookup"><span data-stu-id="81e71-123">Add a threshold that, when exceeded, changes `columnSet` to carousel of columns.</span></span>

### <a name="new-element-types"></a><span data-ttu-id="81e71-124">新的元素类型</span><span class="sxs-lookup"><span data-stu-id="81e71-124">New element types</span></span>

* <span data-ttu-id="81e71-125">映射？</span><span class="sxs-lookup"><span data-stu-id="81e71-125">Maps?</span></span> <span data-ttu-id="81e71-126">-将地图嵌入到卡具有交互性或回退到位图</span><span class="sxs-lookup"><span data-stu-id="81e71-126">- embed a map into a card with interactivity or fallback to bitmap</span></span>
* <span data-ttu-id="81e71-127">*哪些元素执行您想要或需要*？</span><span class="sxs-lookup"><span data-stu-id="81e71-127">*What elements do you want or need*?</span></span>

### <a name="new-rendering-libraries"></a><span data-ttu-id="81e71-128">新呈现库</span><span class="sxs-lookup"><span data-stu-id="81e71-128">New rendering libraries</span></span>

* <span data-ttu-id="81e71-129">反应？</span><span class="sxs-lookup"><span data-stu-id="81e71-129">React?</span></span>
* <span data-ttu-id="81e71-130">Xamarin？</span><span class="sxs-lookup"><span data-stu-id="81e71-130">Xamarin?</span></span>
* <span data-ttu-id="81e71-131">*你想什么框架？*</span><span class="sxs-lookup"><span data-stu-id="81e71-131">*What frameworks do you want?*</span></span>
