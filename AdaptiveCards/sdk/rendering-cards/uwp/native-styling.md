---
title: 本机样式-UWP SDK
author: matthidinger
ms.author: mahiding
ms.date: 08/15/2018
ms.topic: article
ms.openlocfilehash: da3b95dc53c55c81fbbbbed6ee7605f86eb427a9
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552519"
---
# <a name="native-styling---uwp"></a><span data-ttu-id="1e6dc-102">本机样式-UWP</span><span class="sxs-lookup"><span data-stu-id="1e6dc-102">Native styling - UWP</span></span>

<span data-ttu-id="1e6dc-103">尽管主机配置可以帮助您了解大多数的方式有每个平台上，很可能您将只需在每个平台上的某些本机样式设置。</span><span class="sxs-lookup"><span data-stu-id="1e6dc-103">While Host Config will get you most of the way there on each platform, it's likely that you will have to do some native styling on each platform.</span></span> 

<span data-ttu-id="1e6dc-104">UWP 来实现轻松这允许将传入 ResourceDictionary 细粒度的样式设置、 行为、 动画等。</span><span class="sxs-lookup"><span data-stu-id="1e6dc-104">UWP makes this easy by allowing you to pass a ResourceDictionary for fine-grained styling, behavior, animations, etc.</span></span>

