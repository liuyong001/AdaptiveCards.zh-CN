---
title: 本机样式-iOS SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: f9ed839a19ac778381fa36361ad37e95b7ab5e08
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2020
ms.locfileid: "76727468"
---
# <a name="native-styling---ios"></a><span data-ttu-id="03d0d-102">本机样式-iOS</span><span class="sxs-lookup"><span data-stu-id="03d0d-102">Native styling - iOS</span></span>

<span data-ttu-id="03d0d-103">使用 XIB 进行精细的样式设置。</span><span class="sxs-lookup"><span data-stu-id="03d0d-103">Use XIB for fine-grained styling.</span></span>

<span data-ttu-id="03d0d-104">存在以下 Xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-104">The following XIBs exist</span></span>

| <span data-ttu-id="03d0d-105">XIB</span><span class="sxs-lookup"><span data-stu-id="03d0d-105">XIB</span></span> | <span data-ttu-id="03d0d-106">사용 패턴</span><span class="sxs-lookup"><span data-stu-id="03d0d-106">Usage</span></span> |
|---|---|
| <span data-ttu-id="03d0d-107">ACRButton. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-107">ACRButton.xib</span></span> | <span data-ttu-id="03d0d-108">按钮</span><span class="sxs-lookup"><span data-stu-id="03d0d-108">buttons</span></span> |
| <span data-ttu-id="03d0d-109">ACRCellForCompactMode. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-109">ACRCellForCompactMode.xib</span></span>   | <span data-ttu-id="03d0d-110">ChoiceSet compact 模式</span><span class="sxs-lookup"><span data-stu-id="03d0d-110">ChoiceSet compact mode</span></span>|
| <span data-ttu-id="03d0d-111">ACRDatePicker. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-111">ACRDatePicker.xib</span></span> | <span data-ttu-id="03d0d-112">DatePicker 的输入日期</span><span class="sxs-lookup"><span data-stu-id="03d0d-112">DatePicker for Input.Date</span></span> |
| <span data-ttu-id="03d0d-113">ACRDateTextField. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-113">ACRDateTextField.xib</span></span>  | <span data-ttu-id="03d0d-114">输入的文本字段。日期</span><span class="sxs-lookup"><span data-stu-id="03d0d-114">TextField for Input.Date</span></span> |
| <span data-ttu-id="03d0d-115">ACRInputTableView. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-115">ACRInputTableView.xib</span></span>   | <span data-ttu-id="03d0d-116">输入的容器</span><span class="sxs-lookup"><span data-stu-id="03d0d-116">Container for Inputs</span></span> |
| <span data-ttu-id="03d0d-117">ACRLabelView. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-117">ACRLabelView.xib</span></span>  | <span data-ttu-id="03d0d-118">TextBlock</span><span class="sxs-lookup"><span data-stu-id="03d0d-118">TextBlock</span></span> |
| <span data-ttu-id="03d0d-119">ACRPickerView. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-119">ACRPickerView.xib</span></span> | <span data-ttu-id="03d0d-120">ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="03d0d-120">ChoiceSet</span></span> |
| <span data-ttu-id="03d0d-121">ACRQuickActionMultilineView. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-121">ACRQuickActionMultilineView.xib</span></span>  | <span data-ttu-id="03d0d-122">Multilines 的快速操作</span><span class="sxs-lookup"><span data-stu-id="03d0d-122">Quick Actions with multilines</span></span> |
| <span data-ttu-id="03d0d-123">ACRQuickActionView. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-123">ACRQuickActionView.xib</span></span> | <span data-ttu-id="03d0d-124">快速操作</span><span class="sxs-lookup"><span data-stu-id="03d0d-124">Quick Actions</span></span> |
| <span data-ttu-id="03d0d-125">ACRTextField. xib</span><span class="sxs-lookup"><span data-stu-id="03d0d-125">ACRTextField.xib</span></span> | <span data-ttu-id="03d0d-126">입력</span><span class="sxs-lookup"><span data-stu-id="03d0d-126">Input</span></span> |

<span data-ttu-id="03d0d-127">可以通过 XCode IB 编辑 XIB。</span><span class="sxs-lookup"><span data-stu-id="03d0d-127">XIB can be edited through XCode IB.</span></span>
<span data-ttu-id="03d0d-128">将 Xib 编辑为规范后。</span><span class="sxs-lookup"><span data-stu-id="03d0d-128">Once XIBs are edited to the specification.</span></span>
<span data-ttu-id="03d0d-129">从终端</span><span class="sxs-lookup"><span data-stu-id="03d0d-129">From a terminal</span></span>
```
ibtool --compile name.nib name.xib 
```

<span data-ttu-id="03d0d-130">例如，若要对按钮进行样式</span><span class="sxs-lookup"><span data-stu-id="03d0d-130">For example, to style a button</span></span>
```
ibtool --compile ACRButton.nib ACRButton.xib 
```

<span data-ttu-id="03d0d-131">然后，可以在 AdaptiveCards 替换生成的笔尖文件</span><span class="sxs-lookup"><span data-stu-id="03d0d-131">The generated nib files can be then replaced at AdaptiveCards.framework</span></span>
