---
title: 操作
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 42ba1ca4ba2ecd508bdee2f04061293d48349aab
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553369"
---
# <a name="actions"></a>操作

默认情况下，操作将呈现为在卡上的按钮，但这取决于您的应用程序以使其按预期工作。 每个 SDK 有相当于`OnAction`必须处理的事件。

* **Action.OpenUrl** -打开指定`url`。  
* **Action.Submit** -提取的提交结果，并将其发送到源。 如何向的源发送它是卡片的完全取决于您。
* **Action.ShowCard** -调用一个对话框，并将子卡呈现到该对话框。 请注意，只需处理此 if`ShowCardActionMode`设置为`popup`。