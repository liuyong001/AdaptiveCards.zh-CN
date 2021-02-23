---
title: 操作
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 7aeaa0b10e33d5e603a12d95e0b99f595f54e6aa
ms.sourcegitcommit: 0ed81e04d8cdcf8f8bf6f854edf53b7eb9f67d2a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532568"
---
# <a name="actions"></a>操作

默认情况下，操作在卡上会呈现为按钮，但应用可以根据你的需要来定义操作的行为。 每个 SDK 都有 `OnAction` 事件的等效项，必须对其进行处理。

* **Action.OpenUrl** - 打开指定的 `url`。  
* **Action.Submit** - 获取提交的结果并将其发送到源。 如何将其发送到卡片的源完全取决于你自己。
* **Action.ShowCard** - 调用某个对话并将子卡呈现到该对话中。 请注意，只有在 `ShowCardActionMode` 设置为 `popup` 的情况下，才需要对此进行处理。
* Action.ToggleVisibility - 显示或隐藏卡片中的一个或多个元素。