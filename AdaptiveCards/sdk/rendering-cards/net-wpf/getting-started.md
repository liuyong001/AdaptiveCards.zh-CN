---
title: .NET WPF SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: a3f63fc812c97014af06dd1a197b24c5d07361c2
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553619"
---
# <a name="getting-started---net-wpf"></a><span data-ttu-id="8dadc-102">获取已开始-.NET WPF</span><span class="sxs-lookup"><span data-stu-id="8dadc-102">Getting started - .NET WPF</span></span>

<span data-ttu-id="8dadc-103">如我们所述[Getting Started](../../../authoring-cards/getting-started.md)页上，自适应卡是一个 JSON 序列化卡对象模型。</span><span class="sxs-lookup"><span data-stu-id="8dadc-103">As we described in [Getting Started](../../../authoring-cards/getting-started.md) page, an Adaptive Card is a JSON-serialized card object model.</span></span> <span data-ttu-id="8dadc-104">此库，可轻松地将该 JSON 呈现到 WPF UI，你可以使用您的应用程序中。</span><span class="sxs-lookup"><span data-stu-id="8dadc-104">This library makes it easy to render that JSON into WPF UI that you can use within your app.</span></span>

## <a name="nuget-install"></a><span data-ttu-id="8dadc-105">NuGet 安装</span><span class="sxs-lookup"><span data-stu-id="8dadc-105">NuGet install</span></span>

<span data-ttu-id="8dadc-106">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf)</span><span class="sxs-lookup"><span data-stu-id="8dadc-106">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf)</span></span>

```console
Install-Package AdaptiveCards.Rendering.Wpf
```

### <a name="xceed-enhanced-input-package"></a><span data-ttu-id="8dadc-107">Xceed 增强输入的包</span><span class="sxs-lookup"><span data-stu-id="8dadc-107">Xceed enhanced input package</span></span>

<span data-ttu-id="8dadc-108">此可选包增强了超出 WPF 提供了现成的自适应卡输入控件。</span><span class="sxs-lookup"><span data-stu-id="8dadc-108">This optional package enhances the Adaptive Card Input controls beyond what WPF provides out of the box.</span></span> <span data-ttu-id="8dadc-109">它具有的依赖关系 `Extended.Wpf.Toolkit`</span><span class="sxs-lookup"><span data-stu-id="8dadc-109">It has a dependency on `Extended.Wpf.Toolkit`</span></span>

<span data-ttu-id="8dadc-110">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.Xceed.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf.Xceed)</span><span class="sxs-lookup"><span data-stu-id="8dadc-110">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.Xceed.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf.Xceed)</span></span>

```console
Install-Package AdaptiveCards.Rendering.Wpf.Xceed
```

## <a name="wpf-visualizer-sample"></a><span data-ttu-id="8dadc-111">WPF 可视化工具示例</span><span class="sxs-lookup"><span data-stu-id="8dadc-111">WPF Visualizer Sample</span></span>

![可视化工具屏幕截图](../../../resources/media/tools/wpfvisualizer.png)

<span data-ttu-id="8dadc-113">[WPF 可视化工具示例](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer)用于可视化使用 WPF 的卡。</span><span class="sxs-lookup"><span data-stu-id="8dadc-113">The [WPF Visualizer sample](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer) lets you visualize cards using WPF.</span></span>  <span data-ttu-id="8dadc-114">一个`Host Config`编辑器生成用于编辑和查看主机的配置设置。</span><span class="sxs-lookup"><span data-stu-id="8dadc-114">A `Host Config` editor is built in for editing and viewing host config settings.</span></span> <span data-ttu-id="8dadc-115">将这些设置保存为 JSON 中呈现应用程序中使用它们。</span><span class="sxs-lookup"><span data-stu-id="8dadc-115">Save these settings as a JSON to use them in rendering in your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dadc-116">后续步骤</span><span class="sxs-lookup"><span data-stu-id="8dadc-116">Next steps</span></span>

<span data-ttu-id="8dadc-117">请参阅[呈现卡片](render-a-card.md)以了解后续步骤 ！</span><span class="sxs-lookup"><span data-stu-id="8dadc-117">See [Render a card](render-a-card.md) for the next steps!</span></span>
