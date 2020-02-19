---
title: 操作-.NET HTML SDK
author: matthidinger
ms.author: mahiding
ms.date: 10/19/2017
ms.topic: article
ms.openlocfilehash: f577c0bab73e2bd1f75bb22dd7a41a7dbfd63307
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454570"
---
# <a name="actions---net-html"></a>操作-.NET HTML

顶级卡 `actions` 将呈现为 HTML `<button>`。 由于这是一个服务器端库，因此在按下按钮时，将由您来连接客户端事件处理程序。 HTML 中的每个 `<button>` 都具有可用于连接正确行为的特性。

某些元素具有 `selectAction` 属性（容器、列、图像），使其可调用。 如果元素具有 `selectAction` 呈现器将添加 `ac-selectable`的 CSS 类以及以下属性。

操作类型 | CSS 类 | 其他属性
---|---|---
`Action.OpenUrl` | `ac-action-openUrl` | `data-ac-url` （卡片中的 `url` 属性）
`Action.Submit` | `ac-action-submit` | `data-ac-data` （卡片中的 `data` 属性）
`Action.ShowCard` | `ac-action-showCard` | `data-ac-showcardid` （包含内部卡的 `<div>` 的 `id`）