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
# <a name="adaptive-cards-for-bot-developers"></a><span data-ttu-id="a4379-102">智能机器人应用程序开发人员的的自适应卡</span><span class="sxs-lookup"><span data-stu-id="a4379-102">Adaptive Cards for Bot Developers</span></span>

<span data-ttu-id="a4379-103">自适应卡是非常适合用于智能机器人。</span><span class="sxs-lookup"><span data-stu-id="a4379-103">Adaptive Cards are a great fit for Bots.</span></span> <span data-ttu-id="a4379-104">它们使你一次编写一个卡，并将其美观地呈现在多个应用，如 Microsoft Teams、 你自己的网站，和的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a4379-104">They let you author a card once and have it render beautifully inside multiple apps, like  Microsoft Teams, your own website, and more.</span></span>

> [!NOTE]
> <span data-ttu-id="a4379-105">Skype 不支持在当前的预览版。</span><span class="sxs-lookup"><span data-stu-id="a4379-105">Skype is not supported in the current preview.</span></span> <span data-ttu-id="a4379-106">请参阅[合作伙伴状态](../resources/partners.md)有关最新的页。</span><span class="sxs-lookup"><span data-stu-id="a4379-106">See the [Partner Status](../resources/partners.md) page for the latest.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="a4379-107">试用</span><span class="sxs-lookup"><span data-stu-id="a4379-107">Try it out</span></span>

