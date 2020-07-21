---
title: 模板化概述
author: matthidinger
ms.author: mahiding
ms.date: 05/18/2020
ms.topic: article
ms.openlocfilehash: 41eb972603b1688a1f1857cec83208b9b55b02c3
ms.sourcegitcommit: fec0fd2c23293127e8e8f7ca7821c04d46987f37
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86417615"
---
# <a name="adaptive-cards-templating"></a>自适应卡片模板化

我们很高兴与大家一起预览用于**创建**、**重复使用**和**共享**自适应卡片的新工具。 

> [!IMPORTANT] 
> 
> **2020 年 5 月候选发布版本**中的**中断性变更**
>
> 如果你使用的是较旧的包，那么你应了解该模板化候选发布版本包含的一些较小的中断性变更。 请参见以下详细内容。


## <a name="breaking-changes-as-of-may-2020"></a>2020 年 5 月起的中断性变更

1. 绑定语法已从 `{...}` 更改为 `${...}`。 
    * 例如：`"text": "Hello {name}"` 变为 `"text": "Hello ${name}"`
2. JavaScript API 不再包含 `EvaluationContext` 对象。 只需将数据传递到 `expand` 函数。 有关完整的详细信息，请参阅 [SDK 页](sdk.md)。
3. .NET API 经过了重新设计，以便更紧密地匹配 JavaScript API。 有关完整的详细信息，请参阅 [SDK 页](sdk.md)。

## <a name="how-can-templating-help-you"></a>模板化对你有何帮助

模板化可以将自适应卡片中的**数据**与**布局**分开。 

### <a name="it-helps-design-a-card-once-and-then-populate-it-with-real-data"></a>只需设计卡片一次，然后为其填充实际数据即可

