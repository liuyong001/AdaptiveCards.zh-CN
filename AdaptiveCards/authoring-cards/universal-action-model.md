---
title: 通用机器人操作模型
author: sowrabh-msft
ms.author: sonrs
ms.date: 02/10/2021
ms.topic: article
ms.openlocfilehash: bf1fcac09ce55ff0dd5833aefe5d101dd4932737
ms.sourcegitcommit: 0ed81e04d8cdcf8f8bf6f854edf53b7eb9f67d2a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532680"
---
# <a name="universal-bot-action-model"></a>通用机器人操作模型

## <a name="context"></a>上下文

自适应卡片是与平台无关的 UI 片段，使用轻量级 JSON 格式创作而成，应用和服务可以共享它。 自适应卡片不仅适应主机的观感，还提供丰富的交互功能。 有关自适应卡片的详细信息，请访问 [adaptivecards.io](http://adaptivecards.io)。 

随着自适应卡片越来越受欢迎，不同的主机开始支持不同的操作模型，这导致了碎片化。 若要解决此问题，Teams、Outlook 和自适应卡片团队致力于创建一个可跨主机兼容的新型通用机器人操作模型。 这项工作导致了以下情况：
- 机器人和 Bot Framework 的通用化，作为对 Teams（机器人）和 Outlook（可操作邮件）实现基于自适应卡片的场景的方式
- `Action.Execute` 作为 `Action.Submit`（当前由机器人使用）和 `Action.Http`（当前由可操作邮件使用）的替换项
- 仅由可操作邮件支持的常用功能可供机器人使用，即：
  - 卡片能够在显示时进行刷新
  - 用于返回更新卡片的 `Action.Execute` 操作能够立即在客户端显示

有关 Outlook 中可操作邮件的详细信息，请参阅[可操作邮件文档](https://docs.microsoft.com/outlook/actionable-messages/send-via-email)

`Action.Execute` 之前 |  有 `Action.Execute`
:-------------------------:|:-------------------------:
![图像描述了 Teams 和 Outlook 中当前的不一致模型](media/universal-action-model/inconsistent-action-model-lifecycle.png) | ![图像描述了在 Teams 和 Outlook 中使用 Action.Execute 启用的一致模型](media/universal-action-model/universal-action-model-lifecycle.jpg)
![图像显示了自适应卡片 JSON 在当前不一致模型下的外观](media/universal-action-model/inconsistent-action-model.png) | ![图像显示了自适应卡片 JSON 如何在基于 Action.Execute 的新模型下保持相同的外观](media/universal-action-model/new-universal-action-model.jpg)

源：[自适应卡片 @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)

本文档的其余部分重点介绍如何在 Teams 和 Outlook 的上下文中记录通用机器人操作模型。 如果你已经在带有机器人的 Teams 中使用自适应卡片，则可使用相同的机器人，只需稍加更改即可支持 `Action.Execute`。 如果你要使用 Outlook 上的可操作邮件，则需要开发一个支持 `Action.Execute` 的机器人。 目前，Outlook 客户端上对通用机器人操作模型的支持正在积极开发中。

## <a name="schema"></a>架构

> ### <a name="important"></a>重要事项
>
> 通用机器人操作模型在自适应卡片架构版本 1.4 中引入。 若要使用这些新功能，必须将自适应卡片的 `version` 属性设置为 1.4 或更高版本，如以下示例中所示。 请注意，这会使你的自适应卡片与不支持通用机器人操作模型的旧客户端（Outlook 或 Teams）不兼容。
>
> 如果你使用 `refresh` 属性和/或 `Action.Execute` 并指定卡片版本低于 1.4，则将发生以下情况：
>
> | 客户端 | 行为 |
> | --- | --- |
> | Outlook | 你的卡片将无法工作。 `refresh` 将不会生效，并且 `Action.Execute` 不会呈现。 你的卡片甚至可能会被完全拒绝。 |
> | Teams | 你的卡片可能无法工作（`refresh` 可能不会生效，并且 `Action.Execute` 操作可能不会呈现），具体取决于 Teams 客户端的版本。<br><br> 若要确保 Teams 中的最大兼容性，请考虑在 `fallback` 属性中使用 `Action.Submit` 操作来定义 `Action.Execute` 操作。 |
>
> 有关详细信息，请参阅下面的“后向兼容性”部分。


### <a name="actionexecute"></a>Action.Execute

创作自适应卡片时，请使用 `Action.Execute` 来代替 `Action.Submit` &  `Action.Http`。 `Action.Execute` 的架构与 `Action.Submit` 的架构非常类似。

**示例 JSON**
```json
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.4",
  "body": [
    {
      "type": "TextBlock",
      "text": "Present a form and submit it back to the originator"
    },
    {
      "type": "Input.Text",
      "id": "firstName",
      "placeholder": "What is your first name?"
    },
    {
      "type": "Input.Text",
      "id": "lastName",
      "placeholder": "What is your last name?"
    },
    {
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Submit",
          "verb": "personalDetailsFormSubmit",
          "fallback": "Action.Submit"
        }
      ]
    }
  ]
}
```

**属性**

| 属性 | 类型 | 必需 | 说明 
| -------- | ---- | -------- | ----------- 
| **type** | `"Action.Execute"` | 是 | 必须是 `"Action.Execute"`。 |
| **谓词** | string | 否 | 可供开发人员用来标识操作的便捷字符串 |
| **data** | `string`, `object` | 否 | 输入字段将与之组合的初始数据。 这些实质上是“隐藏的”属性。 |
| **title** | `string` | 否 | 表示此操作的按钮或链接的标签。 |
| **iconUrl** | `uri` | 否 | 要针对某操作与标题一起显示的可选图标。 在自适应卡片版本 1.2 及以上版本中支持数据 URI |
| style | `ActionStyle` | 否 | 控制操作的样式，这会影响操作的显示方式、朗读方式等。 |
| fallback | `<action object>`, `"drop"` | 否 | 描述当显示卡片的客户端不支持 Action.Execute 时要执行的操作。 |
| requires | `Dictionary<string>` | 否 | 一系列键/值对，用于指示项所需的功能以及相应的最低版本。 当某个功能缺失或版本较低时，将触发回退。 |


### <a name="refresh-mechanism"></a>刷新机制

除了 `Action.Execute` 之外，现在还支持一种新的刷新机制，这使得创建在显示时自动更新的自适应卡片成为可能。 这可确保用户始终能看到最新的数据。 批准请求是一个典型的刷新用例：批准后，最好不要向用户显示一个卡片，提示他们在批准已完成后进行批准，而是提供请求得到批准的时间和批准者的信息。

若要允许自适应卡片自动刷新，请定义其 `refresh` 属性，该属性嵌入 `Action.Execute` 类型的 `action` 和 `userIds` 数组。

| 属性 | 类型 | 必需 | 说明 
| -------- | ---- | -------- | ----------- 
| **action** | `"Action.Execute"` | 是 | 必须是 `"Action.Execute"` 类型的操作实例。 |
| userIds | `Array<string>` | 是 | 必须为其启用自动刷新的用户的 `MRI` 数组。<br><br>重要事项：如果卡片的 `refresh` 部分中未包含 `userIds` 列表属性，则在显示时不会自动刷新此卡片。 而系统会向用户显示一个按钮，允许用户进行手动刷新。 这样做的原因是 Teams 中的通道可以包含大量成员；如果许多成员同时查看该通道，无条件自动刷新将导致对机器人的许多并发调用，而这无法缩放。 若要缓解潜在的缩放问题，应始终包含 `userIds` 属性，以确定哪些用户应进行自动刷新，目前最多允许 5 个用户标识。<br><br>请注意，`userIds` 属性在 Outlook 中被忽略，而 `refresh` 属性始终自动生效。 Outlook 中没有缩放问题，因为用户通常会在不同的时间查看卡片。 |

示例 JSON
```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "originator":"c9b4352b-a76b-43b9-88ff-80edddaa243b",
  "version": "1.4",
  "refresh": {
    "action": {
      "type": "Action.Execute",
      "title": "Submit",
      "verb": "personalDetailsCardRefresh"
    },
    "userIds": []
  },
  "body": [
    {
      "type": "TextBlock",
      "text": "Present a form and submit it back to the originator"
    },
    {
      "type": "Input.Text",
      "id": "firstName",
      "placeholder": "What is your first name?"
    },
    {
      "type": "Input.Text",
      "id": "lastName",
      "placeholder": "What is your last name?"
    },
    { 
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Submit",
          "verb": "personalDetailsFormSubmit",
          "fallback": "Action.Submit"
        }
      ]
    }
  ]
}
```

#### <a name="important-note-for-outlook-actionable-message-developers"></a>面向 Outlook 可操作邮件开发人员的重要说明

开发 Outlook 可操作邮件场景时，必须指定自适应卡片的 `originator` 属性。 `originator` 是机器人订阅 Outlook 通道时生成的全局唯一标识符 (GUID)。 Outlook 使用它来验证自适应卡片是由授权的机器人发送的。 如果 `originator` 不存在，则不会在 Outlook 中呈现自适应卡片。 `originator` 在 Teams 中被忽略。

### <a name="adaptivecardaction-invoke-activity"></a>`adaptiveCard/action` Invoke 活动

在客户端中执行 `Action.Execute` 时（无论它是刷新操作还是用户通过单击某按钮显式执行的操作），系统会对机器人执行一种新型的 Invoke 活动 - `adaptiveCard/action`。 典型的 `adaptiveCard/action` Invoke 活动请求如下所示：

#### <a name="request-format"></a>请求格式

```
{ 
  "type": "invoke",
  "name": "adaptiveCard/action",

  // ... other properties omitted for brevity

  "value": { 
    "action": { 
      "type": "Action.Execute", 
      "id": "abc", 
      "verb": "def",
      "data": { ... } 
    },
    "trigger": "automatic | manual" 
  }
} 
```

| 字段 | 说明 |
| -------- | ----------- |
| value.action | 自适应卡片中定义的操作副本。 与 `Action.Submit` 一样，操作的 `data` 属性包括卡片中各种输入的值（如果有） |
| value.trigger | 指示操作是显式触发（通过用户单击按钮）还是隐式触发（通过自动刷新） |

#### <a name="response-format"></a>响应格式

如果机器人确实处理了一个传入的 `adaptiveCard/action` Invoke 活动（例如，如果机器人的代码在处理请求时牵涉其中），则该机器人返回的 HTTP 响应的状态代码必须等于 200，并且该 HTTP 响应的正文必须如下进行格式设置:

```JSON
{ 
    "statusCode": <number (200 – 599)>, 
    "type": "<string>", 
    "value": "<object>"
} 
```

| 字段 | 说明 |
| -------- | ----------- |
| **statusCode** | HTTP 响应状态代码 200 不一定意味着机器人能够成功地处理请求。 客户端应用程序必须始终在响应的正文中查看 `statucCode` 属性，了解机器人处理请求的情况如何。 `statusCode` 是一个介于 200-599 之间的数字，用于镜像 HTTP 状态代码值，并且是机器人处理 Invoke 的结果的子状态。 `statusCode` 的值缺失、为 null 或未定义表示 200（成功）。 |
| type  | 一组已知的字符串常量，用于描述 value 属性的预期形状  |
| **value** | 一个特定于响应正文类型的对象  |

支持的状态代码

下表列出了机器人的响应正文中 `statusCode`、`type` 和 `value` 的允许值：

| 状态代码 | 类型 | 值架构 | 备注 |
| --- | --- | --- | --- |
| 200 | `application/vnd.microsoft.adaptive.card` | `Adaptive Card` | 请求已成功处理，响应包含一个自适应卡片，客户端应该显示该卡片来代替当前的卡片。 |
| 200 | `application/vnd.microsoft.activity.message` | `string` | 请求已成功处理，响应包含客户端应显示的邮件。 |
| 400 | `application/vnd.microsoft.error` | 错误对象（TODO：需要链接） | 传入的请求无效。 | 
| 401 | `application/vnd.microsoft.activity.loginRequest` | OAuthCard（TODO：需要链接） | 客户端需要提示用户进行身份验证。 |
| 401 | `application/vnd.microsoft.error.inccorectAuthCode` | Null | 客户端传递的身份验证状态不正确，身份验证失败。 |
| 412 | `application/vnd.microsoft.error.preconditionFailed` | 错误对象（TODO：需要链接） | SSO 身份验证流失败。 |
| 500 | `application/vnd.microsoft.error` | 错误对象（TODO：需要链接） | 发生了意外错误。 |

## <a name="summary-how-to-leverage-the-universal-bot-action-model"></a>摘要：如何利用通用机器人操作模型

1. 请使用 `Action.Execute`，而不是 `Action.Submit`。 若要更新 Teams 中的现有场景，请将所有的 `Action.Submit` 实例替换为 `Action.Execute`。 若要升级 Outlook 中的现有场景，请参阅下面的“后向兼容性”部分。
2. 对于要在 Outlook 上显示的卡片，请添加 `originator` 字段。 请参阅上面的示例 JSON。  
3. 如果要利用自动刷新机制或你的场景需要上下文视图，请将 `refresh` 子句添加到自适应卡片。 请确保指定 `userIds` 属性，以确定哪些用户（最多 5 名）将进行自动更新。 
4. 在机器人中处理 `adaptiveCard/action` Invoke 请求
5. 每当机器人在处理 `Action.Execute` 后需要返回新的卡片时，你可使用 Invoke 请求的上下文来生成专门为给定用户制作的卡片。 请确保响应符合上面定义的响应架构。

## <a name="backward-compatibility"></a>向后兼容性

### <a name="outlook"></a>Outlook

新的 `Action.Execute` 通用操作模型不同于 Outlook 可操作邮件目前使用的 `Action.Http` 操作模型，后者将操作在自适应卡片中编码为显式 HTTP 调用。 利用 `Action.Execute` 模型，开发人员可实现在 Outlook 和 Teams 中均可正常工作的场景。 可操作邮件场景既可使用 `Action.Http` 模型，也可使用新的 `Action.Execute` 模型，但不能同时使用两者。 使用通用 `Action.Execute` 模型的场景必须作为机器人实现，并订阅 `Outlook Actionable Messages` 通道。

> #### <a name="important-notes"></a>重要事项
> - 使用通用 `Action.Execute` 模型实现的场景与旧版 Outlook 不兼容
> - 允许现有的可操作邮件场景无缝迁移到通用 `Action.Execute` 模型的工作正在进行中

### <a name="teams"></a>Teams

为了使卡片能够后向兼容并适用于旧版 Teams 的用户，`Action.Execute` 操作应包含定义为 `Action.Submit` 的 `fallback` 属性。 机器人应以能够同时处理 `Action.Execute` 和 `Action.Submit` 的方式进行编码。 请注意，机器人在处理 `Action.Submit` 时不能返回新卡片，因此通过 `Action.Submit` 的回退行为将为最终用户提供降级的体验。

> #### <a name="important-note"></a>重要说明
> 若 fallback 属性未包装在 `ActionSet` 中，某些旧版 Teams 客户端不支持该属性。 为了在此类客户端上不中断，强烈建议将所有 `Action.Execute` 包装在 `ActionSet` 中。 请参阅下面的示例，了解如何在 `ActionSet` 中包装 `Action.Execute`。

在以下示例中，请注意，卡片的 `version` 属性设置为 `1.2`，并使用 `Action.Submit` 作为 `fallback` 来定义 `Action.Execute`。 当在支持自适应卡片 1.4 的 Teams 客户端中呈现时，`Action.Execute` 将按预期方式呈现并工作。 在不支持自适应卡片 1.4 的 Teams 客户端中，将呈现 `Action.Submit` 来代替 `Action.Execute`。

```JSON
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "type": "AdaptiveCard",
  "version": "1.2",
  "body": [
    {
      "type": "TextBlock",
      "text": "Present a form and submit it back to the originator"
    },
    {
      "type": "Input.Text",
      "id": "firstName",
      "placeholder": "What is your first name?"
    },
    {
      "type": "Input.Text",
      "id": "lastName",
      "placeholder": "What is your last name?"
    },
    {
      "type": "ActionSet",
      "actions": [
        {
          "type": "Action.Execute",
          "title": "Submit",
          "verb": "personalDetailsFormSubmit",
          "fallback": {
            "type": "Action.Submit",
            "title": "Submit"
          }  
        }
      ]
    }
  ]
}
```

## <a name="references"></a>参考
- [自适应卡片 @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
- [自适应卡片 @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)


































