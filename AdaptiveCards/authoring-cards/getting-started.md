---
title: 入门
author: matthidinger
ms.author: mahiding
ms.date: 11/9/2017
ms.topic: article
ms.openlocfilehash: c9a0ad07ba5fefbcdc35239591c02fe0720b5b66
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454840"
---
# <a name="getting-started"></a><span data-ttu-id="9899c-102">入门</span><span class="sxs-lookup"><span data-stu-id="9899c-102">Getting Started</span></span> 

<span data-ttu-id="9899c-103">自适应卡片是进行了 JSON 序列化的卡片对象模型。</span><span class="sxs-lookup"><span data-stu-id="9899c-103">An Adaptive Card is a JSON-serialized card object model.</span></span>

## <a name="adaptive-card-structure"></a><span data-ttu-id="9899c-104">自适应卡片结构</span><span class="sxs-lookup"><span data-stu-id="9899c-104">Adaptive Card structure</span></span>

<span data-ttu-id="9899c-105">卡片的基本结构如下：</span><span class="sxs-lookup"><span data-stu-id="9899c-105">The basic structure of a card is as follows:</span></span>

* <span data-ttu-id="9899c-106">`AdaptiveCard` - 此根对象描述 AdaptiveCard 本身，包括其元素构成、其操作、其朗读方式，以及呈现它所需的架构版本。</span><span class="sxs-lookup"><span data-stu-id="9899c-106">`AdaptiveCard` - The root object describes the AdaptiveCard itself, including its element makeup, its actions, how it should be spoken, and the schema version required to render it.</span></span>
* <span data-ttu-id="9899c-107">`body` - 卡片的主体由称为 `elements` 的构建基块组成。</span><span class="sxs-lookup"><span data-stu-id="9899c-107">`body` - The body of the card is made up of building-blocks known as `elements`.</span></span> <span data-ttu-id="9899c-108">元素有几乎无限的排列组合，因此可以创建许多类型的卡片。</span><span class="sxs-lookup"><span data-stu-id="9899c-108">Elements can be composed in nearly infinite arrangements to create many types of cards.</span></span> 
* <span data-ttu-id="9899c-109">`actions` - 许多卡片有一组可供用户在其上执行的操作。</span><span class="sxs-lookup"><span data-stu-id="9899c-109">`actions` - Many cards have a set of actions a user may take on it.</span></span> <span data-ttu-id="9899c-110">此属性描述的那些操作通常在底部的“操作栏”中呈现。</span><span class="sxs-lookup"><span data-stu-id="9899c-110">This property describes those actions which typically get rendered in an "action bar" at the bottom.</span></span>

### <a name="example-card"></a><span data-ttu-id="9899c-111">示例卡片</span><span class="sxs-lookup"><span data-stu-id="9899c-111">Example Card</span></span>

<span data-ttu-id="9899c-112">此示例卡片包括单行文本和一张图像。</span><span class="sxs-lookup"><span data-stu-id="9899c-112">This sample card which includes a single line of text followed by an image.</span></span>

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

## <a name="type-property"></a><span data-ttu-id="9899c-113">`Type` 属性</span><span class="sxs-lookup"><span data-stu-id="9899c-113">`Type` property</span></span>

<span data-ttu-id="9899c-114">每个元素都有一个 `type` 属性，用于标识它是哪种类型的对象。</span><span class="sxs-lookup"><span data-stu-id="9899c-114">Every element has a `type` property which identifies what kind of object it is.</span></span> <span data-ttu-id="9899c-115">看看上面这张卡片，可以看到我们有两个元素：`TextBlock` 和 `Image`。</span><span class="sxs-lookup"><span data-stu-id="9899c-115">Looking at the above card, you can see we have two elements, a `TextBlock` and an `Image`.</span></span>

