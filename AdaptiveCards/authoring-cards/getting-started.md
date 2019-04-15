---
title: 入门
author: matthidinger
ms.author: mahiding
ms.date: 11/9/2017
ms.topic: article
ms.openlocfilehash: 9d363da0c10b242e23d2594984292fcc1f31382f
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552679"
---
# <a name="getting-started"></a><span data-ttu-id="ebdd9-102">入门</span><span class="sxs-lookup"><span data-stu-id="ebdd9-102">Getting Started</span></span> 

<span data-ttu-id="ebdd9-103">自适应卡是一个 JSON 序列化卡对象模型。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-103">An Adaptive Card is a JSON-serialized card object model.</span></span>

## <a name="adaptive-card-structure"></a><span data-ttu-id="ebdd9-104">自适应卡结构</span><span class="sxs-lookup"><span data-stu-id="ebdd9-104">Adaptive Card structure</span></span>

<span data-ttu-id="ebdd9-105">卡片的基本结构是按如下所示：</span><span class="sxs-lookup"><span data-stu-id="ebdd9-105">The basic structure of a card is as follows:</span></span>

* <span data-ttu-id="ebdd9-106">`AdaptiveCard` -根对象描述 AdaptiveCard 本身，包括其元素构成、 其操作、 如何应朗读它，以及呈现它所需的架构版本。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-106">`AdaptiveCard` - The root object describes the AdaptiveCard itself, including its element makeup, its actions, how it should be spoken, and the schema version required to render it.</span></span>
* <span data-ttu-id="ebdd9-107">`body` 的卡片正文组成的构建基块称为`elements`。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-107">`body` - The body of the card is made up of building-blocks known as `elements`.</span></span> <span data-ttu-id="ebdd9-108">元素可以包含几乎无限的布局，以创建多个类型的卡中。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-108">Elements can be composed in nearly infinite arrangements to create many types of cards.</span></span> 
* <span data-ttu-id="ebdd9-109">`actions` -许多数据卡也有一组用户可能在其执行的操作。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-109">`actions` - Many cards have a set of actions a user may take on it.</span></span> <span data-ttu-id="ebdd9-110">此属性描述了这些操作，这通常在底部"操作栏"中的呈现。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-110">This property describes those actions which typically get rendered in an "action bar" at the bottom.</span></span>

### <a name="example-card"></a><span data-ttu-id="ebdd9-111">示例卡</span><span class="sxs-lookup"><span data-stu-id="ebdd9-111">Example Card</span></span>

<span data-ttu-id="ebdd9-112">此示例卡，其中包括单个跟图像的文本行。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-112">This sample card which includes a single line of text followed by an image.</span></span>

```json
{
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png"
        }
    ]
}
```

## <a name="type-property"></a><span data-ttu-id="ebdd9-113">`Type` 属性</span><span class="sxs-lookup"><span data-stu-id="ebdd9-113">`Type` property</span></span>

<span data-ttu-id="ebdd9-114">每个元素都`type`标识何种类型的对象的属性。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-114">Every element has a `type` property which identifies what kind of object it is.</span></span> <span data-ttu-id="ebdd9-115">查看上面的卡，可以看到我们有两个元素`TextBlock`和一个`Image`。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-115">Looking at the above card, you can see we have two elements, a `TextBlock` and an `Image`.</span></span>

<span data-ttu-id="ebdd9-116">自适应卡的所有元素**垂直堆叠**并**扩展到其父级的宽度**(认为`display: block`以 html 格式)。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-116">All Adaptive Card elements **stack vertically** and **expand to the width of their parent** (think `display: block` in HTML).</span></span> <span data-ttu-id="ebdd9-117">但是，可以使用`ColumnSet`若要创建的容器-同时列。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-117">However, you can use a `ColumnSet` to create side-by-side columns of containers.</span></span>

## <a name="adaptive-elements"></a><span data-ttu-id="ebdd9-118">自适应元素</span><span class="sxs-lookup"><span data-stu-id="ebdd9-118">Adaptive Elements</span></span>

<span data-ttu-id="ebdd9-119">最基本的元素是：</span><span class="sxs-lookup"><span data-stu-id="ebdd9-119">The most fundamental elements are:</span></span>

* <span data-ttu-id="ebdd9-120">**TextBlock** -添加具有属性来控制文本如下所示的文本块</span><span class="sxs-lookup"><span data-stu-id="ebdd9-120">**TextBlock** - adds a block of text with properties to control what the text looks like</span></span>
* <span data-ttu-id="ebdd9-121">**映像**-将使用属性来控制图像如下所示的图像添加</span><span class="sxs-lookup"><span data-stu-id="ebdd9-121">**Image** - adds an image with properties to control what the image looks like</span></span>

## <a name="container-elements"></a><span data-ttu-id="ebdd9-122">容器元素</span><span class="sxs-lookup"><span data-stu-id="ebdd9-122">Container elements</span></span>

<span data-ttu-id="ebdd9-123">卡还可以排列子元素的集合的容器。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-123">Cards can also have containers, which arrange a collection of child elements.</span></span>

