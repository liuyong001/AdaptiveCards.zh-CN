---
title: 本机样式 .NET WPF SDK
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
# <a name="native-styling---net-wpf"></a><span data-ttu-id="bf505-102">本机样式设置-.NET WPF</span><span class="sxs-lookup"><span data-stu-id="bf505-102">Native styling - .NET WPF</span></span>

<span data-ttu-id="bf505-103">虽然主机配置在每个平台上都可获得大多数方法, 但你可能需要在每个平台上执行一些本机样式。</span><span class="sxs-lookup"><span data-stu-id="bf505-103">While Host Config will get you most of the way there on each platform, it's likely that you will have to do some native styling on each platform.</span></span> 

<span data-ttu-id="bf505-104">WPF 通过允许您传递 ResourceDictionary 以实现精细的样式、行为、动画等, 从而使其变得简单。</span><span class="sxs-lookup"><span data-stu-id="bf505-104">WPF makes this easy by allowing you to pass a ResourceDictionary for fine-grained styling, behavior, animations, etc.</span></span>

| <span data-ttu-id="bf505-105">元素</span><span class="sxs-lookup"><span data-stu-id="bf505-105">Element</span></span> | <span data-ttu-id="bf505-106">样式名称</span><span class="sxs-lookup"><span data-stu-id="bf505-106">Style names</span></span> |
|---|---|
| <span data-ttu-id="bf505-107">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="bf505-107">AdaptiveCard</span></span> | <span data-ttu-id="bf505-108">Adaptive.Card</span><span class="sxs-lookup"><span data-stu-id="bf505-108">Adaptive.Card</span></span>| 
| <span data-ttu-id="bf505-109">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="bf505-109">Action.OpenUrl</span></span>  | <span data-ttu-id="bf505-110">Adaptive.Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="bf505-110">Adaptive.Action.OpenUrl</span></span>  |
| <span data-ttu-id="bf505-111">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="bf505-111">Action.ShowCard</span></span> | <span data-ttu-id="bf505-112">Adaptive.Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="bf505-112">Adaptive.Action.ShowCard</span></span> |
| <span data-ttu-id="bf505-113">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="bf505-113">Action.Submit</span></span>  | <span data-ttu-id="bf505-114">Adaptive.Action.Submit</span><span class="sxs-lookup"><span data-stu-id="bf505-114">Adaptive.Action.Submit</span></span>  |
| <span data-ttu-id="bf505-115">列</span><span class="sxs-lookup"><span data-stu-id="bf505-115">Column</span></span> | <span data-ttu-id="bf505-116">自适应. 列, 自适应。</span><span class="sxs-lookup"><span data-stu-id="bf505-116">Adaptive.Column, Adaptive.Action.Tap</span></span> |
| <span data-ttu-id="bf505-117">ColumnSet</span><span class="sxs-lookup"><span data-stu-id="bf505-117">ColumnSet</span></span> | <span data-ttu-id="bf505-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span><span class="sxs-lookup"><span data-stu-id="bf505-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span></span> |
| <span data-ttu-id="bf505-119">容器</span><span class="sxs-lookup"><span data-stu-id="bf505-119">Container</span></span> | <span data-ttu-id="bf505-120">Adaptive.Container</span><span class="sxs-lookup"><span data-stu-id="bf505-120">Adaptive.Container</span></span>|
| <span data-ttu-id="bf505-121">Input.ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="bf505-121">Input.ChoiceSet</span></span> | <span data-ttu-id="bf505-122">ChoiceSet、ChoiceSet、ChoiceSet、ChoiceSet、、ChoiceSet、ComboBoxItem、、、、、、。</span><span class="sxs-lookup"><span data-stu-id="bf505-122">Adaptive.Input.ChoiceSet,  Adaptive.Input.ChoiceSet.ComboBox, Adaptive.Input.ChoiceSet.CheckBox,  Adaptive.Input.ChoiceSet.Radio,  Adaptive.Input.ChoiceSet.ComboBoxItem</span></span> |
| <span data-ttu-id="bf505-123">Input.Date</span><span class="sxs-lookup"><span data-stu-id="bf505-123">Input.Date</span></span> | <span data-ttu-id="bf505-124">Adaptive.Input.Text.Date</span><span class="sxs-lookup"><span data-stu-id="bf505-124">Adaptive.Input.Text.Date</span></span>
| <span data-ttu-id="bf505-125">Input.Number</span><span class="sxs-lookup"><span data-stu-id="bf505-125">Input.Number</span></span> | <span data-ttu-id="bf505-126">Adaptive.Input.Text.Number</span><span class="sxs-lookup"><span data-stu-id="bf505-126">Adaptive.Input.Text.Number</span></span> |
| <span data-ttu-id="bf505-127">Input.Text</span><span class="sxs-lookup"><span data-stu-id="bf505-127">Input.Text</span></span> | <span data-ttu-id="bf505-128">Adaptive.Input.Text</span><span class="sxs-lookup"><span data-stu-id="bf505-128">Adaptive.Input.Text</span></span> |
| <span data-ttu-id="bf505-129">Input.Time</span><span class="sxs-lookup"><span data-stu-id="bf505-129">Input.Time</span></span> | <span data-ttu-id="bf505-130">Adaptive.Input.Text.Time</span><span class="sxs-lookup"><span data-stu-id="bf505-130">Adaptive.Input.Text.Time</span></span> |
| <span data-ttu-id="bf505-131">Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="bf505-131">Input.Toggle</span></span>| <span data-ttu-id="bf505-132">Adaptive.Input.Toggle</span><span class="sxs-lookup"><span data-stu-id="bf505-132">Adaptive.Input.Toggle</span></span>|
| <span data-ttu-id="bf505-133">图像</span><span class="sxs-lookup"><span data-stu-id="bf505-133">Image</span></span>  | <span data-ttu-id="bf505-134">Adaptive.Image</span><span class="sxs-lookup"><span data-stu-id="bf505-134">Adaptive.Image</span></span> |
| <span data-ttu-id="bf505-135">ImageSet</span><span class="sxs-lookup"><span data-stu-id="bf505-135">ImageSet</span></span>  | <span data-ttu-id="bf505-136">Adaptive.ImageSet</span><span class="sxs-lookup"><span data-stu-id="bf505-136">Adaptive.ImageSet</span></span> |
| <span data-ttu-id="bf505-137">FactSet</span><span class="sxs-lookup"><span data-stu-id="bf505-137">FactSet</span></span> | <span data-ttu-id="bf505-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span><span class="sxs-lookup"><span data-stu-id="bf505-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span></span> |
| <span data-ttu-id="bf505-139">TextBlock</span><span class="sxs-lookup"><span data-stu-id="bf505-139">TextBlock</span></span>  | <span data-ttu-id="bf505-140">Adaptive.TextBlock</span><span class="sxs-lookup"><span data-stu-id="bf505-140">Adaptive.TextBlock</span></span> |

