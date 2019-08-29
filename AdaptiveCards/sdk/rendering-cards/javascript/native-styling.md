---
title: 本机样式设置-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 6f086d268abcaeb7fa159b74708597e89aafaf53
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552889"
---
# <a name="native-styling---javascript"></a><span data-ttu-id="513fc-102">本机样式设置-JavaScript</span><span class="sxs-lookup"><span data-stu-id="513fc-102">Native styling - JavaScript</span></span>

<span data-ttu-id="513fc-103">使用 CSS 对卡片 HTML 进行精细的样式设置。</span><span class="sxs-lookup"><span data-stu-id="513fc-103">Use CSS for fine-grained styling of the card HTML.</span></span>

<span data-ttu-id="513fc-104">以下 CSS 类将添加到各种元素。</span><span class="sxs-lookup"><span data-stu-id="513fc-104">The following CSS classes will be added to various elements.</span></span>

| <span data-ttu-id="513fc-105">CSS 类</span><span class="sxs-lookup"><span data-stu-id="513fc-105">CSS class</span></span> | <span data-ttu-id="513fc-106">用法</span><span class="sxs-lookup"><span data-stu-id="513fc-106">Usage</span></span> |
|---|---|
| <span data-ttu-id="513fc-107">.ac-container</span><span class="sxs-lookup"><span data-stu-id="513fc-107">.ac-container</span></span> | <span data-ttu-id="513fc-108">存放</span><span class="sxs-lookup"><span data-stu-id="513fc-108">containers</span></span> |
| <span data-ttu-id="513fc-109">. 交流电-可选</span><span class="sxs-lookup"><span data-stu-id="513fc-109">.ac-selectable</span></span>  | <span data-ttu-id="513fc-110">元素与`selectAction`</span><span class="sxs-lookup"><span data-stu-id="513fc-110">elements with `selectAction`</span></span> |
| <span data-ttu-id="513fc-111">.ac-image</span><span class="sxs-lookup"><span data-stu-id="513fc-111">.ac-image</span></span> | <span data-ttu-id="513fc-112">image</span><span class="sxs-lookup"><span data-stu-id="513fc-112">image</span></span> |
| <span data-ttu-id="513fc-113">.ac-pushButton</span><span class="sxs-lookup"><span data-stu-id="513fc-113">.ac-pushButton</span></span> | <span data-ttu-id="513fc-114">呈现的操作类似于按钮</span><span class="sxs-lookup"><span data-stu-id="513fc-114">actions rendered like buttons</span></span> |
| <span data-ttu-id="513fc-115">.ac-linkButton</span><span class="sxs-lookup"><span data-stu-id="513fc-115">.ac-linkButton</span></span>  | <span data-ttu-id="513fc-116">呈现的操作, 如链接</span><span class="sxs-lookup"><span data-stu-id="513fc-116">actions rendered like links</span></span> |
| <span data-ttu-id="513fc-117">.ac-input</span><span class="sxs-lookup"><span data-stu-id="513fc-117">.ac-input</span></span> | <span data-ttu-id="513fc-118">输入控件</span><span class="sxs-lookup"><span data-stu-id="513fc-118">input controls</span></span>|
| <span data-ttu-id="513fc-119">.ac-textInput</span><span class="sxs-lookup"><span data-stu-id="513fc-119">.ac-textInput</span></span>| <span data-ttu-id="513fc-120">文本输入</span><span class="sxs-lookup"><span data-stu-id="513fc-120">text input</span></span> |
| <span data-ttu-id="513fc-121">.ac-multiline</span><span class="sxs-lookup"><span data-stu-id="513fc-121">.ac-multiline</span></span> | <span data-ttu-id="513fc-122">多行文本输入</span><span class="sxs-lookup"><span data-stu-id="513fc-122">multiline text input</span></span> |
| <span data-ttu-id="513fc-123">.ac-numberInput</span><span class="sxs-lookup"><span data-stu-id="513fc-123">.ac-numberInput</span></span> | <span data-ttu-id="513fc-124">数字输入</span><span class="sxs-lookup"><span data-stu-id="513fc-124">number input</span></span>|
| <span data-ttu-id="513fc-125">.ac-dateInput</span><span class="sxs-lookup"><span data-stu-id="513fc-125">.ac-dateInput</span></span> | <span data-ttu-id="513fc-126">日期输入</span><span class="sxs-lookup"><span data-stu-id="513fc-126">date input</span></span>|
| <span data-ttu-id="513fc-127">.ac-timeInput</span><span class="sxs-lookup"><span data-stu-id="513fc-127">.ac-timeInput</span></span> | <span data-ttu-id="513fc-128">时间输入</span><span class="sxs-lookup"><span data-stu-id="513fc-128">time input</span></span> |
| <span data-ttu-id="513fc-129">.ac-multichoiceInput</span><span class="sxs-lookup"><span data-stu-id="513fc-129">.ac-multichoiceInput</span></span> | <span data-ttu-id="513fc-130">multichoice 输入</span><span class="sxs-lookup"><span data-stu-id="513fc-130">multichoice input</span></span>|