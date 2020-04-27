---
title: 自适应卡片路线图
author: matthidinger
ms.author: mahiding
ms.date: 05/16/2018
ms.topic: article
ms.openlocfilehash: b11edbedca83bb26d2990d029a220165f68bc1ca
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "77454890"
---
# <a name="future-work"></a><span data-ttu-id="cdf9a-102">未来工作</span><span class="sxs-lookup"><span data-stu-id="cdf9a-102">Future work</span></span>

<span data-ttu-id="cdf9a-103">虽然我们已在定义自适应卡片方面有了很大的进展，但仍有大量工作要做。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-103">While we have made excellent progress defining adaptive cards, there is still lots of work to do.</span></span> <span data-ttu-id="cdf9a-104">我们希望，通过 Botness 之类的开发人员社区的积极参与，以及 Slack 和 Kik 之类的合作伙伴的通力协作，我们可以打造一个跨平台卡片的良好生态系统。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-104">Our hope is that through active developer communities like botness, and great partners like Slack and Kik, we can create a great ecosystem of cross-platform cards.</span></span>

## <a name="roadmap"></a><span data-ttu-id="cdf9a-105">路线图</span><span class="sxs-lookup"><span data-stu-id="cdf9a-105">Roadmap</span></span>

<span data-ttu-id="cdf9a-106">你可以在[这里查看我们当前（并非最终）的路线图](https://portal.productboard.com/adaptivecards/1-adaptive-cards-portal/tabs/1-backlog)。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-106">You can see our [current (non-final) roadmap here](https://portal.productboard.com/adaptivecards/1-adaptive-cards-portal/tabs/1-backlog).</span></span> <span data-ttu-id="cdf9a-107">请注意，此处的任何内容都可能会更改，不保证寄送。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-107">Note that anything on here is subject to change, and is not a guarantee of shipping.</span></span>

## <a name="future-ideas"></a><span data-ttu-id="cdf9a-108">未来创意</span><span class="sxs-lookup"><span data-stu-id="cdf9a-108">Future ideas</span></span>

<span data-ttu-id="cdf9a-109">下面是我们的一些未来创意，仍处于集体讨论阶段。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-109">The following are some future ideas we have, which are simply in the brainstorm stage.</span></span> <span data-ttu-id="cdf9a-110">如果你对其中的任何内容感兴趣，请在评论中给我们留言。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-110">If you're interested in any of these, let us know in a comment.</span></span>

### <a name="great-looking-cards-from-data"></a><span data-ttu-id="cdf9a-111">外观良好的卡片离不开数据</span><span class="sxs-lookup"><span data-stu-id="cdf9a-111">Great looking Cards from Data</span></span>

<span data-ttu-id="cdf9a-112">我们知道，许多卡片作者已经有可以在卡片上使用的定义好的数据。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-112">We know many card authors already have well-defined data behind their cards.</span></span> <span data-ttu-id="cdf9a-113">我们的计划是探索出一个模板化的模型，这样，用户就可以使用数据以及定义好的可自定义模板的库来生成卡片（不管是在服务器端还是在客户端）。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-113">Our plan is to explore a templating model that would allow cards to be generated (server side or client side) based on the data and a repository of well-defined and customizable templates.</span></span>

### <a name="make-cards-responsive"></a><span data-ttu-id="cdf9a-114">让卡片响应快</span><span class="sxs-lookup"><span data-stu-id="cdf9a-114">Make cards responsive</span></span>

<span data-ttu-id="cdf9a-115">卡片布局应该可以根据可用空间大小进行调整。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-115">Card layouts should be reactive to available space.</span></span> <span data-ttu-id="cdf9a-116">自适应卡片可以适应不同的设备、UX 样式和 UI 框架，但它们还无法主动进行调整。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-116">Adaptive cards are adaptable to different devices, ux styles and and ui frameworks, but they are not reactive yet.</span></span> <span data-ttu-id="cdf9a-117">必须在元素上定义其他属性，让卡片生产者可以为呈现库提供必需的提示，这样库就能够以智能方式更改布局，使卡片的用途不变。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-117">Additional properties must be defined on elements which allow card producers to provide the necessary hints to the rendering libraries so that they can intelligently change the layout in a way which maintains the intent of the card.</span></span>

### <a name="responsive-exploration"></a><span data-ttu-id="cdf9a-118">响应式浏览</span><span class="sxs-lookup"><span data-stu-id="cdf9a-118">Responsive exploration</span></span>

* <span data-ttu-id="cdf9a-119">添加 **importance** 属性，标注内容的重要性。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-119">Add an **importance** property which annotates importance of content.</span></span> <span data-ttu-id="cdf9a-120">可以根据空间大小删除不太重要的内容</span><span class="sxs-lookup"><span data-stu-id="cdf9a-120">Less important content can be dropped to fit available space</span></span>
* <span data-ttu-id="cdf9a-121">添加 **constraints** 和 **policy** 属性，说明在无法满足约束条件的情况下无法进行应对。</span><span class="sxs-lookup"><span data-stu-id="cdf9a-121">Add **constraints** and **policy** properties describing how to react when constraints can't be met.</span></span> 
  * <span data-ttu-id="cdf9a-122">隐藏内容，或者将内容折叠以降低其大小</span><span class="sxs-lookup"><span data-stu-id="cdf9a-122">Hide content or collapse content to smaller size.</span></span>
  * <span data-ttu-id="cdf9a-123">添加一个阈值，超过该阈值时更改 `columnSet`，将列循环展示</span><span class="sxs-lookup"><span data-stu-id="cdf9a-123">Add a threshold that, when exceeded, changes `columnSet` to carousel of columns.</span></span>

### <a name="new-element-types"></a><span data-ttu-id="cdf9a-124">新元素类型</span><span class="sxs-lookup"><span data-stu-id="cdf9a-124">New element types</span></span>

* <span data-ttu-id="cdf9a-125">地图？</span><span class="sxs-lookup"><span data-stu-id="cdf9a-125">Maps?</span></span> <span data-ttu-id="cdf9a-126">- 将地图嵌入具有交互功能的卡片中，或者回退到位图</span><span class="sxs-lookup"><span data-stu-id="cdf9a-126">- embed a map into a card with interactivity or fallback to bitmap</span></span>
* <span data-ttu-id="cdf9a-127">你想要或需要什么元素？ </span><span class="sxs-lookup"><span data-stu-id="cdf9a-127">*What elements do you want or need*?</span></span>

### <a name="new-rendering-libraries"></a><span data-ttu-id="cdf9a-128">新的呈现库</span><span class="sxs-lookup"><span data-stu-id="cdf9a-128">New rendering libraries</span></span>

* <span data-ttu-id="cdf9a-129">React？</span><span class="sxs-lookup"><span data-stu-id="cdf9a-129">React?</span></span>
* <span data-ttu-id="cdf9a-130">Xamarin？</span><span class="sxs-lookup"><span data-stu-id="cdf9a-130">Xamarin?</span></span>
* <span data-ttu-id="cdf9a-131">你想要什么框架？ </span><span class="sxs-lookup"><span data-stu-id="cdf9a-131">*What frameworks do you want?*</span></span>