<span data-ttu-id="9899c-116">所有自适应卡片元素都会**垂直进行堆叠**，并**在受父项限制的情况下进行横向扩展**（这类似于 HTML 中的 `display: block`）。</span><span class="sxs-lookup"><span data-stu-id="9899c-116">All Adaptive Card elements **stack vertically** and **expand to the width of their parent** (think `display: block` in HTML).</span></span> <span data-ttu-id="9899c-117">不过，可以使用 `ColumnSet` 创建多个包含容器的并排列。</span><span class="sxs-lookup"><span data-stu-id="9899c-117">However, you can use a `ColumnSet` to create side-by-side columns of containers.</span></span>

## <a name="adaptive-elements"></a><span data-ttu-id="9899c-118">自适应元素</span><span class="sxs-lookup"><span data-stu-id="9899c-118">Adaptive Elements</span></span>

<span data-ttu-id="9899c-119">最基本的元素包括：</span><span class="sxs-lookup"><span data-stu-id="9899c-119">The most fundamental elements are:</span></span>

* <span data-ttu-id="9899c-120">**TextBlock** - 添加一个文本块，其包含的属性可以用来控制文本的外观</span><span class="sxs-lookup"><span data-stu-id="9899c-120">**TextBlock** - adds a block of text with properties to control what the text looks like</span></span>
* <span data-ttu-id="9899c-121">**Image** - 添加一个图像，其包含的属性可以用来控制图像的外观</span><span class="sxs-lookup"><span data-stu-id="9899c-121">**Image** - adds an image with properties to control what the image looks like</span></span>

## <a name="container-elements"></a><span data-ttu-id="9899c-122">容器元素</span><span class="sxs-lookup"><span data-stu-id="9899c-122">Container elements</span></span>

<span data-ttu-id="9899c-123">卡片也可以有容器，用于对一组子元素进行排列组合。</span><span class="sxs-lookup"><span data-stu-id="9899c-123">Cards can also have containers, which arrange a collection of child elements.</span></span>

* <span data-ttu-id="9899c-124">**Container** - 定义一组元素</span><span class="sxs-lookup"><span data-stu-id="9899c-124">**Container** - Defines a a collection of elements</span></span>
* <span data-ttu-id="9899c-125">**ColumnSet/Column** - 定义一组列，每个列都是一个容器</span><span class="sxs-lookup"><span data-stu-id="9899c-125">**ColumnSet/Column** - Defines a collection of columns, each column is a container</span></span>
* <span data-ttu-id="9899c-126">**FactSet** - 事实容器</span><span class="sxs-lookup"><span data-stu-id="9899c-126">**FactSet** - Container of Facts</span></span>
* <span data-ttu-id="9899c-127">**ImageSet** - 图像容器，方便 UI 针对一组图像显示相应的照片库体验。</span><span class="sxs-lookup"><span data-stu-id="9899c-127">**ImageSet** - Container of Images so that UI can show appropriate photo gallery experience for a collection of images.</span></span>

## <a name="input-elements"></a><span data-ttu-id="9899c-128">输入元素</span><span class="sxs-lookup"><span data-stu-id="9899c-128">Input elements</span></span>

<span data-ttu-id="9899c-129">可以通过输入元素要求本机 UI 构建简单的窗体：</span><span class="sxs-lookup"><span data-stu-id="9899c-129">Input elements allow you to ask for native UI to build simple forms:</span></span>

* <span data-ttu-id="9899c-130">**Input.Text** - 从用户获取文本内容</span><span class="sxs-lookup"><span data-stu-id="9899c-130">**Input.Text** - get text content from the user</span></span>
* <span data-ttu-id="9899c-131">**Input.Date** - 从用户获取日期</span><span class="sxs-lookup"><span data-stu-id="9899c-131">**Input.Date** - get a Date from the user</span></span>
* <span data-ttu-id="9899c-132">**Input.Time** - 从用户获取时间</span><span class="sxs-lookup"><span data-stu-id="9899c-132">**Input.Time** - get a Time from the user</span></span>
* <span data-ttu-id="9899c-133">**Input.Number** - 从用户获取数字</span><span class="sxs-lookup"><span data-stu-id="9899c-133">**Input.Number** - get a Number from the user</span></span>
* <span data-ttu-id="9899c-134">**Input.ChoiceSet** - 为用户提供一组选项供其选取</span><span class="sxs-lookup"><span data-stu-id="9899c-134">**Input.ChoiceSet** - Give the user a set of choices and have them pick</span></span>
* <span data-ttu-id="9899c-135">**Input.Toggle** - 为用户提供一个在两个项之间进行切换的切换式选项供其选取</span><span class="sxs-lookup"><span data-stu-id="9899c-135">**Input.Toggle** - Give the user a single choice between two items and have them pick</span></span>

