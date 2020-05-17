---
title: 面向 Windows 开发人员的自适应卡片
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 39bdc64ed3244aca68d36c886a9562d964ded217
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "76145387"
---
# <a name="adaptive-cards-for-windows-developers"></a><span data-ttu-id="f5d8b-102">面向 Windows 开发人员的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="f5d8b-102">Adaptive Cards for Windows Developers</span></span>

## <a name="timeline"></a><span data-ttu-id="f5d8b-103">时间线</span><span class="sxs-lookup"><span data-stu-id="f5d8b-103">Timeline</span></span>

<span data-ttu-id="f5d8b-104">首项支持自适应卡片的 Windows 体验是时间线，这是首次在 Windows 10 1803 中引入的全新体验。</span><span class="sxs-lookup"><span data-stu-id="f5d8b-104">The first Windows experience to supports Adaptive Cards is Timeline, a brand new experience first introduced in Windows 10 1803.</span></span> 

![时间线](media/windows/timeline.png)

### <a name="useractivity-api"></a><span data-ttu-id="f5d8b-106">UserActivity API</span><span class="sxs-lookup"><span data-stu-id="f5d8b-106">UserActivity API</span></span>

<span data-ttu-id="f5d8b-107">可以通过 [`Windows.ApplicationModel.UserActivities.UserActivity`](https://docs.microsoft.com/uwp/api/windows.applicationmodel.useractivities.useractivity) API 将活动填充到时间线中。</span><span class="sxs-lookup"><span data-stu-id="f5d8b-107">The [`Windows.ApplicationModel.UserActivities.UserActivity`](https://docs.microsoft.com/uwp/api/windows.applicationmodel.useractivities.useractivity) API is what populates an Activity into Timeline.</span></span>

<span data-ttu-id="f5d8b-108">将通过 `VisualElement` 的 `Content` 属性提供自适应卡片，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f5d8b-108">The Adaptive Card will be supplied via the `Content` property of `VisualElement`, as seen below:</span></span>

```csharp
UserActivity userActivity = await channel.GetOrCreateUserActivityAsync(activityId, new HostName("contoso.com"));
userActivity.ActivationUri = new Uri("rss-reader:article?" + article.Link);
userActivity.DisplayText = article.Title; //used for details tile text
userActivity.VisualElements.Content = AdaptiveCardBuilder.CreateAdaptiveCardFromJson(jsonString);
await userActivity.SaveAsync();
```

### <a name="learning-module"></a><span data-ttu-id="f5d8b-109">学习模块</span><span class="sxs-lookup"><span data-stu-id="f5d8b-109">Learning Module</span></span>

<span data-ttu-id="f5d8b-110">这里有一个非常棒的 45 分钟的学习模块，其中包含了从头到尾的这些步骤。</span><span class="sxs-lookup"><span data-stu-id="f5d8b-110">There is a great 45-min learn module that covers these steps end-to-end.</span></span>

[<span data-ttu-id="f5d8b-111">将自适应卡集成到 Windows 10 时间线</span><span class="sxs-lookup"><span data-stu-id="f5d8b-111">Integrate adaptive cards into Windows 10 Timeline</span></span>](https://docs.microsoft.com/learn/modules/integrate-app-into-windows-10-timeline/)

### <a name="learn-more"></a><span data-ttu-id="f5d8b-112">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="f5d8b-112">Learn more</span></span>

<span data-ttu-id="f5d8b-113">Build 2017 的此次会议详细介绍了用户活动。</span><span class="sxs-lookup"><span data-stu-id="f5d8b-113">This session at Build 2017 covers User Activities in detial.</span></span>

<iframe src="https://channel9.msdn.com/Events/Build/2017/B8108/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="other-windows-surfaces"></a><span data-ttu-id="f5d8b-114">其他 Windows Surface</span><span class="sxs-lookup"><span data-stu-id="f5d8b-114">Other Windows Surfaces</span></span>
<span data-ttu-id="f5d8b-115">我们目前还没有任何可以透露的内容，但我们正在努力将自适应卡片引入到更多 Windows 体验中。</span><span class="sxs-lookup"><span data-stu-id="f5d8b-115">We don't have anything to share just yet, but we're working on incorporating Adaptive Cards into more Windows experiences.</span></span>

## <a name="dive-in"></a><span data-ttu-id="f5d8b-116">深入了解！</span><span class="sxs-lookup"><span data-stu-id="f5d8b-116">Dive in!</span></span>

<span data-ttu-id="f5d8b-117">在本教程中，我们只是介绍了一些粗浅的知识。若要了解自适应卡片的更多内容，请过不久再回来查看并浏览下面的链接。</span><span class="sxs-lookup"><span data-stu-id="f5d8b-117">We've barely scratched the surface in this tutorial, so check back soon and browse the links below to explore more about Adaptive Cards.</span></span>

* <span data-ttu-id="f5d8b-118">[浏览示例卡片](http://adaptivecards.io/samples/)获取灵感</span><span class="sxs-lookup"><span data-stu-id="f5d8b-118">[Browse Sample cards](http://adaptivecards.io/samples/) for inspiration</span></span>
* <span data-ttu-id="f5d8b-119">使用[架构资源管理器](http://adaptivecards.io/explorer)了解可用元素</span><span class="sxs-lookup"><span data-stu-id="f5d8b-119">Use the [Schema Explorer](http://adaptivecards.io/explorer) to learn the available elements</span></span>
* <span data-ttu-id="f5d8b-120">使用[交互式可视化工具](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)构建一张卡片</span><span class="sxs-lookup"><span data-stu-id="f5d8b-120">Build a card using the [Interactive Visualizer](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)</span></span>
* <span data-ttu-id="f5d8b-121">如果你有任何反馈，请[联系我们](http://adaptivecards.io/connect)</span><span class="sxs-lookup"><span data-stu-id="f5d8b-121">[Get in touch](http://adaptivecards.io/connect) with any feedback you have</span></span>
