---
title: 在应用程序中呈现卡片
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: a562a05a91676dc5e6d8b51690acc4788802fb99
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454930"
---
# <a name="rendering-cards-inside-your-application"></a>在应用程序中呈现卡片

在应用程序中呈现自适应卡片很轻松。 我们提供适用于所有常用平台的 SDK，并提供[详细规范](implement-a-renderer.md)来指导你创建自己的自适应卡片呈现器。

1. **安装呈现器 SDK** - 适用于目标平台。
2. **创建呈现器实例** - 配置了应用的样式、规则和操作事件处理程序。
3. **根据本机 UI 呈现卡片** - 自动根据你的应用进行样式设置

## <a name="adaptive-cards-sdks"></a>自适应卡片 SDK

|平台|安装|生成|Docs|状态|
|---|---|---|---|---|
| JavaScript | [![npm install](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/nodejs)| [文档](../sdk/rendering-cards/javascript/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20564.svg) |
| .NET WPF | [![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet)| [文档](../sdk/rendering-cards/net-wpf/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20596.svg) |
| .NET HTML | [![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Html.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Html) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet) | [文档](../sdk/rendering-cards/net-html/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20596.svg) |
| Windows UWP | [![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Uwp.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Uwp) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/uwp) | [文档](../sdk/rendering-cards/uwp/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/56cf629e-8f3a-4412-acbc-bf69366c552c/20583.svg) |
| Android | [![Maven Central](https://img.shields.io/maven-central/v/io.adaptivecards/adaptivecards-android.svg)](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22adaptivecards-android%22) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/android) | [文档](../sdk/rendering-cards/android/getting-started.md) | ![生成状态](https://img.shields.io/vso/build/Microsoft/8d47e068-03c8-4cdc-aa9b-fc6929290322/17651.svg)
| iOS | [![CocoaPods](https://img.shields.io/cocoapods/v/AdaptiveCards.svg)](https://cocoapods.org/pods/AdaptiveCards) | [源](https://github.com/Microsoft/AdaptiveCards/tree/master/source/ios) | [文档](../sdk/rendering-cards/ios/getting-started.md) |  ![生成状态](https://img.shields.io/vso/build/Microsoft/8d47e068-03c8-4cdc-aa9b-fc6929290322/16990.svg) |

## <a name="create-an-instance-of-the-renderer"></a>创建呈现器的实例

下一步是创建 `AdaptiveCardRenderer` 的实例。 

### <a name="hook-up-action-events"></a>挂接操作事件

默认情况下，操作在卡上会呈现为按钮，但应用可以根据你的需要来定义操作的行为。 每个 SDK 都有 `OnAction` 事件的等效项，必须对其进行处理。

* **Action.OpenUrl** - 打开指定的 `url`。  
* **Action.Submit** - 获取提交的结果并将其发送到源。 如何将其发送到卡片的源完全取决于你自己。
* **Action.ShowCard** - 调用某个对话并将子卡呈现到该对话中。 请注意，只有在 `ShowCardActionMode` 设置为 `popup` 的情况下，才需要对此进行处理。

## <a name="render-a-card"></a>呈现卡片

获取卡片有效负载以后，请直接调用呈现器并传入卡片。 系统会返回一个由卡片内容组成的本机 UI 对象。 现在，只需将该 UI 置于应用中的某个位置即可。

## <a name="customization"></a>自定义

可以通过多种方式自定义呈现的内容。 

### <a name="hostconfig"></a>HostConfig

[HostConfig](host-config.md) 是一个共享的跨平台配置对象，用于控制应用中的卡片的基本样式设置和行为。 它定义的内容包括：字体大小、元素之间的间距、颜色、支持的操作的数目，等等。 

### <a name="native-platform-styling"></a>本机平台样式设置

大多数 UI 框架允许你根据本机 UI 框架样式设置来设置呈现的卡片的样式。 例如，在 HTML 中，可以指定 HTML 的 CSS 类；在 XAML 中，可以传入自定义 ResourceDictionary，以便对输出进行精细的控制。

### <a name="customize-per-element-rendering"></a>自定义按元素呈现功能

每个 SDK 都允许你重写任何元素的呈现，甚至允许你为自己定义的全新元素添加支持。  例如，可以更改 `Input.Date` 呈现器，以便在仍然保留呈现器的其余输出的情况下，发出你自己的自定义控制。 也可添加对你定义的自定义 `Rating` 元素的支持。



