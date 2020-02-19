---
title: 本机样式设置-.NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: 5b829d9eefe933f133c8532030856849802c5eb5
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454490"
---
# <a name="native-styling---net-html"></a><span data-ttu-id="e4b7f-102">本机样式设置-.NET HTML</span><span class="sxs-lookup"><span data-stu-id="e4b7f-102">Native styling - .NET HTML</span></span>

<span data-ttu-id="e4b7f-103">虽然主机配置在每个平台上都可获得大多数方法，但你可能需要在每个平台上执行一些本机样式。</span><span class="sxs-lookup"><span data-stu-id="e4b7f-103">While Host Config will get you most of the way there on each platform, it's likely that you will have to do some native styling on each platform.</span></span> 

<span data-ttu-id="e4b7f-104">HTML 通过向每个元素添加 CSS 类来简化这一过程。</span><span class="sxs-lookup"><span data-stu-id="e4b7f-104">HTML makes this easy by adding CSS classes to every element.</span></span>

| <span data-ttu-id="e4b7f-105">元素</span><span class="sxs-lookup"><span data-stu-id="e4b7f-105">Element</span></span> | <span data-ttu-id="e4b7f-106">CSS 类</span><span class="sxs-lookup"><span data-stu-id="e4b7f-106">CSS class</span></span> |
|---|---|
| <span data-ttu-id="e4b7f-107">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="e4b7f-107">AdaptiveCard</span></span> | <span data-ttu-id="e4b7f-108">ac-adaptivecard</span><span class="sxs-lookup"><span data-stu-id="e4b7f-108">ac-adaptivecard</span></span> |
| <span data-ttu-id="e4b7f-109">所有操作</span><span class="sxs-lookup"><span data-stu-id="e4b7f-109">All Actions</span></span> | <span data-ttu-id="e4b7f-110">ac-按键</span><span class="sxs-lookup"><span data-stu-id="e4b7f-110">ac-pushButton</span></span> | 
| <span data-ttu-id="e4b7f-111">选择操作</span><span class="sxs-lookup"><span data-stu-id="e4b7f-111">Select Actions</span></span> | <span data-ttu-id="e4b7f-112">可选择交流电</span><span class="sxs-lookup"><span data-stu-id="e4b7f-112">ac-selectable</span></span> |
| <span data-ttu-id="e4b7f-113">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="e4b7f-113">Action.OpenUrl</span></span>  | <span data-ttu-id="e4b7f-114">ac-action-openUrl</span><span class="sxs-lookup"><span data-stu-id="e4b7f-114">ac-action-openUrl</span></span> |
| <span data-ttu-id="e4b7f-115">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="e4b7f-115">Action.ShowCard</span></span> | <span data-ttu-id="e4b7f-116">ac-action-showCard</span><span class="sxs-lookup"><span data-stu-id="e4b7f-116">ac-action-showCard</span></span> |
| <span data-ttu-id="e4b7f-117">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="e4b7f-117">Action.Submit</span></span>  | <span data-ttu-id="e4b7f-118">ac-action-submit</span><span class="sxs-lookup"><span data-stu-id="e4b7f-118">ac-action-submit</span></span>  |
| <span data-ttu-id="e4b7f-119">ActionSet</span><span class="sxs-lookup"><span data-stu-id="e4b7f-119">ActionSet</span></span> | <span data-ttu-id="e4b7f-120">ac-actionset</span><span class="sxs-lookup"><span data-stu-id="e4b7f-120">ac-actionset</span></span> |
| <span data-ttu-id="e4b7f-121">列</span><span class="sxs-lookup"><span data-stu-id="e4b7f-121">Column</span></span> | <span data-ttu-id="e4b7f-122">ac 列</span><span class="sxs-lookup"><span data-stu-id="e4b7f-122">ac-column</span></span> |
| <span data-ttu-id="e4b7f-123">ColumnSet</span><span class="sxs-lookup"><span data-stu-id="e4b7f-123">ColumnSet</span></span> | <span data-ttu-id="e4b7f-124">ac-columnset</span><span class="sxs-lookup"><span data-stu-id="e4b7f-124">ac-columnset</span></span> |
| <span data-ttu-id="e4b7f-125">容器</span><span class="sxs-lookup"><span data-stu-id="e4b7f-125">Container</span></span> | <span data-ttu-id="e4b7f-126">ac-容器</span><span class="sxs-lookup"><span data-stu-id="e4b7f-126">ac-container</span></span> |
| <span data-ttu-id="e4b7f-127">所有输入</span><span class="sxs-lookup"><span data-stu-id="e4b7f-127">All Inputs</span></span> | <span data-ttu-id="e4b7f-128">ac-input</span><span class="sxs-lookup"><span data-stu-id="e4b7f-128">ac-input</span></span> |
| <span data-ttu-id="e4b7f-129">Input.ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="e4b7f-129">Input.ChoiceSet</span></span> | <span data-ttu-id="e4b7f-130">ac-multichoiceInput</span><span class="sxs-lookup"><span data-stu-id="e4b7f-130">ac-multichoiceInput</span></span>  |
| <span data-ttu-id="e4b7f-131">Input.Date</span><span class="sxs-lookup"><span data-stu-id="e4b7f-131">Input.Date</span></span> | <span data-ttu-id="e4b7f-132">ac-dateInput</span><span class="sxs-lookup"><span data-stu-id="e4b7f-132">ac-dateInput</span></span> |
| <span data-ttu-id="e4b7f-133">Input.Number</span><span class="sxs-lookup"><span data-stu-id="e4b7f-133">Input.Number</span></span> | <span data-ttu-id="e4b7f-134">ac-numberInput</span><span class="sxs-lookup"><span data-stu-id="e4b7f-134">ac-numberInput</span></span> |
| <span data-ttu-id="e4b7f-135">Input.Text</span><span class="sxs-lookup"><span data-stu-id="e4b7f-135">Input.Text</span></span> | <span data-ttu-id="e4b7f-136">ac-textInput</span><span class="sxs-lookup"><span data-stu-id="e4b7f-136">ac-textInput</span></span> |
| <span data-ttu-id="e4b7f-137">Input.Time</span><span class="sxs-lookup"><span data-stu-id="e4b7f-137">Input.Time</span></span> | <span data-ttu-id="e4b7f-138">ac-timeInput</span><span class="sxs-lookup"><span data-stu-id="e4b7f-138">ac-timeInput</span></span> |
| <span data-ttu-id="e4b7f-139">Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="e4b7f-139">Input.Toggle</span></span>| - |
| <span data-ttu-id="e4b7f-140">映像</span><span class="sxs-lookup"><span data-stu-id="e4b7f-140">Image</span></span>  | <span data-ttu-id="e4b7f-141">ac-映像</span><span class="sxs-lookup"><span data-stu-id="e4b7f-141">ac-image</span></span> |
| <span data-ttu-id="e4b7f-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="e4b7f-142">ImageSet</span></span>  | <span data-ttu-id="e4b7f-143">ac-imageset</span><span class="sxs-lookup"><span data-stu-id="e4b7f-143">ac-imageset</span></span> |
| <span data-ttu-id="e4b7f-144">FactSet</span><span class="sxs-lookup"><span data-stu-id="e4b7f-144">FactSet</span></span> | <span data-ttu-id="e4b7f-145">ac-factset</span><span class="sxs-lookup"><span data-stu-id="e4b7f-145">ac-factset</span></span> |
| <span data-ttu-id="e4b7f-146">TextBlock</span><span class="sxs-lookup"><span data-stu-id="e4b7f-146">TextBlock</span></span>  | <span data-ttu-id="e4b7f-147">ac-textblock</span><span class="sxs-lookup"><span data-stu-id="e4b7f-147">ac-textblock</span></span> |