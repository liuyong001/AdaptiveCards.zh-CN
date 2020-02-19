---
title: 本机样式 .NET WPF SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: 204845f942be4e7d04e20e9cd64d826daef26e93
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454020"
---
# <a name="native-styling---net-wpf"></a><span data-ttu-id="facb3-102">本机样式设置-.NET WPF</span><span class="sxs-lookup"><span data-stu-id="facb3-102">Native styling - .NET WPF</span></span>

<span data-ttu-id="facb3-103">虽然主机配置在每个平台上都可获得大多数方法，但你可能需要在每个平台上执行一些本机样式。</span><span class="sxs-lookup"><span data-stu-id="facb3-103">While Host Config will get you most of the way there on each platform, it's likely that you will have to do some native styling on each platform.</span></span> 

<span data-ttu-id="facb3-104">WPF 通过允许您传递 ResourceDictionary 以实现精细的样式、行为、动画等，从而使其变得简单。</span><span class="sxs-lookup"><span data-stu-id="facb3-104">WPF makes this easy by allowing you to pass a ResourceDictionary for fine-grained styling, behavior, animations, etc.</span></span>

| <span data-ttu-id="facb3-105">元素</span><span class="sxs-lookup"><span data-stu-id="facb3-105">Element</span></span> | <span data-ttu-id="facb3-106">样式名称</span><span class="sxs-lookup"><span data-stu-id="facb3-106">Style names</span></span> |
|---|---|
| <span data-ttu-id="facb3-107">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="facb3-107">AdaptiveCard</span></span> | <span data-ttu-id="facb3-108">Adaptive.Card</span><span class="sxs-lookup"><span data-stu-id="facb3-108">Adaptive.Card</span></span>| 
| <span data-ttu-id="facb3-109">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="facb3-109">Action.OpenUrl</span></span>  | <span data-ttu-id="facb3-110">Adaptive.Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="facb3-110">Adaptive.Action.OpenUrl</span></span>  |
| <span data-ttu-id="facb3-111">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="facb3-111">Action.ShowCard</span></span> | <span data-ttu-id="facb3-112">Adaptive.Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="facb3-112">Adaptive.Action.ShowCard</span></span> |
| <span data-ttu-id="facb3-113">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="facb3-113">Action.Submit</span></span>  | <span data-ttu-id="facb3-114">Adaptive.Action.Submit</span><span class="sxs-lookup"><span data-stu-id="facb3-114">Adaptive.Action.Submit</span></span>  |
| <span data-ttu-id="facb3-115">列</span><span class="sxs-lookup"><span data-stu-id="facb3-115">Column</span></span> | <span data-ttu-id="facb3-116">自适应. 列，自适应。</span><span class="sxs-lookup"><span data-stu-id="facb3-116">Adaptive.Column, Adaptive.Action.Tap</span></span> |
| <span data-ttu-id="facb3-117">ColumnSet</span><span class="sxs-lookup"><span data-stu-id="facb3-117">ColumnSet</span></span> | <span data-ttu-id="facb3-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span><span class="sxs-lookup"><span data-stu-id="facb3-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span></span> |
| <span data-ttu-id="facb3-119">容器</span><span class="sxs-lookup"><span data-stu-id="facb3-119">Container</span></span> | <span data-ttu-id="facb3-120">Adaptive.Container</span><span class="sxs-lookup"><span data-stu-id="facb3-120">Adaptive.Container</span></span>|
| <span data-ttu-id="facb3-121">Input.ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="facb3-121">Input.ChoiceSet</span></span> | <span data-ttu-id="facb3-122">ChoiceSet、ChoiceSet、ChoiceSet、ChoiceSet、、ChoiceSet、ComboBoxItem、、、、、、。</span><span class="sxs-lookup"><span data-stu-id="facb3-122">Adaptive.Input.ChoiceSet,  Adaptive.Input.ChoiceSet.ComboBox, Adaptive.Input.ChoiceSet.CheckBox,  Adaptive.Input.ChoiceSet.Radio,  Adaptive.Input.ChoiceSet.ComboBoxItem</span></span> |
| <span data-ttu-id="facb3-123">Input.Date</span><span class="sxs-lookup"><span data-stu-id="facb3-123">Input.Date</span></span> | <span data-ttu-id="facb3-124">Adaptive.Input.Text.Date</span><span class="sxs-lookup"><span data-stu-id="facb3-124">Adaptive.Input.Text.Date</span></span>
| <span data-ttu-id="facb3-125">Input.Number</span><span class="sxs-lookup"><span data-stu-id="facb3-125">Input.Number</span></span> | <span data-ttu-id="facb3-126">Adaptive.Input.Text.Number</span><span class="sxs-lookup"><span data-stu-id="facb3-126">Adaptive.Input.Text.Number</span></span> |
| <span data-ttu-id="facb3-127">Input.Text</span><span class="sxs-lookup"><span data-stu-id="facb3-127">Input.Text</span></span> | <span data-ttu-id="facb3-128">Adaptive.Input.Text</span><span class="sxs-lookup"><span data-stu-id="facb3-128">Adaptive.Input.Text</span></span> |
| <span data-ttu-id="facb3-129">Input.Time</span><span class="sxs-lookup"><span data-stu-id="facb3-129">Input.Time</span></span> | <span data-ttu-id="facb3-130">Adaptive.Input.Text.Time</span><span class="sxs-lookup"><span data-stu-id="facb3-130">Adaptive.Input.Text.Time</span></span> |
| <span data-ttu-id="facb3-131">Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="facb3-131">Input.Toggle</span></span>| <span data-ttu-id="facb3-132">Adaptive.Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="facb3-132">Adaptive.Input.Toggle</span></span>|
| <span data-ttu-id="facb3-133">映像</span><span class="sxs-lookup"><span data-stu-id="facb3-133">Image</span></span>  | <span data-ttu-id="facb3-134">Adaptive.Image</span><span class="sxs-lookup"><span data-stu-id="facb3-134">Adaptive.Image</span></span> |
| <span data-ttu-id="facb3-135">ImageSet</span><span class="sxs-lookup"><span data-stu-id="facb3-135">ImageSet</span></span>  | <span data-ttu-id="facb3-136">Adaptive.ImageSet</span><span class="sxs-lookup"><span data-stu-id="facb3-136">Adaptive.ImageSet</span></span> |
| <span data-ttu-id="facb3-137">FactSet</span><span class="sxs-lookup"><span data-stu-id="facb3-137">FactSet</span></span> | <span data-ttu-id="facb3-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span><span class="sxs-lookup"><span data-stu-id="facb3-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span></span> |
| <span data-ttu-id="facb3-139">TextBlock</span><span class="sxs-lookup"><span data-stu-id="facb3-139">TextBlock</span></span>  | <span data-ttu-id="facb3-140">Adaptive.TextBlock</span><span class="sxs-lookup"><span data-stu-id="facb3-140">Adaptive.TextBlock</span></span> |

