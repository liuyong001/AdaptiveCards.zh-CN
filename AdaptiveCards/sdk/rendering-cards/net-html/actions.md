---
title: 操作-.NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: 99bf6121489391c207a71b45264dc68aa2c6116e
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553309"
---
# <a name="actions---net-html"></a>操作-.NET HTML

顶级卡`actions`将呈现为 HTML `<button>`。 由于这是服务器端库，这取决于您按下按钮时绑定客户端事件处理程序。 每个`<button>`HTML 中会具有可以使用的属性进行正确的行为。

某些元素具有`selectAction`使它们可调用的属性 （列，容器映像）。 如果某个元素有`selectAction`呈现器将添加的 CSS 类`ac-selectable`，以及以下属性。

操作类型 | CSS 类 | 其他属性
---|---|---
`Action.OpenUrl` | `ac-action-openUrl` | `data-ac-url` (`url`属性从智能卡)
`Action.Submit` | `ac-action-submit` | `data-ac-data` (`data`属性从智能卡)
`Action.ShowCard` | `ac-action-showCard` | `data-ac-showcardid` (`id`的`<div>`包含内部卡)