<span data-ttu-id="a4379-108">单击以下链接并[与我们的潜水机器人](http://contososcubademo.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="a4379-108">Click the following link and [talk to our Scuba Bot](http://contososcubademo.azurewebsites.net/).</span></span> <span data-ttu-id="a4379-109">假设`I'm looking for scuba`，它将帮助你预订您梦想名潜水行程。</span><span class="sxs-lookup"><span data-stu-id="a4379-109">Say `I'm looking for scuba` and it'll help you book the scuba trip of your dreams.</span></span>  

<span data-ttu-id="a4379-110">使用自适应卡创建所有的智能机器人应用程序的响应。</span><span class="sxs-lookup"><span data-stu-id="a4379-110">All of the bot's responses are created with Adaptive Cards.</span></span>

<span data-ttu-id="a4379-111">[![名潜水聊天屏幕快照](media/bots/scuba-chat.png)](http://contososcubademo.azurewebsites.net/)</span><span class="sxs-lookup"><span data-stu-id="a4379-111">[![Scuba chat screenshot](media/bots/scuba-chat.png)](http://contososcubademo.azurewebsites.net/)</span></span>

<span data-ttu-id="a4379-112">**获取代码**： 完整[Contoso 名潜水智能机器人应用程序源代码](https://github.com/matthidinger/ContosoScubaBot
)可在 GitHub 上找到。</span><span class="sxs-lookup"><span data-stu-id="a4379-112">**Get the code**: the full [Contoso Scuba Bot source code](https://github.com/matthidinger/ContosoScubaBot
) can be found on GitHub.</span></span>


## <a name="bot-framework-integration"></a><span data-ttu-id="a4379-113">智能机器人应用程序框架集成</span><span class="sxs-lookup"><span data-stu-id="a4379-113">Bot Framework Integration</span></span>

<span data-ttu-id="a4379-114">与[Bot Framework](https://dev.botframework.com/)可以编写单个智能机器人，如 Skype、 Microsoft Teams、 Facebook Messenger 等能够与跨多个"通道"，用户聊天应用程序。</span><span class="sxs-lookup"><span data-stu-id="a4379-114">With the [Bot Framework](https://dev.botframework.com/) you can write a single bot that is able to chat with users across multiple "channels", like Skype, Microsoft Teams, Facebook Messenger, etc.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="a4379-115">演练</span><span class="sxs-lookup"><span data-stu-id="a4379-115">Walkthrough</span></span>

<span data-ttu-id="a4379-116">它非常简洁将自适应卡添加到智能机器人。</span><span class="sxs-lookup"><span data-stu-id="a4379-116">It's pretty straight forward to add an Adaptive Card to your bot.</span></span>

### <a name="step-0-start-with-a-basic-message"></a><span data-ttu-id="a4379-117">步骤 0:开始一个基本的消息</span><span class="sxs-lookup"><span data-stu-id="a4379-117">Step 0: Start with a basic message</span></span>

<span data-ttu-id="a4379-118">下面是一个标准的智能机器人应用程序框架`message`可以传递到任何通道，并且向用户显示文本的有效负载。</span><span class="sxs-lookup"><span data-stu-id="a4379-118">Here's a standard Bot Framework `message` payload that can be delivered to any channel and display text to the user.</span></span>

```json
{
   "type": "message",
   "text": "Plain text is ok, but sometimes I long for more..."
}
```

### <a name="step-1-add-an-adaptive-card-attachment"></a><span data-ttu-id="a4379-119">第 1 步：添加自适应卡 `attachment`</span><span class="sxs-lookup"><span data-stu-id="a4379-119">Step 1: Add an Adaptive Card `attachment`</span></span>

<span data-ttu-id="a4379-120">若要添加一些超出只包含文本的丰富性，Bot Framework 有一个的概念`attachments`。</span><span class="sxs-lookup"><span data-stu-id="a4379-120">To add some richness beyond just text, the Bot Framework has a concept of `attachments`.</span></span> 

<span data-ttu-id="a4379-121">让我们将附加自适应卡用于显示自定义文本。</span><span class="sxs-lookup"><span data-stu-id="a4379-121">Let's attach an Adaptive Card that displays custom text.</span></span>

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

### <a name="step-2-build-even-richer-cards"></a><span data-ttu-id="a4379-123">步骤 2：构建更丰富的卡</span><span class="sxs-lookup"><span data-stu-id="a4379-123">Step 2: Build even richer cards</span></span> 

<span data-ttu-id="a4379-124">自适应卡提供远不只是可自定义文本。</span><span class="sxs-lookup"><span data-stu-id="a4379-124">Adaptive Cards offer much more than just customizable text.</span></span> 

<span data-ttu-id="a4379-125">你可以：</span><span class="sxs-lookup"><span data-stu-id="a4379-125">You can:</span></span> 

* <span data-ttu-id="a4379-126">添加`Images`到您的卡</span><span class="sxs-lookup"><span data-stu-id="a4379-126">Add `Images` to your card</span></span>
* <span data-ttu-id="a4379-127">组织与内容`Containers`和 `Columns`</span><span class="sxs-lookup"><span data-stu-id="a4379-127">Organize your content with `Containers` and `Columns`</span></span>
* <span data-ttu-id="a4379-128">添加多个类型的 `Actions`</span><span class="sxs-lookup"><span data-stu-id="a4379-128">Add multiple types of `Actions`</span></span>
* <span data-ttu-id="a4379-129">收集`Input`从你的用户</span><span class="sxs-lookup"><span data-stu-id="a4379-129">Collect `Input` from your users</span></span>
* <span data-ttu-id="a4379-130">有一张卡 `show another card`</span><span class="sxs-lookup"><span data-stu-id="a4379-130">Have one card `show another card`</span></span>
* <span data-ttu-id="a4379-131">[请查看完整架构资源管理器](http://adaptivecards.io/explorer/)！</span><span class="sxs-lookup"><span data-stu-id="a4379-131">[Check out the full schema explorer](http://adaptivecards.io/explorer/)!</span></span> 

## <a name="platform-sdks"></a><span data-ttu-id="a4379-132">平台 Sdk</span><span class="sxs-lookup"><span data-stu-id="a4379-132">Platform SDKs</span></span>

<span data-ttu-id="a4379-133">如果使用.NET 或 NodeJS 开发智能机器人还有库来简化构建自适应卡更容易。</span><span class="sxs-lookup"><span data-stu-id="a4379-133">If your bot is developed using .NET or NodeJS we have libraries to make building Adaptive Cards even easier.</span></span>

<span data-ttu-id="a4379-134">平台</span><span class="sxs-lookup"><span data-stu-id="a4379-134">Platform</span></span>|<span data-ttu-id="a4379-135">安装</span><span class="sxs-lookup"><span data-stu-id="a4379-135">Install</span></span>|<span data-ttu-id="a4379-136">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="a4379-136">Learn more</span></span>
--------|-------|----------
<span data-ttu-id="a4379-137">.NET</span><span class="sxs-lookup"><span data-stu-id="a4379-137">.NET</span></span> | `Install-Package AdaptiveCards -IncludePrerelease` | [<span data-ttu-id="a4379-138">Bot Framework.NET 文档</span><span class="sxs-lookup"><span data-stu-id="a4379-138">Bot Framework .NET Docs</span></span>](https://docs.microsoft.com/en-us/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
<span data-ttu-id="a4379-139">NodeJS</span><span class="sxs-lookup"><span data-stu-id="a4379-139">NodeJS</span></span> | `npm install adaptivecards` | [<span data-ttu-id="a4379-140">Bot Framework NodeJS Docs</span><span class="sxs-lookup"><span data-stu-id="a4379-140">Bot Framework NodeJS Docs</span></span>](https://docs.microsoft.com/en-us/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)


## <a name="channel-status"></a><span data-ttu-id="a4379-141">通道状态</span><span class="sxs-lookup"><span data-stu-id="a4379-141">Channel status</span></span>

<span data-ttu-id="a4379-142">Bot Framework，可以向多个渠道发布智能机器人。</span><span class="sxs-lookup"><span data-stu-id="a4379-142">The Bot Framework lets you publish your bot to multiple channels.</span></span> <span data-ttu-id="a4379-143">我们正在使用不同的通道提供的自适应卡完全支持。</span><span class="sxs-lookup"><span data-stu-id="a4379-143">We're working with various channels to provide full support for Adaptive Cards.</span></span> <span data-ttu-id="a4379-144">请参阅[合作伙伴状态](../resources/partners.md)有关最新的页。</span><span class="sxs-lookup"><span data-stu-id="a4379-144">See the [Partner Status](../resources/partners.md) page for the latest.</span></span>


## <a name="dive-in"></a><span data-ttu-id="a4379-145">深入了解 ！</span><span class="sxs-lookup"><span data-stu-id="a4379-145">Dive in!</span></span>

<span data-ttu-id="a4379-146">我们已只是简单介绍了在本教程中，因此请查看以下链接，了解更多自适应卡可以提高智能机器人的方法。</span><span class="sxs-lookup"><span data-stu-id="a4379-146">We've just scratched the surface in this tutorial, so please take a look at the links below to explore more ways that Adaptive Cards can enhance your bot.</span></span>

* <span data-ttu-id="a4379-147">[浏览示例卡](http://adaptivecards.io/samples/)激发灵感</span><span class="sxs-lookup"><span data-stu-id="a4379-147">[Browse Sample cards](http://adaptivecards.io/samples/) for inspiration</span></span>
* <span data-ttu-id="a4379-148">使用[架构资源管理器](http://adaptivecards.io/explorer)若要了解可用元素</span><span class="sxs-lookup"><span data-stu-id="a4379-148">Use the [Schema Explorer](http://adaptivecards.io/explorer) to learn the available elements</span></span>
* <span data-ttu-id="a4379-149">生成卡使用[交互式可视化工具](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)</span><span class="sxs-lookup"><span data-stu-id="a4379-149">Build a card using the [Interactive Visualizer](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)</span></span>
* <span data-ttu-id="a4379-150">[与我们联系](http://adaptivecards.io/connect)与你有任何反馈</span><span class="sxs-lookup"><span data-stu-id="a4379-150">[Get in touch](http://adaptivecards.io/connect) with any feedback you have</span></span>