## <a name="actions"></a><span data-ttu-id="9899c-136">“操作”</span><span class="sxs-lookup"><span data-stu-id="9899c-136">Actions</span></span>

<span data-ttu-id="9899c-137">操作会将按钮添加到卡片上。</span><span class="sxs-lookup"><span data-stu-id="9899c-137">Actions add buttons to the card.</span></span> <span data-ttu-id="9899c-138">这些按钮可以执行多种操作，例如打开 URL 或提交某些数据。</span><span class="sxs-lookup"><span data-stu-id="9899c-138">These can perform a variety of actions, like opening a URL or submitting some data.</span></span>

* <span data-ttu-id="9899c-139">**Action.OpenUrl** - 按钮打开一个供查看的外部 URL</span><span class="sxs-lookup"><span data-stu-id="9899c-139">**Action.OpenUrl** - the button opens an external URL for viewing</span></span>
* <span data-ttu-id="9899c-140">**Action.ShowCard** - 请求一张显示给用户的子卡。</span><span class="sxs-lookup"><span data-stu-id="9899c-140">**Action.ShowCard** - Requests a sub-card to be shown to the user.</span></span>
* <span data-ttu-id="9899c-141">**Action.Submit** - 要求将所有输入元素收集到一个对象中，然后通过主机应用程序定义的某个方法将该对象发送给你。</span><span class="sxs-lookup"><span data-stu-id="9899c-141">**Action.Submit** - Ask for all of the input elements to be gathered up into an object which is then sent to you through some method defined by the host application.</span></span>

> <span data-ttu-id="9899c-142">**示例 Action.Submit**：使用 Skype 时，Action.Submit 会将 Bot Framework 机器人活动发送回机器人，其中的 **Value** 属性包含一个其上有所有输入数据的对象。</span><span class="sxs-lookup"><span data-stu-id="9899c-142">**Example Action.Submit**: With Skype, an Action.Submit will send a Bot Framework bot activity back to the bot with the **Value** property containing an object with all of the input data on it.</span></span>

## <a name="learn-more"></a><span data-ttu-id="9899c-143">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="9899c-143">Learn More</span></span>

* <span data-ttu-id="9899c-144">[浏览示例卡片](http://adaptivecards.io/samples/)获取灵感</span><span class="sxs-lookup"><span data-stu-id="9899c-144">[Browse Sample cards](http://adaptivecards.io/samples/) for inspiration</span></span>
* <span data-ttu-id="9899c-145">使用[架构资源管理器](http://adaptivecards.io/explorer)浏览可用元素</span><span class="sxs-lookup"><span data-stu-id="9899c-145">Use the [Schema Explorer](http://adaptivecards.io/explorer) to browse the available elements</span></span>
* <span data-ttu-id="9899c-146">使用[交互式可视化工具](http://adaptivecards.io/visualizer/)构建一张卡片</span><span class="sxs-lookup"><span data-stu-id="9899c-146">Build a card using the [Interactive Visualizer](http://adaptivecards.io/visualizer/)</span></span>
* <span data-ttu-id="9899c-147">如果你有任何反馈，请[联系我们](http://adaptivecards.io/connect)</span><span class="sxs-lookup"><span data-stu-id="9899c-147">[Get in touch](http://adaptivecards.io/connect) with any feedback you have</span></span>
