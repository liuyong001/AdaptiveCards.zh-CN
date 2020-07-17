---
title: 本机样式 .NET WPF SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: f9243fc6880c926c04f80f74713e91d1e37cf3d5
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417597"
---
# <a name="native-styling---net-wpf"></a>本机样式设置-.NET WPF

虽然主机配置在每个平台上都可获得大多数方法，但你可能需要在每个平台上执行一些本机样式。 

WPF 通过允许您传递 ResourceDictionary 以实现精细的样式、行为、动画等，从而使其变得简单。

| 元素 | 样式名称 |
|---|---|
| AdaptiveCard | 自适应卡| 
| Action.OpenUrl  | OpenUrl  |
| Action.ShowCard | ShowCard |
| Action.Submit  | 自适应. 提交  |
| 列 | 自适应. 列，自适应。 |
| ColumnSet | 列集，自适应. VerticalSeparator |
| 容器 | 自适应|
| 输入. ChoiceSet | ChoiceSet、ChoiceSet、ChoiceSet、ChoiceSet、、ChoiceSet、ComboBoxItem、、、、、、。 |
| 输入。日期 | 自适应. 文本。
| 输入。数字 | 自适应. 数字 |
| 输入。文本 | 自适应. 输入文本 |
| 输入。时间 | 自适应. 文本。时间 |
| 输入。切换| 自适应. 输入开关|
| 映像  | 自适应图像 |
| ImageSet  | 自适应. ImageSet |
| FactSet | FactSet、自适应. Title、自适应事实. 值 |
| TextBlock  | 自适应. TextBlock |

此示例 XAML 资源字典，它将所有 Textblock 的背景设置为浅绿色。 你可能希望比此更高级的东西😁

```xml
<ResourceDictionary
    xmlns="https://schemas.microsoft.com/winfx/2006/xaml/presentation" 
    xmlns:x="https://schemas.microsoft.com/winfx/2006/xaml">
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
> **有关服务器端映像生成的说明**WPF 呈现器提供 `RenderCardToImageAsync` 可用于生成服务器端映像的方法。 仅 `ResourcesPath` 在此环境中使用属性时，才能使用此属性。 有关详细信息，请参阅[图像呈现](../net-image/getting-started.md)文档