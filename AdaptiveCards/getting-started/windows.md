---
title: 面向 Windows 开发人员的自适应卡片
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 076add9a677af55c109ee65858841fd9efbd9f32
ms.sourcegitcommit: 0ed81e04d8cdcf8f8bf6f854edf53b7eb9f67d2a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532578"
---
# <a name="adaptive-cards-for-windows-developers"></a>面向 Windows 开发人员的自适应卡片

## <a name="timeline"></a>时间线

首项支持自适应卡片的 Windows 体验是时间线，这是首次在 Windows 10 1803 中引入的全新体验。 

![时间线](media/windows/timeline.png)

### <a name="useractivity-api"></a>UserActivity API

可以通过 [`Windows.ApplicationModel.UserActivities.UserActivity`](/uwp/api/windows.applicationmodel.useractivities.useractivity) API 将活动填充到时间线中。

将通过 `VisualElement` 的 `Content` 属性提供自适应卡片，如下所示：

```csharp
UserActivity userActivity = await channel.GetOrCreateUserActivityAsync(activityId, new HostName("contoso.com"));
userActivity.ActivationUri = new Uri("rss-reader:article?" + article.Link);
userActivity.DisplayText = article.Title; //used for details tile text
userActivity.VisualElements.Content = AdaptiveCardBuilder.CreateAdaptiveCardFromJson(jsonString);
await userActivity.SaveAsync();
```

### <a name="learning-module"></a>学习模块

这里有一个非常棒的 45 分钟的学习模块，其中包含了从头到尾的这些步骤。

[将自适应卡集成到 Windows 10 时间线](/learn/modules/integrate-app-into-windows-10-timeline/)

### <a name="learn-more"></a>了解详细信息

Build 2017 的此次会议详细介绍了用户活动。

<iframe src="https://channel9.msdn.com/Events/Build/2017/B8108/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="other-windows-surfaces"></a>其他 Windows Surface
我们目前还没有任何可以透露的内容，但我们正在努力将自适应卡片引入到更多 Windows 体验中。

## <a name="dive-in"></a>深入了解！

在本教程中，我们只是介绍了一些粗浅的知识。若要了解自适应卡片的更多内容，请过不久再回来查看并浏览下面的链接。

* [浏览示例卡片](https://adaptivecards.io/samples/)获取灵感
* 使用[架构资源管理器](https://adaptivecards.io/explorer)了解可用元素
* 使用[交互式可视化工具](https://adaptivecards.io/visualizer/index.html?hostApp=Skype)构建一张卡片
* 如果你有任何反馈，请[联系我们](https://adaptivecards.io/connect)