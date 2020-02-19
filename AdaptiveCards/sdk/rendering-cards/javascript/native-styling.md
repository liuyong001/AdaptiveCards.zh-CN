---
title: 本机样式设置-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 687a90dd572ba2df786816fdd9dc313746cca982
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454640"
---
# <a name="native-styling---javascript"></a><span data-ttu-id="9554d-102">本机样式设置-JavaScript</span><span class="sxs-lookup"><span data-stu-id="9554d-102">Native styling - JavaScript</span></span>

<span data-ttu-id="9554d-103">使用 CSS 对卡片 HTML 进行精细的样式设置。</span><span class="sxs-lookup"><span data-stu-id="9554d-103">Use CSS for fine-grained styling of the card HTML.</span></span>

<span data-ttu-id="9554d-104">以下 CSS 类将添加到各种元素。</span><span class="sxs-lookup"><span data-stu-id="9554d-104">The following CSS classes will be added to various elements.</span></span>

| <span data-ttu-id="9554d-105">CSS 类</span><span class="sxs-lookup"><span data-stu-id="9554d-105">CSS class</span></span> | <span data-ttu-id="9554d-106">用法</span><span class="sxs-lookup"><span data-stu-id="9554d-106">Usage</span></span> |
|---|---|
| <span data-ttu-id="9554d-107">.ac-container</span><span class="sxs-lookup"><span data-stu-id="9554d-107">.ac-container</span></span> | <span data-ttu-id="9554d-108">容器</span><span class="sxs-lookup"><span data-stu-id="9554d-108">containers</span></span> |
| <span data-ttu-id="9554d-109">. 交流电-可选</span><span class="sxs-lookup"><span data-stu-id="9554d-109">.ac-selectable</span></span>  | <span data-ttu-id="9554d-110">具有 `selectAction` 的元素</span><span class="sxs-lookup"><span data-stu-id="9554d-110">elements with `selectAction`</span></span> |
| <span data-ttu-id="9554d-111">.ac-image</span><span class="sxs-lookup"><span data-stu-id="9554d-111">.ac-image</span></span> | <span data-ttu-id="9554d-112">图像</span><span class="sxs-lookup"><span data-stu-id="9554d-112">image</span></span> |
| <span data-ttu-id="9554d-113">.ac-pushButton</span><span class="sxs-lookup"><span data-stu-id="9554d-113">.ac-pushButton</span></span> | <span data-ttu-id="9554d-114">呈现的操作类似于按钮</span><span class="sxs-lookup"><span data-stu-id="9554d-114">actions rendered like buttons</span></span> |
| <span data-ttu-id="9554d-115">.ac-linkButton</span><span class="sxs-lookup"><span data-stu-id="9554d-115">.ac-linkButton</span></span>  | <span data-ttu-id="9554d-116">呈现的操作，如链接</span><span class="sxs-lookup"><span data-stu-id="9554d-116">actions rendered like links</span></span> |
| <span data-ttu-id="9554d-117">.ac-input</span><span class="sxs-lookup"><span data-stu-id="9554d-117">.ac-input</span></span> | <span data-ttu-id="9554d-118">输入控件</span><span class="sxs-lookup"><span data-stu-id="9554d-118">input controls</span></span>|
| <span data-ttu-id="9554d-119">.ac-textInput</span><span class="sxs-lookup"><span data-stu-id="9554d-119">.ac-textInput</span></span>| <span data-ttu-id="9554d-120">文本输入</span><span class="sxs-lookup"><span data-stu-id="9554d-120">text input</span></span> |
| <span data-ttu-id="9554d-121">.ac-multiline</span><span class="sxs-lookup"><span data-stu-id="9554d-121">.ac-multiline</span></span> | <span data-ttu-id="9554d-122">多行文本输入</span><span class="sxs-lookup"><span data-stu-id="9554d-122">multiline text input</span></span> |
| <span data-ttu-id="9554d-123">.ac-numberInput</span><span class="sxs-lookup"><span data-stu-id="9554d-123">.ac-numberInput</span></span> | <span data-ttu-id="9554d-124">数字输入</span><span class="sxs-lookup"><span data-stu-id="9554d-124">number input</span></span>|
| <span data-ttu-id="9554d-125">.ac-dateInput</span><span class="sxs-lookup"><span data-stu-id="9554d-125">.ac-dateInput</span></span> | <span data-ttu-id="9554d-126">日期输入</span><span class="sxs-lookup"><span data-stu-id="9554d-126">date input</span></span>|
| <span data-ttu-id="9554d-127">.ac-timeInput</span><span class="sxs-lookup"><span data-stu-id="9554d-127">.ac-timeInput</span></span> | <span data-ttu-id="9554d-128">时间输入</span><span class="sxs-lookup"><span data-stu-id="9554d-128">time input</span></span> |
| <span data-ttu-id="9554d-129">.ac-multichoiceInput</span><span class="sxs-lookup"><span data-stu-id="9554d-129">.ac-multichoiceInput</span></span> | <span data-ttu-id="9554d-130">multichoice 输入</span><span class="sxs-lookup"><span data-stu-id="9554d-130">multichoice input</span></span>|