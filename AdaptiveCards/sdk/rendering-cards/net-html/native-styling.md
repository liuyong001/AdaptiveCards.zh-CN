---
title: 本机样式-.NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: 620940dee873742898d58979c61827320bc3c202
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552559"
---
# <a name="native-styling---net-html"></a><span data-ttu-id="3ef08-102">本机样式-.NET HTML</span><span class="sxs-lookup"><span data-stu-id="3ef08-102">Native styling - .NET HTML</span></span>

<span data-ttu-id="3ef08-103">尽管主机配置可以帮助您了解大多数的方式有每个平台上，很可能您将只需在每个平台上的某些本机样式设置。</span><span class="sxs-lookup"><span data-stu-id="3ef08-103">While Host Config will get you most of the way there on each platform, it's likely that you will have to do some native styling on each platform.</span></span> 

<span data-ttu-id="3ef08-104">HTML 轻松这通过将 CSS 类添加到每个元素。</span><span class="sxs-lookup"><span data-stu-id="3ef08-104">HTML makes this easy by adding CSS classes to every element.</span></span>

| <span data-ttu-id="3ef08-105">元素</span><span class="sxs-lookup"><span data-stu-id="3ef08-105">Element</span></span> | <span data-ttu-id="3ef08-106">CSS 类</span><span class="sxs-lookup"><span data-stu-id="3ef08-106">CSS class</span></span> |
|---|---|
| <span data-ttu-id="3ef08-107">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="3ef08-107">AdaptiveCard</span></span> | <span data-ttu-id="3ef08-108">ac-adaptivecard</span><span class="sxs-lookup"><span data-stu-id="3ef08-108">ac-adaptivecard</span></span> |
| <span data-ttu-id="3ef08-109">所有操作</span><span class="sxs-lookup"><span data-stu-id="3ef08-109">All Actions</span></span> | <span data-ttu-id="3ef08-110">ac-pushButton</span><span class="sxs-lookup"><span data-stu-id="3ef08-110">ac-pushButton</span></span> | 
| <span data-ttu-id="3ef08-111">选择操作</span><span class="sxs-lookup"><span data-stu-id="3ef08-111">Select Actions</span></span> | <span data-ttu-id="3ef08-112">ac-selectable</span><span class="sxs-lookup"><span data-stu-id="3ef08-112">ac-selectable</span></span> |
| <span data-ttu-id="3ef08-113">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="3ef08-113">Action.OpenUrl</span></span>  | <span data-ttu-id="3ef08-114">ac-action-openUrl</span><span class="sxs-lookup"><span data-stu-id="3ef08-114">ac-action-openUrl</span></span> |
| <span data-ttu-id="3ef08-115">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="3ef08-115">Action.ShowCard</span></span> | <span data-ttu-id="3ef08-116">ac-action-showCard</span><span class="sxs-lookup"><span data-stu-id="3ef08-116">ac-action-showCard</span></span> |
| <span data-ttu-id="3ef08-117">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="3ef08-117">Action.Submit</span></span>  | <span data-ttu-id="3ef08-118">ac-action-submit</span><span class="sxs-lookup"><span data-stu-id="3ef08-118">ac-action-submit</span></span>  |
| <span data-ttu-id="3ef08-119">ActionSet</span><span class="sxs-lookup"><span data-stu-id="3ef08-119">ActionSet</span></span> | <span data-ttu-id="3ef08-120">ac-actionset</span><span class="sxs-lookup"><span data-stu-id="3ef08-120">ac-actionset</span></span> |
| <span data-ttu-id="3ef08-121">列</span><span class="sxs-lookup"><span data-stu-id="3ef08-121">Column</span></span> | <span data-ttu-id="3ef08-122">ac-column</span><span class="sxs-lookup"><span data-stu-id="3ef08-122">ac-column</span></span> |
| <span data-ttu-id="3ef08-123">ColumnSet</span><span class="sxs-lookup"><span data-stu-id="3ef08-123">ColumnSet</span></span> | <span data-ttu-id="3ef08-124">ac-columnset</span><span class="sxs-lookup"><span data-stu-id="3ef08-124">ac-columnset</span></span> |
| <span data-ttu-id="3ef08-125">容器</span><span class="sxs-lookup"><span data-stu-id="3ef08-125">Container</span></span> | <span data-ttu-id="3ef08-126">ac-container</span><span class="sxs-lookup"><span data-stu-id="3ef08-126">ac-container</span></span> |
| <span data-ttu-id="3ef08-127">所有输入</span><span class="sxs-lookup"><span data-stu-id="3ef08-127">All Inputs</span></span> | <span data-ttu-id="3ef08-128">ac-input</span><span class="sxs-lookup"><span data-stu-id="3ef08-128">ac-input</span></span> |
| <span data-ttu-id="3ef08-129">Input.ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="3ef08-129">Input.ChoiceSet</span></span> | <span data-ttu-id="3ef08-130">ac-multichoiceInput</span><span class="sxs-lookup"><span data-stu-id="3ef08-130">ac-multichoiceInput</span></span>  |
| <span data-ttu-id="3ef08-131">Input.Date</span><span class="sxs-lookup"><span data-stu-id="3ef08-131">Input.Date</span></span> | <span data-ttu-id="3ef08-132">ac-dateInput</span><span class="sxs-lookup"><span data-stu-id="3ef08-132">ac-dateInput</span></span> |
| <span data-ttu-id="3ef08-133">Input.Number</span><span class="sxs-lookup"><span data-stu-id="3ef08-133">Input.Number</span></span> | <span data-ttu-id="3ef08-134">ac-numberInput</span><span class="sxs-lookup"><span data-stu-id="3ef08-134">ac-numberInput</span></span> |
| <span data-ttu-id="3ef08-135">Input.Text</span><span class="sxs-lookup"><span data-stu-id="3ef08-135">Input.Text</span></span> | <span data-ttu-id="3ef08-136">ac-textInput</span><span class="sxs-lookup"><span data-stu-id="3ef08-136">ac-textInput</span></span> |
| <span data-ttu-id="3ef08-137">Input.Time</span><span class="sxs-lookup"><span data-stu-id="3ef08-137">Input.Time</span></span> | <span data-ttu-id="3ef08-138">ac-timeInput</span><span class="sxs-lookup"><span data-stu-id="3ef08-138">ac-timeInput</span></span> |
| <span data-ttu-id="3ef08-139">Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="3ef08-139">Input.Toggle</span></span>| - |
| <span data-ttu-id="3ef08-140">图像</span><span class="sxs-lookup"><span data-stu-id="3ef08-140">Image</span></span>  | <span data-ttu-id="3ef08-141">ac-image</span><span class="sxs-lookup"><span data-stu-id="3ef08-141">ac-image</span></span> |
| <span data-ttu-id="3ef08-142">ImageSet</span><span class="sxs-lookup"><span data-stu-id="3ef08-142">ImageSet</span></span>  | <span data-ttu-id="3ef08-143">ac-imageset</span><span class="sxs-lookup"><span data-stu-id="3ef08-143">ac-imageset</span></span> |
| <span data-ttu-id="3ef08-144">FactSet</span><span class="sxs-lookup"><span data-stu-id="3ef08-144">FactSet</span></span> | <span data-ttu-id="3ef08-145">ac-factset</span><span class="sxs-lookup"><span data-stu-id="3ef08-145">ac-factset</span></span> |
| <span data-ttu-id="3ef08-146">TextBlock</span><span class="sxs-lookup"><span data-stu-id="3ef08-146">TextBlock</span></span>  | <span data-ttu-id="3ef08-147">ac-textblock</span><span class="sxs-lookup"><span data-stu-id="3ef08-147">ac-textblock</span></span> |