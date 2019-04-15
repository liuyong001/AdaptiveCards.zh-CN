---
title: 自适应卡工具
author: matthidinger
ms.author: mahiding
ms.date: 03/14/2019
ms.topic: article
ms.openlocfilehash: 35ce89653a6cf2a313518be0f221a166e1eb7711
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552499"
---
# <a name="card-designer"></a>卡设计器 

需要工具来设计您的卡？ 请关注处的基于浏览器的自适应卡设计器 [https://adaptivecards.io/designer](https://adaptivecards.io/designer)

[![设计器的屏幕截图](media/tools/designer.jpg)](https://adaptivecards.io/designer)

## <a name="embed-the-designer-into-your-app"></a>将在设计器嵌入到您的应用程序

但为什么时你可以那里发送你的用户**卡设计器将直接嵌入到你的 web**使用我们的 JavaScript 库应用程序。 

请查看[adaptivecards 设计器](https://npmjs.com/adaptivecards-designer)入门程序包。

# <a name="schema-validation"></a>架构验证

架构验证是更轻松地创作和启用工具的一种强大方法。

## <a name="json-schema"></a>JSON 架构
我们提供了一个完整[JSON 架构文件](http://adaptivecards.io/schemas/adaptive-card.json)用于编辑和验证 json 中的自适应卡。

在 Visual Studio 和 Visual Studio Code 中你可以通过获取自动 Intellisense`$schema`引用。

![错误](media/tools/invalidjson1.png)

![记忆式键入功能](media/tools/autocomplete.png)

### <a name="example"></a>示例

```json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "0.5",
    "body": []
}
```

# <a name="tools-and-samples"></a>工具和示例
有一些工具和源树中的示例，它们是有用的参考资料，以及有用的工具。

## <a name="visual-studio-code-extension"></a>Visual Studio Code 扩展
我们创建了 Visual Studio code 扩展可用于可视化编辑本身在编辑器内实时的卡。 

![扩展](media/tools/vscode-extension.png)

若要安装，打开扩展应用商店并搜索**自适应卡查看器**。

![Marketplace](media/tools/vscode-extension-marketplace.png)

### <a name="usage"></a>用法

当正在.json 文件编辑自适应卡`$schema`属性可以通过查看`Ctrl+Shift+V A`。
```json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": []
}
```

### <a name="options"></a>选项

以下 Visual Studio Code 设置是适用于 AdaptiveCards 查看器。 这可以在用户设置或工作区设置中设置。

```js
{
    // Open or not open the preview screen automatically
    "adaptivecardsviewer.enableautopreview": true,
}
```

## <a name="wpf-visualizer-sample"></a>WPF 可视化工具示例
[WPF 可视化工具示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer)允许您直观地显示在 Windows 计算机上使用 WPF/Xaml 的卡。  一个`hostconfig`编辑器生成用于编辑和查看主机的配置设置。 将这些设置保存为 JSON 中呈现应用程序中使用它们。

![wpf 可视化工具](media/tools/wpfvisualizer.png)

## <a name="wpf-imagerender-sample"></a>WPF ImageRender 示例
[ImageRender 示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/AdaptiveCards.Sample.ImageRender)将任何卡转变为从命令行使用 WPF PNG。 