| <span data-ttu-id="1e6dc-105">元素</span><span class="sxs-lookup"><span data-stu-id="1e6dc-105">Element</span></span> | <span data-ttu-id="1e6dc-106">样式名称：</span><span class="sxs-lookup"><span data-stu-id="1e6dc-106">Style names</span></span> |
|---|---|
| <span data-ttu-id="1e6dc-107">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="1e6dc-107">AdaptiveCard</span></span> | <span data-ttu-id="1e6dc-108">Adaptive.Card</span><span class="sxs-lookup"><span data-stu-id="1e6dc-108">Adaptive.Card</span></span>| 
| <span data-ttu-id="1e6dc-109">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="1e6dc-109">Action.OpenUrl</span></span>  | <span data-ttu-id="1e6dc-110">Adaptive.Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="1e6dc-110">Adaptive.Action.OpenUrl</span></span>  |
| <span data-ttu-id="1e6dc-111">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="1e6dc-111">Action.ShowCard</span></span> | <span data-ttu-id="1e6dc-112">Adaptive.Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="1e6dc-112">Adaptive.Action.ShowCard</span></span> |
| <span data-ttu-id="1e6dc-113">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="1e6dc-113">Action.Submit</span></span>  | <span data-ttu-id="1e6dc-114">Adaptive.Action.Submit</span><span class="sxs-lookup"><span data-stu-id="1e6dc-114">Adaptive.Action.Submit</span></span>  |
| <span data-ttu-id="1e6dc-115">列</span><span class="sxs-lookup"><span data-stu-id="1e6dc-115">Column</span></span> | <span data-ttu-id="1e6dc-116">Adaptive.Column, Adaptive.Action.Tap</span><span class="sxs-lookup"><span data-stu-id="1e6dc-116">Adaptive.Column, Adaptive.Action.Tap</span></span> |
| <span data-ttu-id="1e6dc-117">ColumnSet</span><span class="sxs-lookup"><span data-stu-id="1e6dc-117">ColumnSet</span></span> | <span data-ttu-id="1e6dc-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span><span class="sxs-lookup"><span data-stu-id="1e6dc-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span></span> |
| <span data-ttu-id="1e6dc-119">容器</span><span class="sxs-lookup"><span data-stu-id="1e6dc-119">Container</span></span> | <span data-ttu-id="1e6dc-120">Adaptive.Container</span><span class="sxs-lookup"><span data-stu-id="1e6dc-120">Adaptive.Container</span></span>|
| <span data-ttu-id="1e6dc-121">Input.ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="1e6dc-121">Input.ChoiceSet</span></span> | <span data-ttu-id="1e6dc-122">Adaptive.Input.ChoiceSet,  Adaptive.Input.ChoiceSet.ComboBox, Adaptive.Input.ChoiceSet.CheckBox,  Adaptive.Input.ChoiceSet.Radio,  Adaptive.Input.ChoiceSet.ComboBoxItem</span><span class="sxs-lookup"><span data-stu-id="1e6dc-122">Adaptive.Input.ChoiceSet,  Adaptive.Input.ChoiceSet.ComboBox, Adaptive.Input.ChoiceSet.CheckBox,  Adaptive.Input.ChoiceSet.Radio,  Adaptive.Input.ChoiceSet.ComboBoxItem</span></span> |
| <span data-ttu-id="1e6dc-123">Input.Date</span><span class="sxs-lookup"><span data-stu-id="1e6dc-123">Input.Date</span></span> | <span data-ttu-id="1e6dc-124">Adaptive.Input.Text.Date</span><span class="sxs-lookup"><span data-stu-id="1e6dc-124">Adaptive.Input.Text.Date</span></span>
| <span data-ttu-id="1e6dc-125">Input.Number</span><span class="sxs-lookup"><span data-stu-id="1e6dc-125">Input.Number</span></span> | <span data-ttu-id="1e6dc-126">Adaptive.Input.Text.Number</span><span class="sxs-lookup"><span data-stu-id="1e6dc-126">Adaptive.Input.Text.Number</span></span> |
| <span data-ttu-id="1e6dc-127">Input.Text</span><span class="sxs-lookup"><span data-stu-id="1e6dc-127">Input.Text</span></span> | <span data-ttu-id="1e6dc-128">Adaptive.Input.Text</span><span class="sxs-lookup"><span data-stu-id="1e6dc-128">Adaptive.Input.Text</span></span> |
| <span data-ttu-id="1e6dc-129">Input.Time</span><span class="sxs-lookup"><span data-stu-id="1e6dc-129">Input.Time</span></span> | <span data-ttu-id="1e6dc-130">Adaptive.Input.Text.Time</span><span class="sxs-lookup"><span data-stu-id="1e6dc-130">Adaptive.Input.Text.Time</span></span> |
| <span data-ttu-id="1e6dc-131">Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="1e6dc-131">Input.Toggle</span></span>| <span data-ttu-id="1e6dc-132">Adaptive.Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="1e6dc-132">Adaptive.Input.Toggle</span></span>|
| <span data-ttu-id="1e6dc-133">图像</span><span class="sxs-lookup"><span data-stu-id="1e6dc-133">Image</span></span>  | <span data-ttu-id="1e6dc-134">Adaptive.Image</span><span class="sxs-lookup"><span data-stu-id="1e6dc-134">Adaptive.Image</span></span> |
| <span data-ttu-id="1e6dc-135">ImageSet</span><span class="sxs-lookup"><span data-stu-id="1e6dc-135">ImageSet</span></span>  | <span data-ttu-id="1e6dc-136">Adaptive.ImageSet</span><span class="sxs-lookup"><span data-stu-id="1e6dc-136">Adaptive.ImageSet</span></span> |
| <span data-ttu-id="1e6dc-137">FactSet</span><span class="sxs-lookup"><span data-stu-id="1e6dc-137">FactSet</span></span> | <span data-ttu-id="1e6dc-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span><span class="sxs-lookup"><span data-stu-id="1e6dc-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span></span> |
| <span data-ttu-id="1e6dc-139">TextBlock</span><span class="sxs-lookup"><span data-stu-id="1e6dc-139">TextBlock</span></span>  | <span data-ttu-id="1e6dc-140">Adaptive.TextBlock</span><span class="sxs-lookup"><span data-stu-id="1e6dc-140">Adaptive.TextBlock</span></span> |

<span data-ttu-id="1e6dc-141">此示例 XAML 资源字典，其中所有 Textblock 的背景设置为浅绿色。</span><span class="sxs-lookup"><span data-stu-id="1e6dc-141">This sample XAML Resource dictionary that sets the background of all TextBlocks to Aqua.</span></span> <span data-ttu-id="1e6dc-142">您可能希望某些比这更高级 😁</span><span class="sxs-lookup"><span data-stu-id="1e6dc-142">You will probably want something more advanced than this 😁</span></span>

```xml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" 
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <Style x:Key="Adaptive.TextBlock" TargetType="TextBlock">
        <Setter Property="Background" Value="Aqua"></Setter>
    </Style>
</ResourceDictionary>
```
```csharp
// Use a ResourceDictionary instance
// DON'T use this property if rendering from a server
renderer.Resources = myResourceDictionary;
```
