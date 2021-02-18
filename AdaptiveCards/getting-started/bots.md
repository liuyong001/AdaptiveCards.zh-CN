---
title: 面向机器人开发人员的自适应卡片
author: matthidinger
ms.author: mahiding
ms.date: 05/30/2018
ms.topic: article
ms.openlocfilehash: 27b27cc004c03ddf7cb873cf67493407d3844ed5
ms.sourcegitcommit: 0ed81e04d8cdcf8f8bf6f854edf53b7eb9f67d2a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532588"
---
# <a name="adaptive-cards-for-bot-developers"></a><span data-ttu-id="0bd3d-102">面向机器人开发人员的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="0bd3d-102">Adaptive Cards for Bot Developers</span></span>

<span data-ttu-id="0bd3d-103">自适应卡片特别适合机器人。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-103">Adaptive Cards are a great fit for Bots.</span></span> <span data-ttu-id="0bd3d-104">借助自适应卡片，你只需创作卡片一次，然后就可以让它美观地呈现在多个应用（例如 Microsoft Teams、你自己的网站，等等）中。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-104">They let you author a card once and have it render beautifully inside multiple apps, like  Microsoft Teams, your own website, and more.</span></span>

> [!NOTE]
> <span data-ttu-id="0bd3d-105">目前的预览版不支持 Skype。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-105">Skype is not supported in the current preview.</span></span> <span data-ttu-id="0bd3d-106">请参阅[合作伙伴状态](../resources/partners.md)页，了解最新信息。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-106">See the [Partner Status](../resources/partners.md) page for the latest.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="0bd3d-107">试试吧</span><span class="sxs-lookup"><span data-stu-id="0bd3d-107">Try it out</span></span>

