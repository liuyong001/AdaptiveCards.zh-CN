---
title: 本机样式-UWP SDK
author: matthidinger
ms.author: mahiding
ms.date: 08/15/2018
ms.topic: article
ms.openlocfilehash: da3c7616ce4fe307eda3073f7037842e3e3df81b
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417522"
---
# <a name="native-styling---uwp"></a>本机样式-UWP

虽然主机配置在每个平台上都可获得大多数方法，但你可能需要在每个平台上执行一些本机样式。 

UWP 使你可以传递 ResourceDictionary 以实现精细的样式、行为、动画等，从而使其变得简单。

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
```