目前不可能使用[自适应卡片设计器](https://adaptivecards.io/designer)来创建卡片并使用该 JSON 为有效负载填充**动态内容**。 为此，必须编写自定义代码来构建 JSON 字符串，或使用对象模型 SDK 来构建表示卡片的 OM 并将其序列化为 JSON。 不管什么情况，设计器执行的是一次性单向操作，一旦将卡片设计转换为代码，就不容易在以后调整它。

### <a name="it-makes-transmissions-over-the-wire-smaller"></a>降低通过网络传输的数据的大小

想象一下，如果可以**直接在客户端上**将模板和数据组合在一起，会是一种什么情景。 这意味着，如果多次使用同一模板，或者要使用新数据来更新它，只需将新数据发送到设备即可，设备可以反复使用同一模板。

### <a name="it-helps-you-create-a-great-looking-card-from-just-the-data-you-provide"></a>直接使用所提供的数据创建外观优美的卡片

我们都认为自适应卡片很好，而如果你不需为需要显示给用户的所有内容编写自适应卡片，那不是好上加好吗？ 有了模板服务（在下面介绍），我们就可以让所有人都能贡献、发现和共享模板，不管使用什么类型的数据。 

可以在自己的项目内和组织中共享，也可以在整个 Internet 中共享。

### <a name="ai-and-other-services-could-improve-user-experiences"></a>AI 和其他服务可以改善用户体验

将数据与内容分开，AI 和其他服务就可以针对我们在卡片中看到的数据进行“推断”，提高用户工作效率，或者帮助我们找到所要的东西。

## <a name="what-is-adaptive-cards-templating"></a>什么是自适应卡片模板化？

它包含 3 个主要组件：

1. **[模板语言](language.md)** ：是用于创作模板的语法。 设计器甚至包含“示例数据”，让你在设计时预览模板。
2. **[模板化 SDK](sdk.md)** ：将存在于所有受支持的自适应卡片平台上。 可以通过这些 SDK 在后端或者直接在客户端为模板填充实际数据。 
3. **[模板服务](service.md)** ：是一项概念证明服务，允许任何人查找、贡献以及共享一组已知的模板。

## <a name="template-language"></a>模板语言

模板语言是用于创作自适应卡片模板的语法。 

> [!NOTE]
> 
> 打开一个新的标签页，按以下示例操作
>
> **https://adaptivecards.io/designer**
> 
> 单击“预览模式”按钮，在设计模式和预览模式之间切换。

![设计器屏幕截图](content/2019-08-01-13-58-27.png)

新更新的设计器添加了相关支持，允许用户创作模板，并提供用于在设计时预览卡片的**示例数据**。

请将以下示例粘贴到“卡片有效负载编辑器”窗格中： 

**EmployeeCardTemplate.json**

```json
{
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "ColumnSet",
            "style": "accent",
            "bleed": true,
            "columns": [
                {
                    "type": "Column",
                    "width": "auto",
                    "items": [
                        {
                            "type": "Image",
                            "url": "${photo}",
                            "altText": "Profile picture",
                            "size": "Small",
                            "style": "Person"
                        }
                    ]
                },
                {
                    "type": "Column",
                    "width": "stretch",
                    "items": [
                        {
                            "type": "TextBlock",
                            "text": "Hi ${name}!",
                            "size": "Medium"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Here's a bit about your org...",
                            "spacing": "None"
                        }
                    ]
                }
            ]
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: **${manager.name}**"
        },
        {
            "type": "TextBlock",
            "text": "Your peers are:"
        },
        {
            "type": "FactSet",
            "facts": [
                {
                    "$data": "${peers}",
                    "title": "${name}",
                    "value": "${title}"
                }
            ]
        }
    ]
}
```

然后，将以下 JSON 数据粘贴到**示例数据编辑器**中。 

**示例数据**可以让你了解卡片在运行时（此时会传递实际数据）的具体外观。

**EmployeeData**

```json
{
    "name": "Matt",
    "photo": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
    "manager": {
        "name": "Thomas",
        "title": "PM Lead"
    },
    "peers": [
        {
            "name": "Lei",
            "title": "Sr Program Manager"
        },
        {
            "name": "Andrew",
            "title": "Program Manager II"
        },
        {
            "name": "Mary Anne",
            "title": "Program Manager"
        }
    ]
}
```

单击“预览模式”按钮。 此时会看到卡片按上面提供的示例数据进行呈现。 可以随意调整示例数据，观察卡片进行实时更新。

**祝贺**，你刚刚创作了你的第一个自适应卡片模板！ 接下来，让我们了解如何为模板填充实际数据。

> 详细了解[目标语言](language.md)

## <a name="sdk-support"></a>SDK 支持

有了模板化 SDK，就可以为模板填充实际数据。

> [!NOTE]
>
> 目前已提供了适用于 .NET 和 NodeJS 的模板化 SDK。 随着时间的推移，我们将为所有剩余的自适应卡片平台（如 iOS、Android、UWP 等）发布模板化 SDK。

平台 | 程序包 | 安装 | 文档
--- | --- | --- | ---
JavaScript | [![npm install](https://img.shields.io/npm/v/adaptivecards-templating.svg)](https://www.npmjs.com/package/adaptivecards-templating) | `npm install adaptivecards-templating` | [文档](https://www.npmjs.com/package/adaptivecards-templating)
.NET | [![Nuget 安装](https://img.shields.io/nuget/vpre/AdaptiveCards.Templating.svg)](https://www.nuget.org/packages/AdaptiveCards.Templating) | `dotnet add package AdaptiveCards.Templating` | [文档](https://docs.microsoft.com/adaptive-cards/templating/sdk#net)

### <a name="javascript-example"></a>JavaScript 示例

以下 JavaScript 演示了将要用来为模板填充数据的常规模式。

```js
var template = new ACData.Template({ 
    // Card Template JSON
});

var card = template.expand({
    $root: {
        // Data Fields
    }
});

// Now you have an AdaptiveCard ready to render!
```

### <a name="c-example"></a>C# 示例

以下 C# 演示了将要用来为模板填充数据的常规模式。

```csharp
var template = new AdaptiveCards.Templating.AdaptiveCardTemplate(cardJson);
   
var card = template.Expand(new {Key="Value"});

// Now you have an AdaptiveCard ready to render!
```

> 详细了解[模板化 SDK](sdk.md)

## <a name="template-service"></a>模板服务

自适应卡片模板服务是一项概念证明服务，允许任何人查找、贡献以及共享一组已知的模板。

如果你要显示一些数据，但不想为其编写自定义的自适应卡片，则可使用此服务。

获取模板的 API 相当直观，但此服务实际上提供很多功能，包括分析数据并查找合适模板的功能。

`HTTP GET https://templates.adaptivecards.io/graph.microsoft.com/Profile.json`

所有模板都是存储在 GitHub 存储库中的平面 JSON 文件，因此任何人都可以为其贡献内容，就像为任何其他的开源代码贡献内容一样。

> 详细了解[卡片模板服务](service.md)

## <a name="whats-next-and-sending-feedback"></a>后续内容和发送反馈

我们已经实现了模板化并将呈现方式与数据进行了分离，这使我们离“建立一个生态系统，用来以标准化的方式在应用和服务之间交换内容”的目标更进了一步。 我们已准备在这一方面提供许多功能，因此请在 [GitHub](https://github.com/Microsoft/AdaptiveCards/issues)上随时了解最新信息，并告诉我们在你使用这些功能时它们的运行状况如何。
