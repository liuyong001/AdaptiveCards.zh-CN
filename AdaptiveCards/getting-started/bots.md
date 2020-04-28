---
title: 面向机器人开发人员的自适应卡片
author: matthidinger
ms.author: mahiding
ms.date: 05/30/2018
ms.topic: article
ms.openlocfilehash: 1c3ad2a4588244a8bd30011a4b6e25e37062624a
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "76145377"
---
# <a name="adaptive-cards-for-bot-developers"></a>面向机器人开发人员的自适应卡片

自适应卡片特别适合机器人。 借助自适应卡片，你只需创作卡片一次，然后就可以让它美观地呈现在多个应用（例如 Microsoft Teams、你自己的网站，等等）中。

> [!NOTE]
> 目前的预览版不支持 Skype。 请参阅[合作伙伴状态](../resources/partners.md)页，了解最新信息。

## <a name="try-it-out"></a>试试吧

单击接下来的链接，[与我们的潜水机器人聊天](http://contososcubademo.azurewebsites.net/)。 说“`I'm looking for scuba`”，它就会帮助你预约梦想中的潜水之旅。  

机器人的所有响应都是使用自适应卡片创建的。

[![潜水聊天屏幕截图](media/bots/scuba-chat.png)](http://contososcubademo.azurewebsites.net/)

**获取代码**：完整的 [Contoso 潜水机器人源代码](https://github.com/matthidinger/ContosoScubaBot
)可以在 GitHub 上找到。


## <a name="bot-framework-integration"></a>Bot Framework 集成

可以使用 [Bot Framework](https://dev.botframework.com/) 编写一个机器人，该机器人可以跨多个“通道”（例如 Skype、Microsoft Teams、Facebook Messenger 等）与用户聊天。

## <a name="walkthrough"></a>演练

向机器人添加自适应卡片很简单。

### <a name="step-0-start-with-a-basic-message"></a>步骤 0：从基本消息开始

下面是一个标准的 Bot Framework `message` 有效负载，该负载可以传递到任何通道，将文本显示给用户。

```json
{
   "type": "message",
   "text": "Plain text is ok, but sometimes I long for more..."
}
```

### <a name="step-1-add-an-adaptive-card-attachment"></a>步骤 1：添加自适应卡片 `attachment`

若要添加文本之外的内容，可以利用 Bot Framework 的 `attachments`。 

让我们附上一张显示自定义文本的自适应卡片。

![基本的自适应卡片](media/bots/hello-adaptivecards.png)

```json
{
  "type": "message",
  "text": "Plain text is ok, but sometimes I long for more...",
  "attachments": [
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "TextBlock",
            "text": "Hello World!",
            "size": "large"
          },
          {
            "type": "TextBlock",
            "text": "*Sincerely yours,*"
          },
          {
            "type": "TextBlock",
            "text": "Adaptive Cards",
            "separation": "none"
          }
        ],
        "actions": [
          {
            "type": "Action.OpenUrl",
            "url": "http://adaptivecards.io",
            "title": "Learn More"
          }
        ]
      }
    }
  ]
}
```

### <a name="step-2-build-even-richer-cards"></a>步骤 2：构建内容更丰富的卡片 

除了可自定义的文本，自适应卡片还提供更为丰富的内容。 

您可以： 

* 向卡片添加`Images`
* 使用`Containers`和`Columns`来组织内容
* 添加多种类型的`Actions`
* 从用户收集`Input`
* 让一张卡片`show another card`
* [查看完整的架构资源管理器](http://adaptivecards.io/explorer/)！ 

## <a name="platform-sdks"></a>平台 SDK

如果你的机器人是使用 .NET 或 NodeJS 开发的，可以使用我们提供的库，这样可以更便捷地构建自适应卡片。

平台|安装|了解详细信息
--------|-------|----------
.NET | `Install-Package AdaptiveCards -IncludePrerelease` | [Bot Framework .NET Docs](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
NodeJS | `npm install adaptivecards` | [Bot Framework NodeJS Docs](https://docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)


## <a name="channel-status"></a>通道状态

可以通过 Bot Framework 将机器人发布到多个通道。 我们将与各个通道协作，为自适应卡片提供完整支持。 请参阅[合作伙伴状态](../resources/partners.md)页，了解最新信息。


## <a name="dive-in"></a>深入了解！

在本教程中，我们只是介绍了一些粗浅的知识。若要了解如何使用自适应卡片以更多方式增强机器人，请查看下面的链接。

* [浏览示例卡片](http://adaptivecards.io/samples/)获取灵感
* 使用[架构资源管理器](http://adaptivecards.io/explorer)了解可用元素
* 使用[交互式可视化工具](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)构建一张卡片
* 如果你有任何反馈，请[联系我们](http://adaptivecards.io/connect)
