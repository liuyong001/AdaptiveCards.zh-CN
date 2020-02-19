---
title: .NET WPF SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: 999f8ac3cd6a18fbbfc8b8bbdcf47465d8bb314f
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454280"
---
# <a name="getting-started---net-wpf"></a><span data-ttu-id="b93b5-102">入门-.NET WPF</span><span class="sxs-lookup"><span data-stu-id="b93b5-102">Getting started - .NET WPF</span></span>

<span data-ttu-id="b93b5-103">正如我们在[入门](../../../authoring-cards/getting-started.md)"页中所述，自适应卡是 JSON 序列化的卡对象模型。</span><span class="sxs-lookup"><span data-stu-id="b93b5-103">As we described in [Getting Started](../../../authoring-cards/getting-started.md) page, an Adaptive Card is a JSON-serialized card object model.</span></span> <span data-ttu-id="b93b5-104">利用此库，可以轻松地将 JSON 呈现到可在应用中使用的 WPF UI 中。</span><span class="sxs-lookup"><span data-stu-id="b93b5-104">This library makes it easy to render that JSON into WPF UI that you can use within your app.</span></span>

## <a name="nuget-install"></a><span data-ttu-id="b93b5-105">NuGet 安装</span><span class="sxs-lookup"><span data-stu-id="b93b5-105">NuGet install</span></span>

<span data-ttu-id="b93b5-106">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf)</span><span class="sxs-lookup"><span data-stu-id="b93b5-106">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf)</span></span>

```console
Install-Package AdaptiveCards.Rendering.Wpf
```

### <a name="xceed-enhanced-input-package"></a><span data-ttu-id="b93b5-107">Xceed 增强型输入包</span><span class="sxs-lookup"><span data-stu-id="b93b5-107">Xceed enhanced input package</span></span>

<span data-ttu-id="b93b5-108">此可选包可增强自适应卡输入控件，而 WPF 不提供该功能。</span><span class="sxs-lookup"><span data-stu-id="b93b5-108">This optional package enhances the Adaptive Card Input controls beyond what WPF provides out of the box.</span></span> <span data-ttu-id="b93b5-109">它依赖于 `Extended.Wpf.Toolkit`</span><span class="sxs-lookup"><span data-stu-id="b93b5-109">It has a dependency on `Extended.Wpf.Toolkit`</span></span>

<span data-ttu-id="b93b5-110">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.Xceed.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf.Xceed)</span><span class="sxs-lookup"><span data-stu-id="b93b5-110">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.Xceed.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf.Xceed)</span></span>

```console
Install-Package AdaptiveCards.Rendering.Wpf.Xceed
```

## <a name="wpf-visualizer-sample"></a><span data-ttu-id="b93b5-111">WPF 可视化工具示例</span><span class="sxs-lookup"><span data-stu-id="b93b5-111">WPF Visualizer Sample</span></span>

![可视化工具屏幕截图](../../../resources/media/tools/wpfvisualizer.png)

<span data-ttu-id="b93b5-113">[Wpf 可视化工具示例](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer)使你可以使用 wpf 可视化卡片。</span><span class="sxs-lookup"><span data-stu-id="b93b5-113">The [WPF Visualizer sample](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer) lets you visualize cards using WPF.</span></span>  <span data-ttu-id="b93b5-114">已经内置了 `Host Config` 编辑器，因此可以编辑和查看 host config 设置。</span><span class="sxs-lookup"><span data-stu-id="b93b5-114">A `Host Config` editor is built in for editing and viewing host config settings.</span></span> <span data-ttu-id="b93b5-115">将这些设置另存为 JSON，即可在应用程序中将它们用于呈现。</span><span class="sxs-lookup"><span data-stu-id="b93b5-115">Save these settings as a JSON to use them in rendering in your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b93b5-116">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b93b5-116">Next steps</span></span>

<span data-ttu-id="b93b5-117">请参阅[呈现卡片](render-a-card.md)，了解后续步骤！</span><span class="sxs-lookup"><span data-stu-id="b93b5-117">See [Render a card](render-a-card.md) for the next steps!</span></span>
