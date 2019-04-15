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
# <a name="adaptive-cards-for-windows-developers"></a>面向 Windows 开发人员的自适应卡



## <a name="timeline"></a>时间线

第一个 Windows 体验对支持自适应卡是时间线，首次在 Windows 10 1803年中引入的全新体验。 

![时间线](media/windows/timeline.png)

### <a name="useractivity-api"></a>UserActivity API

[ `Windows.ApplicationModel.UserActivities.UserActivity` ](https://docs.microsoft.com/en-us/uwp/api/windows.applicationmodel.useractivities.useractivity) API 是什么填充到时间线中的活动。

将通过提供自适应卡`Content`属性的`VisualElement`，如下所示：

```csharp
UserActivity userActivity = await channel.GetOrCreateUserActivityAsync(activityId, new HostName("contoso.com"));
userActivity.ActivationUri = new Uri("rss-reader:article?" + article.Link);
userActivity.DisplayText = article.Title; //used for details tile text
userActivity.VisualElements.Content = AdaptiveCardBuilder.CreateAdaptiveCardFromJson(jsonString);
await userActivity.SaveAsync();
```

### <a name="learn-more"></a>了解详细信息

在 Build 2017 上此讲座介绍了在 detial 中的用户活动。

<iframe src="https://channel9.msdn.com/Events/Build/2017/B8108/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="other-windows-surfaces"></a>其他 Windows 表面
我们没有任何共享，但我们正致力于将自适应卡合并到更多 Windows 体验。

## <a name="dive-in"></a>深入了解 ！

因此我们已几乎不能简单介绍了在本教程中稍后再查看和浏览以下链接，详细了解自适应卡。

* [浏览示例卡](http://adaptivecards.io/samples/)激发灵感
* 使用[架构资源管理器](http://adaptivecards.io/explorer)若要了解可用元素
* 生成卡使用[交互式可视化工具](http://adaptivecards.io/visualizer/index.html?hostApp=Skype)
* [与我们联系](http://adaptivecards.io/connect)与你有任何反馈
