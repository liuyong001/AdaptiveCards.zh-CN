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
# <a name="getting-started---net-wpf"></a>获取已开始-.NET WPF

如我们所述[Getting Started](../../../authoring-cards/getting-started.md)页上，自适应卡是一个 JSON 序列化卡对象模型。 此库，可轻松地将该 JSON 呈现到 WPF UI，你可以使用您的应用程序中。

## <a name="nuget-install"></a>NuGet 安装

[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf)

```console
Install-Package AdaptiveCards.Rendering.Wpf
```

### <a name="xceed-enhanced-input-package"></a>Xceed 增强输入的包

此可选包增强了超出 WPF 提供了现成的自适应卡输入控件。 它具有的依赖关系 `Extended.Wpf.Toolkit`

[![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Rendering.Wpf.Xceed.svg)](https://www.nuget.org/packages/AdaptiveCards.Rendering.Wpf.Xceed)

```console
Install-Package AdaptiveCards.Rendering.Wpf.Xceed
```

## <a name="wpf-visualizer-sample"></a>WPF 可视化工具示例

![可视化工具屏幕截图](../../../resources/media/tools/wpfvisualizer.png)

[WPF 可视化工具示例](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer)用于可视化使用 WPF 的卡。  一个`Host Config`编辑器生成用于编辑和查看主机的配置设置。 将这些设置保存为 JSON 中呈现应用程序中使用它们。

## <a name="next-steps"></a>后续步骤

请参阅[呈现卡片](render-a-card.md)以了解后续步骤 ！
