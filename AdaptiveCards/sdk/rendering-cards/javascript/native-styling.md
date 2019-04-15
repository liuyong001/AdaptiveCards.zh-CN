---
title: 本机样式-JavaScript SDK
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
# <a name="native-styling---javascript"></a><span data-ttu-id="f7a17-102">本机样式-JavaScript</span><span class="sxs-lookup"><span data-stu-id="f7a17-102">Native styling - JavaScript</span></span>

<span data-ttu-id="f7a17-103">使用 CSS 进行细粒度的卡 HTML 样式。</span><span class="sxs-lookup"><span data-stu-id="f7a17-103">Use CSS for fine-grained styling of the card HTML.</span></span>

<span data-ttu-id="f7a17-104">以下的 CSS 类将添加到各种元素。</span><span class="sxs-lookup"><span data-stu-id="f7a17-104">The following CSS classes will be added to various elements.</span></span>

| <span data-ttu-id="f7a17-105">CSS 类</span><span class="sxs-lookup"><span data-stu-id="f7a17-105">CSS class</span></span> | <span data-ttu-id="f7a17-106">用法</span><span class="sxs-lookup"><span data-stu-id="f7a17-106">Usage</span></span> |
|---|---|
| <span data-ttu-id="f7a17-107">.ac-container</span><span class="sxs-lookup"><span data-stu-id="f7a17-107">.ac-container</span></span> | <span data-ttu-id="f7a17-108">容器</span><span class="sxs-lookup"><span data-stu-id="f7a17-108">containers</span></span> |
| <span data-ttu-id="f7a17-109">.ac-selectable</span><span class="sxs-lookup"><span data-stu-id="f7a17-109">.ac-selectable</span></span>  | <span data-ttu-id="f7a17-110">具有的元素 `selectAction`</span><span class="sxs-lookup"><span data-stu-id="f7a17-110">elements with `selectAction`</span></span> |
| <span data-ttu-id="f7a17-111">.ac-image</span><span class="sxs-lookup"><span data-stu-id="f7a17-111">.ac-image</span></span> | <span data-ttu-id="f7a17-112">image</span><span class="sxs-lookup"><span data-stu-id="f7a17-112">image</span></span> |
| <span data-ttu-id="f7a17-113">.ac-pushButton</span><span class="sxs-lookup"><span data-stu-id="f7a17-113">.ac-pushButton</span></span> | <span data-ttu-id="f7a17-114">呈现按钮等的操作</span><span class="sxs-lookup"><span data-stu-id="f7a17-114">actions rendered like buttons</span></span> |
| <span data-ttu-id="f7a17-115">.ac-linkButton</span><span class="sxs-lookup"><span data-stu-id="f7a17-115">.ac-linkButton</span></span>  | <span data-ttu-id="f7a17-116">呈现链接等操作</span><span class="sxs-lookup"><span data-stu-id="f7a17-116">actions rendered like links</span></span> |
| <span data-ttu-id="f7a17-117">.ac-input</span><span class="sxs-lookup"><span data-stu-id="f7a17-117">.ac-input</span></span> | <span data-ttu-id="f7a17-118">输入的控件</span><span class="sxs-lookup"><span data-stu-id="f7a17-118">input controls</span></span>|
| <span data-ttu-id="f7a17-119">.ac-textInput</span><span class="sxs-lookup"><span data-stu-id="f7a17-119">.ac-textInput</span></span>| <span data-ttu-id="f7a17-120">文本输入</span><span class="sxs-lookup"><span data-stu-id="f7a17-120">text input</span></span> |
| <span data-ttu-id="f7a17-121">.ac-multiline</span><span class="sxs-lookup"><span data-stu-id="f7a17-121">.ac-multiline</span></span> | <span data-ttu-id="f7a17-122">多行文本输入</span><span class="sxs-lookup"><span data-stu-id="f7a17-122">multiline text input</span></span> |
| <span data-ttu-id="f7a17-123">.ac-numberInput</span><span class="sxs-lookup"><span data-stu-id="f7a17-123">.ac-numberInput</span></span> | <span data-ttu-id="f7a17-124">数字输入</span><span class="sxs-lookup"><span data-stu-id="f7a17-124">number input</span></span>|
| <span data-ttu-id="f7a17-125">.ac-dateInput</span><span class="sxs-lookup"><span data-stu-id="f7a17-125">.ac-dateInput</span></span> | <span data-ttu-id="f7a17-126">日期输入</span><span class="sxs-lookup"><span data-stu-id="f7a17-126">date input</span></span>|
| <span data-ttu-id="f7a17-127">.ac-timeInput</span><span class="sxs-lookup"><span data-stu-id="f7a17-127">.ac-timeInput</span></span> | <span data-ttu-id="f7a17-128">时间输入</span><span class="sxs-lookup"><span data-stu-id="f7a17-128">time input</span></span> |
| <span data-ttu-id="f7a17-129">.ac-multichoiceInput</span><span class="sxs-lookup"><span data-stu-id="f7a17-129">.ac-multichoiceInput</span></span> | <span data-ttu-id="f7a17-130">单选输入</span><span class="sxs-lookup"><span data-stu-id="f7a17-130">multichoice input</span></span>|