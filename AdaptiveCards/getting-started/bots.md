---
title: 智能机器人应用程序开发人员的的自适应卡
author: matthidinger
ms.author: mahiding
ms.date: 05/30/2018
ms.topic: article
ms.openlocfilehash: 1acc30c0347ea5527de2af1fe74e605c7589cbc6
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553279"
---
# <a name="adaptive-cards-for-bot-developers"></a>智能机器人应用程序开发人员的的自适应卡

自适应卡是非常适合用于智能机器人。 它们使你一次编写一个卡，并将其美观地呈现在多个应用，如 Microsoft Teams、 你自己的网站，和的详细信息。

> [!NOTE]
> Skype 不支持在当前的预览版。 请参阅[合作伙伴状态](../resources/partners.md)有关最新的页。

## <a name="try-it-out"></a>试用

单击以下链接并[与我们的潜水机器人](http://contososcubademo.azurewebsites.net/)。 假设`I'm looking for scuba`，它将帮助你预订您梦想名潜水行程。  

使用自适应卡创建所有的智能机器人应用程序的响应。

[![名潜水聊天屏幕快照](media/bots/scuba-chat.png)](http://contososcubademo.azurewebsites.net/)

**获取代码**： 完整[Contoso 名潜水智能机器人应用程序源代码](https://github.com/matthidinger/ContosoScubaBot
)可在 GitHub 上找到。


## <a name="bot-framework-integration"></a>智能机器人应用程序框架集成

与[Bot Framework](https://dev.botframework.com/)可以编写单个智能机器人，如 Skype、 Microsoft Teams、 Facebook Messenger 等能够与跨多个"通道"，用户聊天应用程序。

## <a name="walkthrough"></a>演练

它非常简洁将自适应卡添加到智能机器人。

### <a name="step-0-start-with-a-basic-message"></a>步骤 0:开始一个基本的消息

下面是一个标准的智能机器人应用程序框架`message`可以传递到任何通道，并且向用户显示文本的有效负载。

```json
{
   "type": "message",
   "text": "Plain text is ok, but sometimes I long for more..."
}
```

### <a name="step-1-add-an-adaptive-card-attachment"></a>第 1 步：添加自适应卡 `attachment`

若要添加一些超出只包含文本的丰富性，Bot Framework 有一个的概念`attachments`。 

让我们将附加自适应卡用于显示自定义文本。

![基本的自适应卡](media/bots/hello-adaptivecards.png)

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

### <a name="step-2-build-even-richer-cards"></a>步骤 2：构建更丰富的卡 

自适应卡提供远不只是可自定义文本。 

你可以： 

* 添加`Images`到您的卡
* 组织与内容`Containers`和 `Columns`
* 添加多个类型的 `Actions`
* 收集`Input`从你的用户
* 有一张卡 `show another card`
* [请查看完整架构资源管理器](http://adaptivecards.io/explorer/)！ 

## <a name="platform-sdks"></a>平台 Sdk

如果使用.NET 或 NodeJS 开发智能机器人还有库来简化构建自适应卡更容易。

平台|安装|了解详细信息
--------|-------|----------
.NET | `Install-Package AdaptiveCards -IncludePrerelease` | [Bot Framework.NET 文档](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
NodeJS | `npm install adaptivecards` | [Bot Framework NodeJS Docs](https://docs.microsoft.com/en-us/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)


## <a name="channel-status"></a>通道状态

Bot Framework，可以向多个渠道发布智能机器人。 我们正在使用不同的通道提供的自适应卡完全支持。 请参阅[合作伙伴状态](../resources/partners.md)有关最新的页。


## <a name="dive-in"></a>深入了解 ！

我们已只是简单介绍了在本教程中，因此请查看以下链接，了解更多自适应卡可以提高智能机器人的方法。

* [浏览示例卡](http://adaptivecards.io/samples/)激发灵感
* 使用[架构资源管理器](http://adaptivecards.io/explorer)若要了解可用元素
* 生成卡使用[交互式可视化工具](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)
* [与我们联系](http://adaptivecards.io/connect)与你有任何反馈