* <span data-ttu-id="ebdd9-124">**容器**-定义元素的集合</span><span class="sxs-lookup"><span data-stu-id="ebdd9-124">**Container** - Defines a a collection of elements</span></span>
* <span data-ttu-id="ebdd9-125">**列集/列**-定义集合的列，每个列是一个容器</span><span class="sxs-lookup"><span data-stu-id="ebdd9-125">**ColumnSet/Column** - Defines a collection of columns, each column is a container</span></span>
* <span data-ttu-id="ebdd9-126">**FactSet**的事实数据的容器</span><span class="sxs-lookup"><span data-stu-id="ebdd9-126">**FactSet** - Container of Facts</span></span>
* <span data-ttu-id="ebdd9-127">**ImageSet** -容器的映像以便该 UI 可以显示相应照片库体验的映像集合。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-127">**ImageSet** - Container of Images so that UI can show appropriate photo gallery experience for a collection of images.</span></span>

## <a name="input-elements"></a><span data-ttu-id="ebdd9-128">输入的元素</span><span class="sxs-lookup"><span data-stu-id="ebdd9-128">Input elements</span></span>

<span data-ttu-id="ebdd9-129">输入的元素允许您提出的本机 UI，以生成简单的窗体：</span><span class="sxs-lookup"><span data-stu-id="ebdd9-129">Input elements allow you to ask for native UI to build simple forms:</span></span>

* <span data-ttu-id="ebdd9-130">**Input.Text** -从用户获取文本内容</span><span class="sxs-lookup"><span data-stu-id="ebdd9-130">**Input.Text** - get text content from the user</span></span>
* <span data-ttu-id="ebdd9-131">**Input.Date** -从用户获取日期</span><span class="sxs-lookup"><span data-stu-id="ebdd9-131">**Input.Date** - get a Date from the user</span></span>
* <span data-ttu-id="ebdd9-132">**Input.Time** -从用户获取一次</span><span class="sxs-lookup"><span data-stu-id="ebdd9-132">**Input.Time** - get a Time from the user</span></span>
* <span data-ttu-id="ebdd9-133">**Input.Number** -从用户获取一个数字</span><span class="sxs-lookup"><span data-stu-id="ebdd9-133">**Input.Number** - get a Number from the user</span></span>
* <span data-ttu-id="ebdd9-134">**Input.ChoiceSet** -为用户提供的一组选项，并让他们选择</span><span class="sxs-lookup"><span data-stu-id="ebdd9-134">**Input.ChoiceSet** - Give the user a set of choices and have them pick</span></span>
* <span data-ttu-id="ebdd9-135">**Input.Toggle** -为用户提供两个项之间的单个选择，并让他们选择</span><span class="sxs-lookup"><span data-stu-id="ebdd9-135">**Input.Toggle** - Give the user a single choice between two items and have them pick</span></span>

## <a name="actions"></a><span data-ttu-id="ebdd9-136">操作</span><span class="sxs-lookup"><span data-stu-id="ebdd9-136">Actions</span></span>

<span data-ttu-id="ebdd9-137">操作添加到卡片的按钮。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-137">Actions add buttons to the card.</span></span> <span data-ttu-id="ebdd9-138">这些可执行各种操作，如打开 URL 或提交一些数据。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-138">These can perform a variety of actions, like opening a URL or submitting some data.</span></span>

* <span data-ttu-id="ebdd9-139">**Action.OpenUrl** -此按钮将打开外部 URL 以进行查看</span><span class="sxs-lookup"><span data-stu-id="ebdd9-139">**Action.OpenUrl** - the button opens an external URL for viewing</span></span>
* <span data-ttu-id="ebdd9-140">**Action.ShowCard** -请求子卡以向用户显示。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-140">**Action.ShowCard** - Requests a sub-card to be shown to the user.</span></span>
* <span data-ttu-id="ebdd9-141">**Action.Submit** -输入元素的所有要求，以便收集到的对象，然后将它发送给你通过主机应用程序定义的一些方法。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-141">**Action.Submit** - Ask for all of the input elements to be gathered up into an object which is then sent to you through some method defined by the host application.</span></span>

> <span data-ttu-id="ebdd9-142">**示例 Action.Submit**:使用 Skype，Action.Submit 将发送 Bot Framework 机器人活动回复到智能机器人**值**包含对它的输入数据的所有对象的属性。</span><span class="sxs-lookup"><span data-stu-id="ebdd9-142">**Example Action.Submit**: With Skype, an Action.Submit will send a Bot Framework bot activity back to the bot with the **Value** property containing an object with all of the input data on it.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ebdd9-143">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="ebdd9-143">Learn More</span></span>

* <span data-ttu-id="ebdd9-144">[浏览示例卡](http://adaptivecards.io/samples/)激发灵感</span><span class="sxs-lookup"><span data-stu-id="ebdd9-144">[Browse Sample cards](http://adaptivecards.io/samples/) for inspiration</span></span>
* <span data-ttu-id="ebdd9-145">使用[架构资源管理器](http://adaptivecards.io/explorer)浏览可用元素</span><span class="sxs-lookup"><span data-stu-id="ebdd9-145">Use the [Schema Explorer](http://adaptivecards.io/explorer) to browse the available elements</span></span>
* <span data-ttu-id="ebdd9-146">生成卡使用[交互式可视化工具](http://adaptivecards.io/visualizer/)</span><span class="sxs-lookup"><span data-stu-id="ebdd9-146">Build a card using the [Interactive Visualizer](http://adaptivecards.io/visualizer/)</span></span>
* <span data-ttu-id="ebdd9-147">[与我们联系](http://adaptivecards.io/connect)与你有任何反馈</span><span class="sxs-lookup"><span data-stu-id="ebdd9-147">[Get in touch](http://adaptivecards.io/connect) with any feedback you have</span></span>
