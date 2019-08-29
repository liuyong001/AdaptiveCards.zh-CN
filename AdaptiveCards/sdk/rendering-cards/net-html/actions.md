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

顶级卡片`actions`将呈现为 HTML `<button>`。 由于这是一个服务器端库, 因此在按下按钮时, 将由您来连接客户端事件处理程序。 HTML `<button>`中的每个都具有可用于连接正确行为的特性。

某些元素具有`selectAction`属性 (容器、列、图像), 使其可调用。 如果元素具有`selectAction` `ac-selectable`, 则呈现器将添加的 CSS 类以及以下属性。

操作类型 | CSS 类 | 其他属性
---|---|---
`Action.OpenUrl` | `ac-action-openUrl` | `data-ac-url`(卡片`url`中的属性)
`Action.Submit` | `ac-action-submit` | `data-ac-data`(卡片`data`中的属性)
`Action.ShowCard` | `ac-action-showCard` | `data-ac-showcardid``id` (`<div>`包含内部卡的)