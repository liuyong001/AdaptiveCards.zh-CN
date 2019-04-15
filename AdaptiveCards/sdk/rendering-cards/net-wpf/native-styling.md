---
title: 本机样式的.NET WPF SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: ee5bec1a11f39ad69d40e57410c105b50ba45981
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552719"
---
# <a name="native-styling---net-wpf"></a><span data-ttu-id="fef9a-102">本机样式的.NET WPF</span><span class="sxs-lookup"><span data-stu-id="fef9a-102">Native styling - .NET WPF</span></span>

<span data-ttu-id="fef9a-103">尽管主机配置可以帮助您了解大多数的方式有每个平台上，很可能您将只需在每个平台上的某些本机样式设置。</span><span class="sxs-lookup"><span data-stu-id="fef9a-103">While Host Config will get you most of the way there on each platform, it's likely that you will have to do some native styling on each platform.</span></span> 

<span data-ttu-id="fef9a-104">WPF 来实现轻松这允许将传入 ResourceDictionary 细粒度的样式设置、 行为、 动画等。</span><span class="sxs-lookup"><span data-stu-id="fef9a-104">WPF makes this easy by allowing you to pass a ResourceDictionary for fine-grained styling, behavior, animations, etc.</span></span>

| <span data-ttu-id="fef9a-105">元素</span><span class="sxs-lookup"><span data-stu-id="fef9a-105">Element</span></span> | <span data-ttu-id="fef9a-106">样式名称：</span><span class="sxs-lookup"><span data-stu-id="fef9a-106">Style names</span></span> |
|---|---|
| <span data-ttu-id="fef9a-107">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="fef9a-107">AdaptiveCard</span></span> | <span data-ttu-id="fef9a-108">Adaptive.Card</span><span class="sxs-lookup"><span data-stu-id="fef9a-108">Adaptive.Card</span></span>| 
| <span data-ttu-id="fef9a-109">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="fef9a-109">Action.OpenUrl</span></span>  | <span data-ttu-id="fef9a-110">Adaptive.Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="fef9a-110">Adaptive.Action.OpenUrl</span></span>  |
| <span data-ttu-id="fef9a-111">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="fef9a-111">Action.ShowCard</span></span> | <span data-ttu-id="fef9a-112">Adaptive.Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="fef9a-112">Adaptive.Action.ShowCard</span></span> |
| <span data-ttu-id="fef9a-113">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="fef9a-113">Action.Submit</span></span>  | <span data-ttu-id="fef9a-114">Adaptive.Action.Submit</span><span class="sxs-lookup"><span data-stu-id="fef9a-114">Adaptive.Action.Submit</span></span>  |
| <span data-ttu-id="fef9a-115">列</span><span class="sxs-lookup"><span data-stu-id="fef9a-115">Column</span></span> | <span data-ttu-id="fef9a-116">Adaptive.Column, Adaptive.Action.Tap</span><span class="sxs-lookup"><span data-stu-id="fef9a-116">Adaptive.Column, Adaptive.Action.Tap</span></span> |
| <span data-ttu-id="fef9a-117">ColumnSet</span><span class="sxs-lookup"><span data-stu-id="fef9a-117">ColumnSet</span></span> | <span data-ttu-id="fef9a-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span><span class="sxs-lookup"><span data-stu-id="fef9a-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span></span> |
| <span data-ttu-id="fef9a-119">容器</span><span class="sxs-lookup"><span data-stu-id="fef9a-119">Container</span></span> | <span data-ttu-id="fef9a-120">Adaptive.Container</span><span class="sxs-lookup"><span data-stu-id="fef9a-120">Adaptive.Container</span></span>|
| <span data-ttu-id="fef9a-121">Input.ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="fef9a-121">Input.ChoiceSet</span></span> | <span data-ttu-id="fef9a-122">Adaptive.Input.ChoiceSet,  Adaptive.Input.ChoiceSet.ComboBox, Adaptive.Input.ChoiceSet.CheckBox,  Adaptive.Input.ChoiceSet.Radio,  Adaptive.Input.ChoiceSet.ComboBoxItem</span><span class="sxs-lookup"><span data-stu-id="fef9a-122">Adaptive.Input.ChoiceSet,  Adaptive.Input.ChoiceSet.ComboBox, Adaptive.Input.ChoiceSet.CheckBox,  Adaptive.Input.ChoiceSet.Radio,  Adaptive.Input.ChoiceSet.ComboBoxItem</span></span> |
| <span data-ttu-id="fef9a-123">Input.Date</span><span class="sxs-lookup"><span data-stu-id="fef9a-123">Input.Date</span></span> | <span data-ttu-id="fef9a-124">Adaptive.Input.Text.Date</span><span class="sxs-lookup"><span data-stu-id="fef9a-124">Adaptive.Input.Text.Date</span></span>
| <span data-ttu-id="fef9a-125">Input.Number</span><span class="sxs-lookup"><span data-stu-id="fef9a-125">Input.Number</span></span> | <span data-ttu-id="fef9a-126">Adaptive.Input.Text.Number</span><span class="sxs-lookup"><span data-stu-id="fef9a-126">Adaptive.Input.Text.Number</span></span> |
| <span data-ttu-id="fef9a-127">Input.Text</span><span class="sxs-lookup"><span data-stu-id="fef9a-127">Input.Text</span></span> | <span data-ttu-id="fef9a-128">Adaptive.Input.Text</span><span class="sxs-lookup"><span data-stu-id="fef9a-128">Adaptive.Input.Text</span></span> |
| <span data-ttu-id="fef9a-129">Input.Time</span><span class="sxs-lookup"><span data-stu-id="fef9a-129">Input.Time</span></span> | <span data-ttu-id="fef9a-130">Adaptive.Input.Text.Time</span><span class="sxs-lookup"><span data-stu-id="fef9a-130">Adaptive.Input.Text.Time</span></span> |
| <span data-ttu-id="fef9a-131">Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="fef9a-131">Input.Toggle</span></span>| <span data-ttu-id="fef9a-132">Adaptive.Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="fef9a-132">Adaptive.Input.Toggle</span></span>|
| <span data-ttu-id="fef9a-133">图像</span><span class="sxs-lookup"><span data-stu-id="fef9a-133">Image</span></span>  | <span data-ttu-id="fef9a-134">Adaptive.Image</span><span class="sxs-lookup"><span data-stu-id="fef9a-134">Adaptive.Image</span></span> |
| <span data-ttu-id="fef9a-135">ImageSet</span><span class="sxs-lookup"><span data-stu-id="fef9a-135">ImageSet</span></span>  | <span data-ttu-id="fef9a-136">Adaptive.ImageSet</span><span class="sxs-lookup"><span data-stu-id="fef9a-136">Adaptive.ImageSet</span></span> |
| <span data-ttu-id="fef9a-137">FactSet</span><span class="sxs-lookup"><span data-stu-id="fef9a-137">FactSet</span></span> | <span data-ttu-id="fef9a-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span><span class="sxs-lookup"><span data-stu-id="fef9a-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span></span> |
| <span data-ttu-id="fef9a-139">TextBlock</span><span class="sxs-lookup"><span data-stu-id="fef9a-139">TextBlock</span></span>  | <span data-ttu-id="fef9a-140">Adaptive.TextBlock</span><span class="sxs-lookup"><span data-stu-id="fef9a-140">Adaptive.TextBlock</span></span> |