<span data-ttu-id="bf505-141">此示例 XAML 资源字典, 它将所有 Textblock 的背景设置为浅绿色。</span><span class="sxs-lookup"><span data-stu-id="bf505-141">This sample XAML Resource dictionary that sets the background of all TextBlocks to Aqua.</span></span> <span data-ttu-id="bf505-142">你可能希望比此更高级的东西😁</span><span class="sxs-lookup"><span data-stu-id="bf505-142">You will probably want something more advanced than this 😁</span></span>

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
> <span data-ttu-id="bf505-143">**有关服务器端映像生成的说明**WPF 呈现器提供`RenderCardToImageAsync`可用于生成服务器端映像的方法。</span><span class="sxs-lookup"><span data-stu-id="bf505-143">**A note about server-side image generation** The WPF renderer provides a `RenderCardToImageAsync` method that can be used for server-side image generation.</span></span> <span data-ttu-id="bf505-144">仅在此环境中`ResourcesPath`使用属性时, 才能使用此属性。</span><span class="sxs-lookup"><span data-stu-id="bf505-144">You must only use the `ResourcesPath` property if used in this environment.</span></span> <span data-ttu-id="bf505-145">有关详细信息, 请参阅[图像呈现](../net-image/getting-started.md)文档</span><span class="sxs-lookup"><span data-stu-id="bf505-145">See the [Image Rendering](../net-image/getting-started.md) docs for more</span></span>