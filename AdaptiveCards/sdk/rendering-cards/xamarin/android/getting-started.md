---
title: Xamarin.Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: cd8dccd2aece23dd67ee8d601e8efaa2a1bcd4f2
ms.sourcegitcommit: 588f3e97ed3de96dfff54906ac666ce42ef1e7f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91928827"
---
# <a name="getting-started---xamarinandroid"></a>入门-Xamarin Android

这是一个面向本机 xamarin android 应用程序的呈现器库，并且基于你可在 [此处](../../android/getting-started.md)找到的 android 呈现器。 

## <a name="nuget-install"></a>NuGet 安装

[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Xamarin.Android.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Xamarin.Android)

可在[此处](http://nuget.org)找到已发布的包

```console
Install-Package AdaptiveCards.Rendering.Xamarin.Android -Version 0.1.0-alpha
```

## <a name="namespace"></a>命名空间

使用此库的必要命名空间为
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

## <a name="xamarinandroid-visualizer-sample"></a>Xamarin Android 可视化工具示例

[Xamarin Android 可视化工具示例](https://github.com/Microsoft/AdaptiveCards/tree/main/source/xamarin/Xamarin.Droid.Sample)允许使用 xamarin 直观显示卡。 如果曾经使用过 Android 示例应用程序，就会发现体验非常相似。

## <a name="next-steps"></a>后续步骤

对于后续步骤，快速入门检查将 [呈现一个卡](render-a-card.md) ！

若要深入了解已为 Xamarin 绑定呈现器库的类，可以通过单击下面的方法来检查某些绑定类：
* [```AdaptiveCard```](adaptivecards-rendering-xamarin-android-objectmodel-adaptivecard.md)
* [```AdaptiveCardRenderer```](adaptivecards-rendering-xamarin-android-renderer-adaptivecardrenderer.md)
* [```CardRendererRegistration```](adaptivecards-rendering-xamarin-android-renderer-cardrendererregistration.md)
* [```FeatureRegistration```](adaptivecards-rendering-xamarin-android-objectmodel-featureregistration.md)
* [```ICardActionHandler```](adaptivecards-renderin-xamarin-android-renderer-actionhandler-icardactionhandler.md)
* [```RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md)
