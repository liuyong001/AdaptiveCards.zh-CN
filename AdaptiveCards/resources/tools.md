---
title: 自适应卡工具
author: matthidinger
ms.author: mahiding
ms.date: 03/14/2019
ms.topic: article
ms.openlocfilehash: f26550a73610073000166357df5b70c1bd8ccdc8
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417588"
---
# <a name="tools-and-samples"></a>工具和示例

## <a name="card-designer"></a>卡设计器 

需要工具来设计卡片？ 不妨看看这个基于浏览器的自适应卡片设计器：[https://adaptivecards.io/designer](https://adaptivecards.io/designer)

[![设计器屏幕截图](media/tools/designer.jpg)](https://adaptivecards.io/designer)

### <a name="embed-the-designer-into-your-app"></a>将设计器嵌入应用

但是，如果你可以使用我们的 JavaScript 库**将卡片设计器直接嵌入 Web 应用**中，为何还要让用户大费周折呢？ 

若要开始，请查看 [adaptivecards-designer](https://npmjs.com/adaptivecards-designer) 包。

## <a name="schema-validation"></a>架构验证

可以通过架构验证轻松地进行创作并启用工具功能。

我们提供了完整的 [JSON 架构文件](https://adaptivecards.io/schemas/1.2.0/adaptive-card.json)，用于编辑和验证 json 格式的自适应卡片。 请注意，架构 URL 进行了版本控制，较新版的自适应卡片会有相应的 URL。

在 Visual Studio 和 Visual Studio Code 中，添加一个 `$schema` 引用即可获取自动 Intellisense。

![无效](media/tools/invalidjson1.png)

![自动完成](media/tools/autocomplete.png)

## <a name="example"></a>示例

```json
{
    "$schema": "http://adaptivecards.io/schemas/1.2.0/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": []
}
```

## <a name="visual-studio-code-extension"></a>Visual Studio Code 扩展

我们创建了一个 Visual Studio Code 扩展，让你可以在编辑器中实时查看正在编辑的卡片。 

![扩展](media/tools/vscode-extension.png)

若要进行安装，请打开“扩展市场”，然后搜索“自适应卡片查看器”。

![市场](media/tools/vscode-extension-marketplace.png)

### <a name="usage"></a>用法

编辑包含自适应卡片 `$schema` 属性的 .json 文件时，可以使用 `Ctrl+Shift+V A` 来查看。
```json
{
    "$schema": "http://adaptivecards.io/schemas/1.2.0/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": []
}
```

### <a name="options"></a>选项

以下 Visual Studio Code 设置适用于自适应卡片查看器。 可以在“用户设置”或“工作区设置”中进行设置。

```js
{
    // Open or not open the preview screen automatically
    "adaptivecardsviewer.enableautopreview": true,
}
```

## <a name="wpf-visualizer-sample"></a>WPF 可视化工具示例

可以通过 [WPF 可视化工具示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer)在 Windows 计算机上使用 WPF/Xaml 实现卡片的可视化。  已经内置了 `hostconfig` 编辑器，因此可以编辑和查看 host config 设置。 将这些设置另存为 JSON，即可在应用程序中将它们用于呈现。

![wpf 可视化工具](media/tools/wpfvisualizer.png)

## <a name="wpf-imagerender-sample"></a>WPF ImageRender 示例

使用 [ImageRender 示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/AdaptiveCards.Sample.ImageRender)，可以通过 WPF 在命令行中将任何卡片转换成 PNG。 