<span data-ttu-id="fef9a-141">此示例 XAML 资源字典，其中所有 Textblock 的背景设置为浅绿色。</span><span class="sxs-lookup"><span data-stu-id="fef9a-141">This sample XAML Resource dictionary that sets the background of all TextBlocks to Aqua.</span></span> <span data-ttu-id="fef9a-142">您可能希望某些比这更高级 😁</span><span class="sxs-lookup"><span data-stu-id="fef9a-142">You will probably want something more advanced than this 😁</span></span>

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
> <span data-ttu-id="fef9a-143">**有关服务器端映像生成的注意事项**WPF 呈现器提供`RenderCardToImageAsync`可用于服务器端映像生成的方法。</span><span class="sxs-lookup"><span data-stu-id="fef9a-143">**A note about server-side image generation** The WPF renderer provides a `RenderCardToImageAsync` method that can be used for server-side image generation.</span></span> <span data-ttu-id="fef9a-144">您必须只使用`ResourcesPath`属性如果在此环境中使用。</span><span class="sxs-lookup"><span data-stu-id="fef9a-144">You must only use the `ResourcesPath` property if used in this environment.</span></span> <span data-ttu-id="fef9a-145">请参阅[图像呈现](../net-image/getting-started.md)docs 的详细信息</span><span class="sxs-lookup"><span data-stu-id="fef9a-145">See the [Image Rendering](../net-image/getting-started.md) docs for more</span></span>