<span data-ttu-id="0bd3d-108">单击接下来的链接，[与我们的潜水机器人聊天](http://contososcubademo.azurewebsites.net/)。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-108">Click the following link and [talk to our Scuba Bot](http://contososcubademo.azurewebsites.net/).</span></span> <span data-ttu-id="0bd3d-109">说“`I'm looking for scuba`”，它就会帮助你预约梦想中的潜水之旅。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-109">Say `I'm looking for scuba` and it'll help you book the scuba trip of your dreams.</span></span>  

<span data-ttu-id="0bd3d-110">机器人的所有响应都是使用自适应卡片创建的。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-110">All of the bot's responses are created with Adaptive Cards.</span></span>

<span data-ttu-id="0bd3d-111">[![潜水聊天屏幕截图](media/bots/scuba-chat.png)](http://contososcubademo.azurewebsites.net/)</span><span class="sxs-lookup"><span data-stu-id="0bd3d-111">[![Scuba chat screenshot](media/bots/scuba-chat.png)](http://contososcubademo.azurewebsites.net/)</span></span>

<span data-ttu-id="0bd3d-112">**获取代码**：完整的 [Contoso 潜水机器人源代码](https://github.com/matthidinger/ContosoScubaBot
)可以在 GitHub 上找到。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-112">**Get the code**: the full [Contoso Scuba Bot source code](https://github.com/matthidinger/ContosoScubaBot
) can be found on GitHub.</span></span>


## <a name="bot-framework-integration"></a><span data-ttu-id="0bd3d-113">Bot Framework 集成</span><span class="sxs-lookup"><span data-stu-id="0bd3d-113">Bot Framework Integration</span></span>

<span data-ttu-id="0bd3d-114">可以使用 [Bot Framework](https://dev.botframework.com/) 编写一个机器人，该机器人可以跨多个“通道”（例如 Skype、Microsoft Teams、Facebook Messenger 等）与用户聊天。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-114">With the [Bot Framework](https://dev.botframework.com/) you can write a single bot that is able to chat with users across multiple "channels", like Skype, Microsoft Teams, Facebook Messenger, etc.</span></span>

## <a name="walkthrough"></a><span data-ttu-id="0bd3d-115">演练</span><span class="sxs-lookup"><span data-stu-id="0bd3d-115">Walkthrough</span></span>

<span data-ttu-id="0bd3d-116">向机器人添加自适应卡片很简单。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-116">It's pretty straight forward to add an Adaptive Card to your bot.</span></span>

### <a name="step-0-start-with-a-basic-message"></a><span data-ttu-id="0bd3d-117">步骤 0：从基本消息开始</span><span class="sxs-lookup"><span data-stu-id="0bd3d-117">Step 0: Start with a basic message</span></span>

<span data-ttu-id="0bd3d-118">下面是一个标准的 Bot Framework `message` 有效负载，该负载可以传递到任何通道，将文本显示给用户。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-118">Here's a standard Bot Framework `message` payload that can be delivered to any channel and display text to the user.</span></span>

```json
{
   "type": "message",
   "text": "Plain text is ok, but sometimes I long for more..."
}
```

### <a name="step-1-add-an-adaptive-card-attachment"></a><span data-ttu-id="0bd3d-119">步骤 1：添加自适应卡片 `attachment`</span><span class="sxs-lookup"><span data-stu-id="0bd3d-119">Step 1: Add an Adaptive Card `attachment`</span></span>

<span data-ttu-id="0bd3d-120">若要添加文本之外的内容，可以利用 Bot Framework 的 `attachments`。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-120">To add some richness beyond just text, the Bot Framework has a concept of `attachments`.</span></span> 

<span data-ttu-id="0bd3d-121">让我们附上一张显示自定义文本的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-121">Let's attach an Adaptive Card that displays custom text.</span></span>

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

### <a name="step-2-build-even-richer-cards"></a><span data-ttu-id="0bd3d-123">步骤 2：构建内容更丰富的卡片</span><span class="sxs-lookup"><span data-stu-id="0bd3d-123">Step 2: Build even richer cards</span></span> 

<span data-ttu-id="0bd3d-124">除了可自定义的文本，自适应卡片还提供更为丰富的内容。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-124">Adaptive Cards offer much more than just customizable text.</span></span> 

<span data-ttu-id="0bd3d-125">您可以：</span><span class="sxs-lookup"><span data-stu-id="0bd3d-125">You can:</span></span> 

* <span data-ttu-id="0bd3d-126">向卡片添加`Images`</span><span class="sxs-lookup"><span data-stu-id="0bd3d-126">Add `Images` to your card</span></span>
* <span data-ttu-id="0bd3d-127">使用`Containers`和`Columns`来组织内容</span><span class="sxs-lookup"><span data-stu-id="0bd3d-127">Organize your content with `Containers` and `Columns`</span></span>
* <span data-ttu-id="0bd3d-128">添加多种类型的`Actions`</span><span class="sxs-lookup"><span data-stu-id="0bd3d-128">Add multiple types of `Actions`</span></span>
* <span data-ttu-id="0bd3d-129">从用户收集`Input`</span><span class="sxs-lookup"><span data-stu-id="0bd3d-129">Collect `Input` from your users</span></span>
* <span data-ttu-id="0bd3d-130">让一张卡片`show another card`</span><span class="sxs-lookup"><span data-stu-id="0bd3d-130">Have one card `show another card`</span></span>
* <span data-ttu-id="0bd3d-131">[查看完整的架构资源管理器](https://adaptivecards.io/explorer/)！</span><span class="sxs-lookup"><span data-stu-id="0bd3d-131">[Check out the full schema explorer](https://adaptivecards.io/explorer/)!</span></span> 

## <a name="platform-sdks"></a><span data-ttu-id="0bd3d-132">平台 SDK</span><span class="sxs-lookup"><span data-stu-id="0bd3d-132">Platform SDKs</span></span>

<span data-ttu-id="0bd3d-133">如果你的机器人是使用 .NET 或 NodeJS 开发的，可以使用我们提供的库，这样可以更便捷地构建自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-133">If your bot is developed using .NET or NodeJS we have libraries to make building Adaptive Cards even easier.</span></span>

<span data-ttu-id="0bd3d-134">平台</span><span class="sxs-lookup"><span data-stu-id="0bd3d-134">Platform</span></span>|<span data-ttu-id="0bd3d-135">安装</span><span class="sxs-lookup"><span data-stu-id="0bd3d-135">Install</span></span>|<span data-ttu-id="0bd3d-136">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="0bd3d-136">Learn more</span></span>
--------|-------|----------
<span data-ttu-id="0bd3d-137">.NET</span><span class="sxs-lookup"><span data-stu-id="0bd3d-137">.NET</span></span> | `Install-Package AdaptiveCards -IncludePrerelease` | [<span data-ttu-id="0bd3d-138">Bot Framework .NET Docs</span><span class="sxs-lookup"><span data-stu-id="0bd3d-138">Bot Framework .NET Docs</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
<span data-ttu-id="0bd3d-139">NodeJS</span><span class="sxs-lookup"><span data-stu-id="0bd3d-139">NodeJS</span></span> | `npm install adaptivecards` | [<span data-ttu-id="0bd3d-140">Bot Framework NodeJS Docs</span><span class="sxs-lookup"><span data-stu-id="0bd3d-140">Bot Framework NodeJS Docs</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)


## <a name="channel-status"></a><span data-ttu-id="0bd3d-141">通道状态</span><span class="sxs-lookup"><span data-stu-id="0bd3d-141">Channel status</span></span>

<span data-ttu-id="0bd3d-142">可以通过 Bot Framework 将机器人发布到多个通道。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-142">The Bot Framework lets you publish your bot to multiple channels.</span></span> <span data-ttu-id="0bd3d-143">我们将与各个通道协作，为自适应卡片提供完整支持。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-143">We're working with various channels to provide full support for Adaptive Cards.</span></span> <span data-ttu-id="0bd3d-144">请参阅[合作伙伴状态](../resources/partners.md)页，了解最新信息。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-144">See the [Partner Status](../resources/partners.md) page for the latest.</span></span>


## <a name="dive-in"></a><span data-ttu-id="0bd3d-145">深入了解！</span><span class="sxs-lookup"><span data-stu-id="0bd3d-145">Dive in!</span></span>

<span data-ttu-id="0bd3d-146">在本教程中，我们只是介绍了一些粗浅的知识。若要了解如何使用自适应卡片以更多方式增强机器人，请查看下面的链接。</span><span class="sxs-lookup"><span data-stu-id="0bd3d-146">We've just scratched the surface in this tutorial, so please take a look at the links below to explore more ways that Adaptive Cards can enhance your bot.</span></span>

* <span data-ttu-id="0bd3d-147">[浏览示例卡片](https://adaptivecards.io/samples/)获取灵感</span><span class="sxs-lookup"><span data-stu-id="0bd3d-147">[Browse Sample cards](https://adaptivecards.io/samples/) for inspiration</span></span>
* <span data-ttu-id="0bd3d-148">使用[架构资源管理器](https://adaptivecards.io/explorer)了解可用元素</span><span class="sxs-lookup"><span data-stu-id="0bd3d-148">Use the [Schema Explorer](https://adaptivecards.io/explorer) to learn the available elements</span></span>
* <span data-ttu-id="0bd3d-149">使用[交互式可视化工具](https://adaptivecards.io/visualizer/index.html?hostApp=Skype)构建一张卡片</span><span class="sxs-lookup"><span data-stu-id="0bd3d-149">Build a card using the [Interactive Visualizer](https://adaptivecards.io/visualizer/index.html?hostApp=Skype)</span></span>
* <span data-ttu-id="0bd3d-150">如果你有任何反馈，请[联系我们](https://adaptivecards.io/connect)</span><span class="sxs-lookup"><span data-stu-id="0bd3d-150">[Get in touch](https://adaptivecards.io/connect) with any feedback you have</span></span>