---
title: 处理操作-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 5a3d72a00560ad92c490517456ea3f1917ae6cf2
ms.sourcegitcommit: 0ed81e04d8cdcf8f8bf6f854edf53b7eb9f67d2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532508"
---
# <a name="handling-actions---javascript"></a>处理操作-JavaScript

JavaScript SDK 引入了一个基本 `Action` 和一组专用操作类 (它们都扩展了 `Action` 映射到自适应卡架构中定义的各种操作类型的) ：
| 架构类型名称 | JavaScript 类 |
| --- | --- |
| [Action.OpenUrl](https://adaptivecards.io/explorer/Action.OpenUrl.html) | `OpenUrlAction` |
| [Action.ShowCard](https://adaptivecards.io/explorer/Action.ShowCard.html) | `ShowCardAction` |
| [操作。 ToggleVisibility](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) | `ToggleVisibilityAction` |
| [Action.Submit](https://adaptivecards.io/explorer/Action.Submit.html) | `SubmitAction` |

## <a name="handling-actions-when-users-click-action-buttons"></a>用户单击操作按钮时处理操作
若要使用 JavaScript SDK 处理操作执行，应用程序应为全局 `AdaptiveCard.onExecuteAction` 事件或每个卡事件提供处理程序 `adaptiveCardInstance.onExecuteAction` 。 无论所执行操作的类型是什么，都将调用事件处理程序，并负责测试正在执行的操作类型并运行相应的代码。 通常，应用程序只需显式处理 `SubmitAction` ，因为其他操作类型会由 SDK 自动处理。

### <a name="example"></a>示例

```typescript
// Create an AdaptiveCard instance
let adaptiveCard = new AdaptiveCard();

// Parse a card payload - this is just a very simple example
adaptiveCard.parse(
    {
        "type": "AdaptiveCard",
        "version": "1.0",
        "actions": [
            {
                "type": "Action.Submit",
                "id": "clickMe",
                "title": "Click me!"
            }
        ]
    }
)

// Provide an onExecuteAction handler to handle the Action.Submit
adaptiveCard.onExecuteAction = (action: Action) => {
    if (action instanceof SubmitAction) {
        // If you copy this code sample, remove the alert statement
        // and provide your own custom handling code
        alert("You clicked " + action.title);
    }
}

document.body.appendChild(adaptiveCard.render());
```

## <a name="executing-actions-in-code"></a>在代码中执行操作

JavaScript SDK 允许您通过方法在必要时执行代码中的操作 `Action.execute()` 。

### <a name="example"></a>示例

```typescript
function triggerAction(card: AdaptiveCard, actionId: string) {
    let action = card.getActionById(actionId);

    if (action !== undefined) {
        // Executing an action in code will trigger the
        // onExecuteAction event
        action.execute();
    }
}
```