---
title: 应用程序中呈现卡片
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 0a5f99268ce483fddd99f4493b386db796c3e9d2
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67138090"
---
# <a name="rendering-cards-inside-your-application"></a>应用程序中呈现卡片

很容易地在应用程序内呈现自适应卡。 我们为所有常见平台，提供 Sdk，以及提供[的详细规范](implement-a-renderer.md)用于创建你自己的自适应卡呈现器。

1. **安装 SDK 的呈现器**-为目标平台。
2. **创建呈现器实例**-配置与你的应用的样式、 规则和操作事件处理程序。
3. **呈现为本机 UI 的卡**-自动应用到你的应用了样式。

## <a name="adaptive-cards-sdks"></a>自适应卡 Sdk

|平台|安装|Build|文档|状态|
|---|---|---|---|---|
| JavaScript | [![npm 安装](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/nodejs)| [Docs](../sdk/rendering-cards/javascript/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20564.svg) |
| .NET WPF | [![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet)| [Docs](../sdk/rendering-cards/net-wpf/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20596.svg) |
| .NET HTML | [![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Html.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Html) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet) | [Docs](../sdk/rendering-cards/net-html/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20596.svg) |
| Windows UWP | [![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Uwp.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Uwp) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/uwp) | [Docs](../sdk/rendering-cards/uwp/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20583.svg) |
| Android | [![Maven 中心](https://img.shields.io/maven-central/v/io.adaptivecards/adaptivecards-android.svg)](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22adaptivecards-android%22) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/android) | [Docs](../sdk/rendering-cards/android/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/8d47e068-03c8-4cdc-aa9b-fc6929290322/17651.svg)
| iOS | [![CocoaPods](https://img.shields.io/cocoapods/v/AdaptiveCards.svg)](https://cocoapods.org/pods/AdaptiveCards) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/ios) | [Docs](../sdk/rendering-cards/ios/getting-started.md) |  ![生成状态](https://img.shields.io/vso/build/Microsoft/8d47e068-03c8-4cdc-aa9b-fc6929290322/16990.svg) |

## <a name="create-an-instance-of-the-renderer"></a>创建呈现器的实例

下一步是创建的实例`AdaptiveCardRenderer`。 

### <a name="hook-up-action-events"></a>关联操作事件

默认情况下，操作将呈现为在卡上的按钮，但这取决于您的应用程序以使其按预期工作。 每个 SDK 有相当于`OnAction`必须处理的事件。

* **Action.OpenUrl** -打开指定`url`。  
* **Action.Submit** -提取的提交结果，并将其发送到源。 如何向的源发送它是卡片的完全取决于您。
* **Action.ShowCard** -调用一个对话框，并将子卡呈现到该对话框。 请注意，只需处理此 if`ShowCardActionMode`设置为`popup`。

## <a name="render-a-card"></a>呈现数据卡

获取卡有效负载后，只需调用呈现器，并在卡片中传递。 您将得到的卡内容组成的本机用户界面对象。 现在只需将此 UI 某处应用程序中。

## <a name="customization"></a>自定义

有几种方法可以自定义要呈现的内容。 

### <a name="hostconfig"></a>HostConfig

一个[HostConfig](host-config.md)是共享的跨平台的配置对象，用于控制的基本样式和行为的卡到你的应用。 它定义字体大小，元素、 颜色、 支持的操作等号之间的间距等内容。 

### <a name="native-platform-styling"></a>本机平台样式设置

大多数 UI 框架，可使用本机 UI 框架样式设置样式呈现的卡。 例如，在 HTML 中可以指定适用于 HTML、 CSS 类，或在 XAML 中可传递自定义的 ResourceDictionary 中的输出的细粒度控制。

### <a name="customize-per-element-rendering"></a>自定义每个元素呈现

每个 SDK，可重写的呈现任何元素，或者甚至添加对您定义的整个新元素的支持。  例如，可以更改`Input.Date`呈现器仍保留的呈现器输出的其余部分的同时发出自定义控件。 也可以添加对自定义支持`Rating`你定义的元素。



