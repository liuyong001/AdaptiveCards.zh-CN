---
title: 自适应卡片路线图
author: matthidinger
ms.author: mahiding
ms.date: 05/16/2018
ms.topic: article
ms.openlocfilehash: b11edbedca83bb26d2990d029a220165f68bc1ca
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454890"
---
# <a name="future-work"></a>未来工作

虽然我们已在定义自适应卡片方面有了很大的进展，但仍有大量工作要做。 我们希望，通过 Botness 之类的开发人员社区的积极参与，以及 Slack 和 Kik 之类的合作伙伴的通力协作，我们可以打造一个跨平台卡片的良好生态系统。

## <a name="roadmap"></a>路线图

你可以在[这里查看我们当前（并非最终）的路线图](https://portal.productboard.com/adaptivecards/1-adaptive-cards-portal/tabs/1-backlog)。 请注意，此处的任何内容都可能会更改，不保证寄送。

## <a name="future-ideas"></a>未来创意

下面是我们的一些未来创意，仍处于集体讨论阶段。 如果你对其中的任何内容感兴趣，请在评论中给我们留言。

### <a name="great-looking-cards-from-data"></a>外观良好的卡片离不开数据

我们知道，许多卡片作者已经有可以在卡片上使用的定义好的数据。 我们的计划是探索出一个模板化的模型，这样，用户就可以使用数据以及定义好的可自定义模板的库来生成卡片（不管是在服务器端还是在客户端）。

### <a name="make-cards-responsive"></a>让卡片响应快

卡片布局应该可以根据可用空间大小进行调整。 自适应卡片可以适应不同的设备、UX 样式和 UI 框架，但它们还无法主动进行调整。 必须在元素上定义其他属性，让卡片生产者可以为呈现库提供必需的提示，这样库就能够以智能方式更改布局，使卡片的用途不变。

### <a name="responsive-exploration"></a>响应式浏览

* 添加 **importance** 属性，标注内容的重要性。 可以根据空间大小删除不太重要的内容
* 添加 **constraints** 和 **policy** 属性，说明在无法满足约束条件的情况下无法进行应对。 
  * 隐藏内容，或者将内容折叠以降低其大小
  * 添加一个阈值，超过该阈值时更改 `columnSet`，将列循环展示

### <a name="new-element-types"></a>新元素类型

* 地图？ - 将地图嵌入具有交互功能的卡片中，或者回退到位图
* 你想要或需要什么元素？ 

### <a name="new-rendering-libraries"></a>新的呈现库

* React？
* Xamarin？
* 你想要什么框架？ 
