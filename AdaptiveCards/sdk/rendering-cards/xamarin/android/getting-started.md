---
title: Xamarin.Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: a7fd40ac7f026e2a325e7dc52e10defe550fd43a
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76146001"
---
# <a name="getting-started---xamarinandroid"></a><span data-ttu-id="0c46c-102">入门-Xamarin Android</span><span class="sxs-lookup"><span data-stu-id="0c46c-102">Getting started - Xamarin.Android</span></span>

<span data-ttu-id="0c46c-103">这是一个面向本机 xamarin android 应用程序的呈现器库，并且基于你可在[此处](../../android/getting-started.md)找到的 android 呈现器。</span><span class="sxs-lookup"><span data-stu-id="0c46c-103">This is a renderer library which targets native xamarin android applications and is based on the Android renderer that you can find [here](../../android/getting-started.md).</span></span> 

## <a name="nuget-install"></a><span data-ttu-id="0c46c-104">NuGet 安装</span><span class="sxs-lookup"><span data-stu-id="0c46c-104">NuGet install</span></span>

<span data-ttu-id="0c46c-105">[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Xamarin.Android.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Xamarin.Android)</span><span class="sxs-lookup"><span data-stu-id="0c46c-105">[![Nuget install](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Xamarin.Android.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Xamarin.Android)</span></span>

<span data-ttu-id="0c46c-106">可在[此处](http://nuget.org)找到已发布的包</span><span class="sxs-lookup"><span data-stu-id="0c46c-106">You can find the published packages [here](http://nuget.org)</span></span>

```console
Install-Package AdaptiveCards.Rendering.Xamarin.Android -Version 0.1.0-alpha
```

## <a name="namespace"></a><span data-ttu-id="0c46c-107">命名空间</span><span class="sxs-lookup"><span data-stu-id="0c46c-107">Namespace</span></span>

<span data-ttu-id="0c46c-108">使用此库的必要命名空间为</span><span class="sxs-lookup"><span data-stu-id="0c46c-108">The necessary namespaces for using this library are</span></span>
```csharp
// To import the base object model classes as AdaptiveCard, TextBlock, Column, ShowCardAction, ...
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;

// To import the AdaptiveCardRenderer class
using AdaptiveCards.Rendering.Xamarin.Android.Renderer;

// To import the ICardActionHandler interface
using AdaptiveCards.Rendering.Xamarin.Android.Renderer.ActionHandler;

// To use feature registration and register custom behaviour 
using AdaptiveCards.Rendering.Xamarin.Android.Renderer.Registration;
```

## <a name="xamarinandroid-visualizer-sample"></a><span data-ttu-id="0c46c-109">Xamarin Android 可视化工具示例</span><span class="sxs-lookup"><span data-stu-id="0c46c-109">Xamarin.Android Visualizer Sample</span></span>

<span data-ttu-id="0c46c-110">[Xamarin Android 可视化工具示例](https://github.com/Microsoft/AdaptiveCards/tree/master/source/xamarin/Xamarin.Droid.Sample)允许使用 xamarin 直观显示卡。</span><span class="sxs-lookup"><span data-stu-id="0c46c-110">The [Xamarin.Android Visualizer sample](https://github.com/Microsoft/AdaptiveCards/tree/master/source/xamarin/Xamarin.Droid.Sample) lets you visualize cards using Xamarin.Android.</span></span> <span data-ttu-id="0c46c-111">如果曾经使用过 Android 示例应用程序，就会发现体验非常相似。</span><span class="sxs-lookup"><span data-stu-id="0c46c-111">If you have ever used the Android sample application you'll find the experience to be really similar.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c46c-112">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0c46c-112">Next steps</span></span>

<span data-ttu-id="0c46c-113">对于后续步骤，快速入门检查将[呈现一个卡](render-a-card.md)！</span><span class="sxs-lookup"><span data-stu-id="0c46c-113">For a quick start check [Render a card](render-a-card.md) for the next steps!</span></span>

<span data-ttu-id="0c46c-114">若要深入了解已为 Xamarin 绑定呈现器库的类，可以通过单击下面的方法来检查某些绑定类：</span><span class="sxs-lookup"><span data-stu-id="0c46c-114">For a more in depth view of the classes that have been binded for the Xamarin.Android renderer library, you can check some of the binded classes by clicking on them below:</span></span>
* [```AdaptiveCard```](adaptivecards-rendering-xamarin-android-objectmodel-adaptivecard.md)
* [```AdaptiveCardRenderer```](adaptivecards-rendering-xamarin-android-renderer-adaptivecardrenderer.md)
* [```CardRendererRegistration```](adaptivecards-rendering-xamarin-android-renderer-cardrendererregistration.md)
* [```FeatureRegistration```](adaptivecards-rendering-xamarin-android-objectmodel-featureregistration.md)
* [```ICardActionHandler```](adaptivecards-renderin-xamarin-android-renderer-actionhandler-icardactionhandler.md)
* [```RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md)