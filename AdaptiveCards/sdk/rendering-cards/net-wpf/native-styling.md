---
title: 本机样式 .NET WPF SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: f9243fc6880c926c04f80f74713e91d1e37cf3d5
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417597"
---
# <a name="native-styling---net-wpf"></a><span data-ttu-id="7aa28-102">本机样式设置-.NET WPF</span><span class="sxs-lookup"><span data-stu-id="7aa28-102">Native styling - .NET WPF</span></span>

<span data-ttu-id="7aa28-103">虽然主机配置在每个平台上都可获得大多数方法，但你可能需要在每个平台上执行一些本机样式。</span><span class="sxs-lookup"><span data-stu-id="7aa28-103">While Host Config will get you most of the way there on each platform, it's likely that you will have to do some native styling on each platform.</span></span> 

<span data-ttu-id="7aa28-104">WPF 通过允许您传递 ResourceDictionary 以实现精细的样式、行为、动画等，从而使其变得简单。</span><span class="sxs-lookup"><span data-stu-id="7aa28-104">WPF makes this easy by allowing you to pass a ResourceDictionary for fine-grained styling, behavior, animations, etc.</span></span>

| <span data-ttu-id="7aa28-105">元素</span><span class="sxs-lookup"><span data-stu-id="7aa28-105">Element</span></span> | <span data-ttu-id="7aa28-106">样式名称</span><span class="sxs-lookup"><span data-stu-id="7aa28-106">Style names</span></span> |
|---|---|
| <span data-ttu-id="7aa28-107">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="7aa28-107">AdaptiveCard</span></span> | <span data-ttu-id="7aa28-108">自适应卡</span><span class="sxs-lookup"><span data-stu-id="7aa28-108">Adaptive.Card</span></span>| 
| <span data-ttu-id="7aa28-109">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="7aa28-109">Action.OpenUrl</span></span>  | <span data-ttu-id="7aa28-110">OpenUrl</span><span class="sxs-lookup"><span data-stu-id="7aa28-110">Adaptive.Action.OpenUrl</span></span>  |
| <span data-ttu-id="7aa28-111">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="7aa28-111">Action.ShowCard</span></span> | <span data-ttu-id="7aa28-112">ShowCard</span><span class="sxs-lookup"><span data-stu-id="7aa28-112">Adaptive.Action.ShowCard</span></span> |
| <span data-ttu-id="7aa28-113">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="7aa28-113">Action.Submit</span></span>  | <span data-ttu-id="7aa28-114">自适应. 提交</span><span class="sxs-lookup"><span data-stu-id="7aa28-114">Adaptive.Action.Submit</span></span>  |
| <span data-ttu-id="7aa28-115">列</span><span class="sxs-lookup"><span data-stu-id="7aa28-115">Column</span></span> | <span data-ttu-id="7aa28-116">自适应. 列，自适应。</span><span class="sxs-lookup"><span data-stu-id="7aa28-116">Adaptive.Column, Adaptive.Action.Tap</span></span> |
| <span data-ttu-id="7aa28-117">ColumnSet</span><span class="sxs-lookup"><span data-stu-id="7aa28-117">ColumnSet</span></span> | <span data-ttu-id="7aa28-118">列集，自适应. VerticalSeparator</span><span class="sxs-lookup"><span data-stu-id="7aa28-118">Adaptive.ColumnSet, Adaptive.VerticalSeparator</span></span> |
| <span data-ttu-id="7aa28-119">容器</span><span class="sxs-lookup"><span data-stu-id="7aa28-119">Container</span></span> | <span data-ttu-id="7aa28-120">自适应</span><span class="sxs-lookup"><span data-stu-id="7aa28-120">Adaptive.Container</span></span>|
| <span data-ttu-id="7aa28-121">输入. ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="7aa28-121">Input.ChoiceSet</span></span> | <span data-ttu-id="7aa28-122">ChoiceSet、ChoiceSet、ChoiceSet、ChoiceSet、、ChoiceSet、ComboBoxItem、、、、、、。</span><span class="sxs-lookup"><span data-stu-id="7aa28-122">Adaptive.Input.ChoiceSet,  Adaptive.Input.ChoiceSet.ComboBox, Adaptive.Input.ChoiceSet.CheckBox,  Adaptive.Input.ChoiceSet.Radio,  Adaptive.Input.ChoiceSet.ComboBoxItem</span></span> |
| <span data-ttu-id="7aa28-123">输入。日期</span><span class="sxs-lookup"><span data-stu-id="7aa28-123">Input.Date</span></span> | <span data-ttu-id="7aa28-124">自适应. 文本。</span><span class="sxs-lookup"><span data-stu-id="7aa28-124">Adaptive.Input.Text.Date</span></span>
| <span data-ttu-id="7aa28-125">输入。数字</span><span class="sxs-lookup"><span data-stu-id="7aa28-125">Input.Number</span></span> | <span data-ttu-id="7aa28-126">自适应. 数字</span><span class="sxs-lookup"><span data-stu-id="7aa28-126">Adaptive.Input.Text.Number</span></span> |
| <span data-ttu-id="7aa28-127">输入。文本</span><span class="sxs-lookup"><span data-stu-id="7aa28-127">Input.Text</span></span> | <span data-ttu-id="7aa28-128">自适应. 输入文本</span><span class="sxs-lookup"><span data-stu-id="7aa28-128">Adaptive.Input.Text</span></span> |
| <span data-ttu-id="7aa28-129">输入。时间</span><span class="sxs-lookup"><span data-stu-id="7aa28-129">Input.Time</span></span> | <span data-ttu-id="7aa28-130">自适应. 文本。时间</span><span class="sxs-lookup"><span data-stu-id="7aa28-130">Adaptive.Input.Text.Time</span></span> |
| <span data-ttu-id="7aa28-131">输入。切换</span><span class="sxs-lookup"><span data-stu-id="7aa28-131">Input.Toggle</span></span>| <span data-ttu-id="7aa28-132">自适应. 输入开关</span><span class="sxs-lookup"><span data-stu-id="7aa28-132">Adaptive.Input.Toggle</span></span>|
| <span data-ttu-id="7aa28-133">映像</span><span class="sxs-lookup"><span data-stu-id="7aa28-133">Image</span></span>  | <span data-ttu-id="7aa28-134">自适应图像</span><span class="sxs-lookup"><span data-stu-id="7aa28-134">Adaptive.Image</span></span> |
| <span data-ttu-id="7aa28-135">ImageSet</span><span class="sxs-lookup"><span data-stu-id="7aa28-135">ImageSet</span></span>  | <span data-ttu-id="7aa28-136">自适应. ImageSet</span><span class="sxs-lookup"><span data-stu-id="7aa28-136">Adaptive.ImageSet</span></span> |
| <span data-ttu-id="7aa28-137">FactSet</span><span class="sxs-lookup"><span data-stu-id="7aa28-137">FactSet</span></span> | <span data-ttu-id="7aa28-138">FactSet、自适应. Title、自适应事实. 值</span><span class="sxs-lookup"><span data-stu-id="7aa28-138">Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value</span></span> |
| <span data-ttu-id="7aa28-139">TextBlock</span><span class="sxs-lookup"><span data-stu-id="7aa28-139">TextBlock</span></span>  | <span data-ttu-id="7aa28-140">自适应. TextBlock</span><span class="sxs-lookup"><span data-stu-id="7aa28-140">Adaptive.TextBlock</span></span> |

