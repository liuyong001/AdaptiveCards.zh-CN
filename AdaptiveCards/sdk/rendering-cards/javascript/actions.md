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
# <a name="handling-actions---javascript"></a><span data-ttu-id="f92d9-102">处理操作-JavaScript</span><span class="sxs-lookup"><span data-stu-id="f92d9-102">Handling actions - JavaScript</span></span>

<span data-ttu-id="f92d9-103">JavaScript SDK 引入了一个基本 `Action` 和一组专用操作类 (它们都扩展了 `Action` 映射到自适应卡架构中定义的各种操作类型的) ：</span><span class="sxs-lookup"><span data-stu-id="f92d9-103">The JavaScript SDK introduces a base `Action` and a set of dedicated action classes (that all extend `Action`) that map to the various action types defined in the Adaptive Card schema:</span></span>
| <span data-ttu-id="f92d9-104">架构类型名称</span><span class="sxs-lookup"><span data-stu-id="f92d9-104">Schema type name</span></span> | <span data-ttu-id="f92d9-105">JavaScript 类</span><span class="sxs-lookup"><span data-stu-id="f92d9-105">JavaScript class</span></span> |
| --- | --- |
| [<span data-ttu-id="f92d9-106">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="f92d9-106">Action.OpenUrl</span></span>](https://adaptivecards.io/explorer/Action.OpenUrl.html) | `OpenUrlAction` |
| [<span data-ttu-id="f92d9-107">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="f92d9-107">Action.ShowCard</span></span>](https://adaptivecards.io/explorer/Action.ShowCard.html) | `ShowCardAction` |
| [<span data-ttu-id="f92d9-108">操作。 ToggleVisibility</span><span class="sxs-lookup"><span data-stu-id="f92d9-108">Action.ToggleVisibility</span></span>](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) | `ToggleVisibilityAction` |
| [<span data-ttu-id="f92d9-109">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="f92d9-109">Action.Submit</span></span>](https://adaptivecards.io/explorer/Action.Submit.html) | `SubmitAction` |

## <a name="handling-actions-when-users-click-action-buttons"></a><span data-ttu-id="f92d9-110">用户单击操作按钮时处理操作</span><span class="sxs-lookup"><span data-stu-id="f92d9-110">Handling actions when users click action buttons</span></span>
<span data-ttu-id="f92d9-111">若要使用 JavaScript SDK 处理操作执行，应用程序应为全局 `AdaptiveCard.onExecuteAction` 事件或每个卡事件提供处理程序 `adaptiveCardInstance.onExecuteAction` 。</span><span class="sxs-lookup"><span data-stu-id="f92d9-111">To handle action execution with the JavaScript SDK, an application should provide a handler for either the global `AdaptiveCard.onExecuteAction` event, or for the per-card `adaptiveCardInstance.onExecuteAction` event.</span></span> <span data-ttu-id="f92d9-112">无论所执行操作的类型是什么，都将调用事件处理程序，并负责测试正在执行的操作类型并运行相应的代码。</span><span class="sxs-lookup"><span data-stu-id="f92d9-112">The event handler will be invoked regardless of the type of action being executed, and it is the responsibility of the application to test which type of action is being executed and run the appropriate code.</span></span> <span data-ttu-id="f92d9-113">通常，应用程序只需显式处理 `SubmitAction` ，因为其他操作类型会由 SDK 自动处理。</span><span class="sxs-lookup"><span data-stu-id="f92d9-113">Typically, applications will only need to explicitly handle `SubmitAction`, as other action types are automatically handled by the SDK.</span></span>

### <a name="example"></a><span data-ttu-id="f92d9-114">示例</span><span class="sxs-lookup"><span data-stu-id="f92d9-114">Example</span></span>

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

## <a name="executing-actions-in-code"></a><span data-ttu-id="f92d9-115">在代码中执行操作</span><span class="sxs-lookup"><span data-stu-id="f92d9-115">Executing actions in code</span></span>

<span data-ttu-id="f92d9-116">JavaScript SDK 允许您通过方法在必要时执行代码中的操作 `Action.execute()` 。</span><span class="sxs-lookup"><span data-stu-id="f92d9-116">The JavaScript SDK allows you to execute actions in code if necessary via the `Action.execute()` method.</span></span>

### <a name="example"></a><span data-ttu-id="f92d9-117">示例</span><span class="sxs-lookup"><span data-stu-id="f92d9-117">Example</span></span>

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