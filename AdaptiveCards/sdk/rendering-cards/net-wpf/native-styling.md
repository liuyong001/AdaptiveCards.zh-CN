---
title: 本机样式 .NET WPF SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: ee5bec1a11f39ad69d40e57410c105b50ba45981
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552719"
---
# <a name="native-styling---net-wpf"></a>本机样式设置-.NET WPF

虽然主机配置在每个平台上都可获得大多数方法, 但你可能需要在每个平台上执行一些本机样式。 

WPF 通过允许您传递 ResourceDictionary 以实现精细的样式、行为、动画等, 从而使其变得简单。

| 元素 | 样式名称 |
|---|---|
| AdaptiveCard | Adaptive.Card| 
| Action.OpenUrl  | Adaptive.Action.OpenUrl  |
| Action.ShowCard | Adaptive.Action.ShowCard |
| Action.Submit  | Adaptive.Action.Submit  |
| 列 | 自适应. 列, 自适应。 |
| ColumnSet | Adaptive.ColumnSet, Adaptive.VerticalSeparator |
| 容器 | Adaptive.Container|
| Input.ChoiceSet | ChoiceSet、ChoiceSet、ChoiceSet、ChoiceSet、、ChoiceSet、ComboBoxItem、、、、、、。 |
| Input.Date | Adaptive.Input.Text.Date
| Input.Number | Adaptive.Input.Text.Number |
| Input.Text | Adaptive.Input.Text |
| Input.Time | Adaptive.Input.Text.Time |
| Input.Toggle| Adaptive.Input.Toggle|
| 图像  | Adaptive.Image |
| ImageSet  | Adaptive.ImageSet |
| FactSet | Adaptive.FactSet, Adaptive.Fact.Title, Adaptive.Fact.Value |
| TextBlock  | Adaptive.TextBlock |

此示例 XAML 资源字典, 它将所有 Textblock 的背景设置为浅绿色。 你可能希望比此更高级的东西😁

```xml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation" 
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
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
> **有关服务器端映像生成的说明**WPF 呈现器提供`RenderCardToImageAsync`可用于生成服务器端映像的方法。 仅在此环境中`ResourcesPath`使用属性时, 才能使用此属性。 有关详细信息, 请参阅[图像呈现](../net-image/getting-started.md)文档