<span data-ttu-id="7aa28-141">此示例 XAML 资源字典，它将所有 Textblock 的背景设置为浅绿色。</span><span class="sxs-lookup"><span data-stu-id="7aa28-141">This sample XAML Resource dictionary that sets the background of all TextBlocks to Aqua.</span></span> <span data-ttu-id="7aa28-142">你可能希望比此更高级的东西😁</span><span class="sxs-lookup"><span data-stu-id="7aa28-142">You will probably want something more advanced than this 😁</span></span>

```xml
<ResourceDictionary
    xmlns="https://schemas.microsoft.com/winfx/2006/xaml/presentation" 
    xmlns:x="https://schemas.microsoft.com/winfx/2006/xaml">
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
> <span data-ttu-id="7aa28-143">**有关服务器端映像生成的说明**WPF 呈现器提供 `RenderCardToImageAsync` 可用于生成服务器端映像的方法。</span><span class="sxs-lookup"><span data-stu-id="7aa28-143">**A note about server-side image generation** The WPF renderer provides a `RenderCardToImageAsync` method that can be used for server-side image generation.</span></span> <span data-ttu-id="7aa28-144">仅 `ResourcesPath` 在此环境中使用属性时，才能使用此属性。</span><span class="sxs-lookup"><span data-stu-id="7aa28-144">You must only use the `ResourcesPath` property if used in this environment.</span></span> <span data-ttu-id="7aa28-145">有关详细信息，请参阅[图像呈现](../net-image/getting-started.md)文档</span><span class="sxs-lookup"><span data-stu-id="7aa28-145">See the [Image Rendering](../net-image/getting-started.md) docs for more</span></span>