<span data-ttu-id="facb3-141">此示例 XAML 资源字典，它将所有 Textblock 的背景设置为浅绿色。</span><span class="sxs-lookup"><span data-stu-id="facb3-141">This sample XAML Resource dictionary that sets the background of all TextBlocks to Aqua.</span></span> <span data-ttu-id="facb3-142">你可能希望比此 😁 更高级的内容</span><span class="sxs-lookup"><span data-stu-id="facb3-142">You will probably want something more advanced than this 😁</span></span>

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

// ... or load it from a file path
// USE this if rendering from a server
renderer.ResourcesPath = <path-to-my-resource-dictionary.xaml>;
```

> [!IMPORTANT]
> <span data-ttu-id="facb3-143">**有关服务器端映像生成的说明**WPF 呈现器提供可用于生成服务器端映像的 `RenderCardToImageAsync` 方法。</span><span class="sxs-lookup"><span data-stu-id="facb3-143">**A note about server-side image generation** The WPF renderer provides a `RenderCardToImageAsync` method that can be used for server-side image generation.</span></span> <span data-ttu-id="facb3-144">仅在此环境中使用时，才能使用 `ResourcesPath` 属性。</span><span class="sxs-lookup"><span data-stu-id="facb3-144">You must only use the `ResourcesPath` property if used in this environment.</span></span> <span data-ttu-id="facb3-145">有关详细信息，请参阅[图像呈现](../net-image/getting-started.md)文档</span><span class="sxs-lookup"><span data-stu-id="facb3-145">See the [Image Rendering](../net-image/getting-started.md) docs for more</span></span>