---
title: 面向 Windows 开发人员的自适应卡
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 20b324c12cd7cec10f2142fc2cf76039b5c329de
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552849"
---
# <a name="adaptive-cards-for-windows-developers"></a><span data-ttu-id="ee894-102">面向 Windows 开发人员的自适应卡</span><span class="sxs-lookup"><span data-stu-id="ee894-102">Adaptive Cards for Windows Developers</span></span>



## <a name="timeline"></a><span data-ttu-id="ee894-103">时间线</span><span class="sxs-lookup"><span data-stu-id="ee894-103">Timeline</span></span>

<span data-ttu-id="ee894-104">第一个 Windows 体验对支持自适应卡是时间线，首次在 Windows 10 1803年中引入的全新体验。</span><span class="sxs-lookup"><span data-stu-id="ee894-104">The first Windows experience to supports Adaptive Cards is Timeline, a brand new experience first introduced in Windows 10 1803.</span></span> 

![时间线](media/windows/timeline.png)

### <a name="useractivity-api"></a><span data-ttu-id="ee894-106">UserActivity API</span><span class="sxs-lookup"><span data-stu-id="ee894-106">UserActivity API</span></span>

<span data-ttu-id="ee894-107">[ `Windows.ApplicationModel.UserActivities.UserActivity` ](https://docs.microsoft.com/en-us/uwp/api/windows.applicationmodel.useractivities.useractivity) API 是什么填充到时间线中的活动。</span><span class="sxs-lookup"><span data-stu-id="ee894-107">The [`Windows.ApplicationModel.UserActivities.UserActivity`](https://docs.microsoft.com/en-us/uwp/api/windows.applicationmodel.useractivities.useractivity) API is what populates an Activity into Timeline.</span></span>

<span data-ttu-id="ee894-108">将通过提供自适应卡`Content`属性的`VisualElement`，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ee894-108">The Adaptive Card will be supplied via the `Content` property of `VisualElement`, as seen below:</span></span>

```csharp
UserActivity userActivity = await channel.GetOrCreateUserActivityAsync(activityId, new HostName("contoso.com"));
userActivity.ActivationUri = new Uri("rss-reader:article?" + article.Link);
userActivity.DisplayText = article.Title; //used for details tile text
userActivity.VisualElements.Content = AdaptiveCardBuilder.CreateAdaptiveCardFromJson(jsonString);
await userActivity.SaveAsync();
```

### <a name="learn-more"></a><span data-ttu-id="ee894-109">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="ee894-109">Learn more</span></span>

<span data-ttu-id="ee894-110">在 Build 2017 上此讲座介绍了在 detial 中的用户活动。</span><span class="sxs-lookup"><span data-stu-id="ee894-110">This session at Build 2017 covers User Activities in detial.</span></span>

<iframe src="https://channel9.msdn.com/Events/Build/2017/B8108/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="other-windows-surfaces"></a><span data-ttu-id="ee894-111">其他 Windows 表面</span><span class="sxs-lookup"><span data-stu-id="ee894-111">Other Windows Surfaces</span></span>
<span data-ttu-id="ee894-112">我们没有任何共享，但我们正致力于将自适应卡合并到更多 Windows 体验。</span><span class="sxs-lookup"><span data-stu-id="ee894-112">We don't have anything to share just yet, but we're working on incorporating Adaptive Cards into more Windows experiences.</span></span>

## <a name="dive-in"></a><span data-ttu-id="ee894-113">深入了解 ！</span><span class="sxs-lookup"><span data-stu-id="ee894-113">Dive in!</span></span>

<span data-ttu-id="ee894-114">因此我们已几乎不能简单介绍了在本教程中稍后再查看和浏览以下链接，详细了解自适应卡。</span><span class="sxs-lookup"><span data-stu-id="ee894-114">We've barely scratched the surface in this tutorial, so check back soon and browse the links below to explore more about Adaptive Cards.</span></span>

* <span data-ttu-id="ee894-115">[浏览示例卡](http://adaptivecards.io/samples/)激发灵感</span><span class="sxs-lookup"><span data-stu-id="ee894-115">[Browse Sample cards](http://adaptivecards.io/samples/) for inspiration</span></span>
* <span data-ttu-id="ee894-116">使用[架构资源管理器](http://adaptivecards.io/explorer)若要了解可用元素</span><span class="sxs-lookup"><span data-stu-id="ee894-116">Use the [Schema Explorer](http://adaptivecards.io/explorer) to learn the available elements</span></span>
* <span data-ttu-id="ee894-117">生成卡使用[交互式可视化工具](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)</span><span class="sxs-lookup"><span data-stu-id="ee894-117">Build a card using the [Interactive Visualizer](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)</span></span>
* <span data-ttu-id="ee894-118">[与我们联系](http://adaptivecards.io/connect)与你有任何反馈</span><span class="sxs-lookup"><span data-stu-id="ee894-118">[Get in touch](http://adaptivecards.io/connect) with any feedback you have</span></span>
