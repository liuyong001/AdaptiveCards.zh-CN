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
# <a name="universal-bot-action-model"></a><span data-ttu-id="71fbf-102">通用机器人操作模型</span><span class="sxs-lookup"><span data-stu-id="71fbf-102">Universal Bot action model</span></span>

## <a name="context"></a><span data-ttu-id="71fbf-103">上下文</span><span class="sxs-lookup"><span data-stu-id="71fbf-103">Context</span></span>

<span data-ttu-id="71fbf-104">自适应卡片是与平台无关的 UI 片段，使用轻量级 JSON 格式创作而成，应用和服务可以共享它。</span><span class="sxs-lookup"><span data-stu-id="71fbf-104">Adaptive Cards are platform-agnostic snippets of UI, authored using a lightweight JSON format, that apps and services can share.</span></span> <span data-ttu-id="71fbf-105">自适应卡片不仅适应主机的观感，还提供丰富的交互功能。</span><span class="sxs-lookup"><span data-stu-id="71fbf-105">Adaptive Cards not only adapt to the look-and-feel of the host, but also provide rich interaction capabilities.</span></span> <span data-ttu-id="71fbf-106">有关自适应卡片的详细信息，请访问 [adaptivecards.io](http://adaptivecards.io)。</span><span class="sxs-lookup"><span data-stu-id="71fbf-106">For more information about Adaptive Cards, please visit [adaptivecards.io](http://adaptivecards.io).</span></span> 

<span data-ttu-id="71fbf-107">随着自适应卡片越来越受欢迎，不同的主机开始支持不同的操作模型，这导致了碎片化。</span><span class="sxs-lookup"><span data-stu-id="71fbf-107">As Adaptive Cards grew in popularity, different hosts started supporting different action models and this led to fragmentation.</span></span> <span data-ttu-id="71fbf-108">若要解决此问题，Teams、Outlook 和自适应卡片团队致力于创建一个可跨主机兼容的新型通用机器人操作模型。</span><span class="sxs-lookup"><span data-stu-id="71fbf-108">To solve this problem, the Teams, Outlook and Adaptive Cards teams worked on creating a new universal Bot action model compatible across hosts.</span></span> <span data-ttu-id="71fbf-109">这项工作导致了以下情况：</span><span class="sxs-lookup"><span data-stu-id="71fbf-109">This effort lead to the following:</span></span>
- <span data-ttu-id="71fbf-110">机器人和 Bot Framework 的通用化，作为对 Teams（机器人）和 Outlook（可操作邮件）实现基于自适应卡片的场景的方式</span><span class="sxs-lookup"><span data-stu-id="71fbf-110">The generalization of Bots and the Bot Framework as the way to implement Adaptive Card-based scenarios for both Teams (Bots) and Outlook (Actionable Message)</span></span>
- <span data-ttu-id="71fbf-111">`Action.Execute` 作为 `Action.Submit`（当前由机器人使用）和 `Action.Http`（当前由可操作邮件使用）的替换项</span><span class="sxs-lookup"><span data-stu-id="71fbf-111">`Action.Execute` as a replacement for both `Action.Submit` (currently used by Bots) and `Action.Http` (currently used by Actionable Messages)</span></span>
- <span data-ttu-id="71fbf-112">仅由可操作邮件支持的常用功能可供机器人使用，即：</span><span class="sxs-lookup"><span data-stu-id="71fbf-112">Popular features only supported by Actionable Messages made available to Bots, namely:</span></span>
  - <span data-ttu-id="71fbf-113">卡片能够在显示时进行刷新</span><span class="sxs-lookup"><span data-stu-id="71fbf-113">The ability for a card to be refreshed at the time it is displayed</span></span>
  - <span data-ttu-id="71fbf-114">用于返回更新卡片的 `Action.Execute` 操作能够立即在客户端显示</span><span class="sxs-lookup"><span data-stu-id="71fbf-114">The ability for `Action.Execute` actions to return an updated card to be immediately displayed in the client</span></span>

<span data-ttu-id="71fbf-115">有关 Outlook 中可操作邮件的详细信息，请参阅[可操作邮件文档](https://docs.microsoft.com/outlook/actionable-messages/send-via-email)</span><span class="sxs-lookup"><span data-stu-id="71fbf-115">For more information about Actionable Messages in Outlook, please refer to the [Actionable Message documentation](https://docs.microsoft.com/outlook/actionable-messages/send-via-email)</span></span>

<span data-ttu-id="71fbf-116">`Action.Execute` 之前</span><span class="sxs-lookup"><span data-stu-id="71fbf-116">Before `Action.Execute`</span></span> |  <span data-ttu-id="71fbf-117">有 `Action.Execute`</span><span class="sxs-lookup"><span data-stu-id="71fbf-117">With `Action.Execute`</span></span>
:-------------------------:|:-------------------------:
![图像描述了 Teams 和 Outlook 中当前的不一致模型](media/universal-action-model/inconsistent-action-model-lifecycle.png) | ![图像描述了在 Teams 和 Outlook 中使用 Action.Execute 启用的一致模型](media/universal-action-model/universal-action-model-lifecycle.jpg)
![图像显示了自适应卡片 JSON 在当前不一致模型下的外观](media/universal-action-model/inconsistent-action-model.png) | ![图像显示了自适应卡片 JSON 如何在基于 Action.Execute 的新模型下保持相同的外观](media/universal-action-model/new-universal-action-model.jpg)

<span data-ttu-id="71fbf-122">源：[自适应卡片 @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)</span><span class="sxs-lookup"><span data-stu-id="71fbf-122">Source: [Adaptive Cards @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)</span></span>

<span data-ttu-id="71fbf-123">本文档的其余部分重点介绍如何在 Teams 和 Outlook 的上下文中记录通用机器人操作模型。</span><span class="sxs-lookup"><span data-stu-id="71fbf-123">The rest of this document focuses on documenting the universal Bot action model in the context of Teams & Outlook.</span></span> <span data-ttu-id="71fbf-124">如果你已经在带有机器人的 Teams 中使用自适应卡片，则可使用相同的机器人，只需稍加更改即可支持 `Action.Execute`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-124">If you are already using Adaptive cards on Teams with Bot, you can use the same Bot with a few changes to support `Action.Execute`.</span></span> <span data-ttu-id="71fbf-125">如果你要使用 Outlook 上的可操作邮件，则需要开发一个支持 `Action.Execute` 的机器人。</span><span class="sxs-lookup"><span data-stu-id="71fbf-125">If you are using Actionable Messages on Outlook, you will need to develop a Bot that supports `Action.Execute`.</span></span> <span data-ttu-id="71fbf-126">目前，Outlook 客户端上对通用机器人操作模型的支持正在积极开发中。</span><span class="sxs-lookup"><span data-stu-id="71fbf-126">Currently the support on Outlook clients for Universal Bot action model is under active development.</span></span>

## <a name="schema"></a><span data-ttu-id="71fbf-127">架构</span><span class="sxs-lookup"><span data-stu-id="71fbf-127">Schema</span></span>

> ### <a name="important"></a><span data-ttu-id="71fbf-128">重要事项</span><span class="sxs-lookup"><span data-stu-id="71fbf-128">IMPORTANT</span></span>
>
> <span data-ttu-id="71fbf-129">通用机器人操作模型在自适应卡片架构版本 1.4 中引入。</span><span class="sxs-lookup"><span data-stu-id="71fbf-129">The universal Bot action model is introduced in the **Adaptive Cards schema version 1.4**.</span></span> <span data-ttu-id="71fbf-130">若要使用这些新功能，必须将自适应卡片的 `version` 属性设置为 1.4 或更高版本，如以下示例中所示。</span><span class="sxs-lookup"><span data-stu-id="71fbf-130">In order to use these new capabilities, the `version` property of your Adaptive Card must be set to **1.4** or greater, as shown in the below examples.</span></span> <span data-ttu-id="71fbf-131">请注意，这会使你的自适应卡片与不支持通用机器人操作模型的旧客户端（Outlook 或 Teams）不兼容。</span><span class="sxs-lookup"><span data-stu-id="71fbf-131">Note that this will make your Adaptive Card incompatible with older clients (Outlook or Teams) that do not support the universal Bot action model.</span></span>
>
> <span data-ttu-id="71fbf-132">如果你使用 `refresh` 属性和/或 `Action.Execute` 并指定卡片版本低于 1.4，则将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="71fbf-132">If you use the `refresh` property and/or `Action.Execute` and specify a card version < 1.4, the following will happen:</span></span>
>
> | <span data-ttu-id="71fbf-133">客户端</span><span class="sxs-lookup"><span data-stu-id="71fbf-133">Client</span></span> | <span data-ttu-id="71fbf-134">行为</span><span class="sxs-lookup"><span data-stu-id="71fbf-134">Behavior</span></span> |
> | --- | --- |
> | <span data-ttu-id="71fbf-135">Outlook</span><span class="sxs-lookup"><span data-stu-id="71fbf-135">Outlook</span></span> | <span data-ttu-id="71fbf-136">你的卡片将无法工作。</span><span class="sxs-lookup"><span data-stu-id="71fbf-136">Your card **WILL NOT** work.</span></span> <span data-ttu-id="71fbf-137">`refresh` 将不会生效，并且 `Action.Execute` 不会呈现。</span><span class="sxs-lookup"><span data-stu-id="71fbf-137">`refresh` will not be honored and `Action.Execute` will not render.</span></span> <span data-ttu-id="71fbf-138">你的卡片甚至可能会被完全拒绝。</span><span class="sxs-lookup"><span data-stu-id="71fbf-138">Your card may even be rejected entirely.</span></span> |
> | <span data-ttu-id="71fbf-139">Teams</span><span class="sxs-lookup"><span data-stu-id="71fbf-139">Teams</span></span> | <span data-ttu-id="71fbf-140">你的卡片可能无法工作（`refresh` 可能不会生效，并且 `Action.Execute` 操作可能不会呈现），具体取决于 Teams 客户端的版本。</span><span class="sxs-lookup"><span data-stu-id="71fbf-140">Your card **MAY NOT** work (the `refresh` may not be honored, and the `Action.Execute` actions may not render) depending on the version of the Teams client.</span></span><br><br> <span data-ttu-id="71fbf-141">若要确保 Teams 中的最大兼容性，请考虑在 `fallback` 属性中使用 `Action.Submit` 操作来定义 `Action.Execute` 操作。</span><span class="sxs-lookup"><span data-stu-id="71fbf-141">To ensure maximum compatibility in Teams, consider defining your `Action.Execute` actions with an `Action.Submit` action in the `fallback` property.</span></span> |
>
> <span data-ttu-id="71fbf-142">有关详细信息，请参阅下面的“后向兼容性”部分。</span><span class="sxs-lookup"><span data-stu-id="71fbf-142">Refer to the **Backward compatibility** section below for more information.</span></span>


### <a name="actionexecute"></a><span data-ttu-id="71fbf-143">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="71fbf-143">Action.Execute</span></span>

<span data-ttu-id="71fbf-144">创作自适应卡片时，请使用 `Action.Execute` 来代替 `Action.Submit` &  `Action.Http`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-144">When authoring Adaptive Cards, use `Action.Execute` in place of both `Action.Submit` &  `Action.Http`.</span></span> <span data-ttu-id="71fbf-145">`Action.Execute` 的架构与 `Action.Submit` 的架构非常类似。</span><span class="sxs-lookup"><span data-stu-id="71fbf-145">The schema for `Action.Execute` is quite similar to that of `Action.Submit`.</span></span>

<span data-ttu-id="71fbf-146">**示例 JSON**</span><span class="sxs-lookup"><span data-stu-id="71fbf-146">**Example JSON**</span></span>
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

<span data-ttu-id="71fbf-147">**属性**</span><span class="sxs-lookup"><span data-stu-id="71fbf-147">**Properties**</span></span>

| <span data-ttu-id="71fbf-148">属性</span><span class="sxs-lookup"><span data-stu-id="71fbf-148">Property</span></span> | <span data-ttu-id="71fbf-149">类型</span><span class="sxs-lookup"><span data-stu-id="71fbf-149">Type</span></span> | <span data-ttu-id="71fbf-150">必需</span><span class="sxs-lookup"><span data-stu-id="71fbf-150">Required</span></span> | <span data-ttu-id="71fbf-151">说明</span><span class="sxs-lookup"><span data-stu-id="71fbf-151">Description</span></span> 
| -------- | ---- | -------- | ----------- 
| <span data-ttu-id="71fbf-152">**type**</span><span class="sxs-lookup"><span data-stu-id="71fbf-152">**type**</span></span> | `"Action.Execute"` | <span data-ttu-id="71fbf-153">是</span><span class="sxs-lookup"><span data-stu-id="71fbf-153">Yes</span></span> | <span data-ttu-id="71fbf-154">必须是 `"Action.Execute"`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-154">Must be `"Action.Execute"`.</span></span> |
| <span data-ttu-id="71fbf-155">**谓词**</span><span class="sxs-lookup"><span data-stu-id="71fbf-155">**verb**</span></span> | <span data-ttu-id="71fbf-156">string</span><span class="sxs-lookup"><span data-stu-id="71fbf-156">string</span></span> | <span data-ttu-id="71fbf-157">否</span><span class="sxs-lookup"><span data-stu-id="71fbf-157">No</span></span> | <span data-ttu-id="71fbf-158">可供开发人员用来标识操作的便捷字符串</span><span class="sxs-lookup"><span data-stu-id="71fbf-158">A convenience string that can be used by developer to identify the action</span></span> |
| <span data-ttu-id="71fbf-159">**data**</span><span class="sxs-lookup"><span data-stu-id="71fbf-159">**data**</span></span> | <span data-ttu-id="71fbf-160">`string`, `object`</span><span class="sxs-lookup"><span data-stu-id="71fbf-160">`string`, `object`</span></span> | <span data-ttu-id="71fbf-161">否</span><span class="sxs-lookup"><span data-stu-id="71fbf-161">No</span></span> | <span data-ttu-id="71fbf-162">输入字段将与之组合的初始数据。</span><span class="sxs-lookup"><span data-stu-id="71fbf-162">Initial data that input fields will be combined with.</span></span> <span data-ttu-id="71fbf-163">这些实质上是“隐藏的”属性。</span><span class="sxs-lookup"><span data-stu-id="71fbf-163">These are essentially ‘hidden’ properties.</span></span> |
| <span data-ttu-id="71fbf-164">**title**</span><span class="sxs-lookup"><span data-stu-id="71fbf-164">**title**</span></span> | `string` | <span data-ttu-id="71fbf-165">否</span><span class="sxs-lookup"><span data-stu-id="71fbf-165">No</span></span> | <span data-ttu-id="71fbf-166">表示此操作的按钮或链接的标签。</span><span class="sxs-lookup"><span data-stu-id="71fbf-166">Label for button or link that represents this action.</span></span> |
| <span data-ttu-id="71fbf-167">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="71fbf-167">**iconUrl**</span></span> | `uri` | <span data-ttu-id="71fbf-168">否</span><span class="sxs-lookup"><span data-stu-id="71fbf-168">No</span></span> | <span data-ttu-id="71fbf-169">要针对某操作与标题一起显示的可选图标。</span><span class="sxs-lookup"><span data-stu-id="71fbf-169">Optional icon to be shown on the action in conjunction with the title.</span></span> <span data-ttu-id="71fbf-170">在自适应卡片版本 1.2 及以上版本中支持数据 URI</span><span class="sxs-lookup"><span data-stu-id="71fbf-170">Supports data URI in Adaptive Cards version 1.2+</span></span> |
| <span data-ttu-id="71fbf-171">style</span><span class="sxs-lookup"><span data-stu-id="71fbf-171">**style**</span></span> | `ActionStyle` | <span data-ttu-id="71fbf-172">否</span><span class="sxs-lookup"><span data-stu-id="71fbf-172">No</span></span> | <span data-ttu-id="71fbf-173">控制操作的样式，这会影响操作的显示方式、朗读方式等。</span><span class="sxs-lookup"><span data-stu-id="71fbf-173">Controls the style of an Action, which influences how the action is displayed, spoken, etc.</span></span> |
| <span data-ttu-id="71fbf-174">fallback</span><span class="sxs-lookup"><span data-stu-id="71fbf-174">**fallback**</span></span> | <span data-ttu-id="71fbf-175">`<action object>`, `"drop"`</span><span class="sxs-lookup"><span data-stu-id="71fbf-175">`<action object>`, `"drop"`</span></span> | <span data-ttu-id="71fbf-176">否</span><span class="sxs-lookup"><span data-stu-id="71fbf-176">No</span></span> | <span data-ttu-id="71fbf-177">描述当显示卡片的客户端不支持 Action.Execute 时要执行的操作。</span><span class="sxs-lookup"><span data-stu-id="71fbf-177">Describes what to do when Action.Execute is unsupported by the client displaying the card.</span></span> |
| <span data-ttu-id="71fbf-178">requires</span><span class="sxs-lookup"><span data-stu-id="71fbf-178">**requires**</span></span> | `Dictionary<string>` | <span data-ttu-id="71fbf-179">否</span><span class="sxs-lookup"><span data-stu-id="71fbf-179">No</span></span> | <span data-ttu-id="71fbf-180">一系列键/值对，用于指示项所需的功能以及相应的最低版本。</span><span class="sxs-lookup"><span data-stu-id="71fbf-180">A series of key/value pairs indicating features that the item requires with corresponding minimum version.</span></span> <span data-ttu-id="71fbf-181">当某个功能缺失或版本较低时，将触发回退。</span><span class="sxs-lookup"><span data-stu-id="71fbf-181">When a feature is missing or of insufficient version, fallback is triggered.</span></span> |


### <a name="refresh-mechanism"></a><span data-ttu-id="71fbf-182">刷新机制</span><span class="sxs-lookup"><span data-stu-id="71fbf-182">Refresh mechanism</span></span>

<span data-ttu-id="71fbf-183">除了 `Action.Execute` 之外，现在还支持一种新的刷新机制，这使得创建在显示时自动更新的自适应卡片成为可能。</span><span class="sxs-lookup"><span data-stu-id="71fbf-183">Alongside `Action.Execute`, a new refresh mechanism is now supported, making it possible to create Adaptive Cards that automatically update at the time they are displayed.</span></span> <span data-ttu-id="71fbf-184">这可确保用户始终能看到最新的数据。</span><span class="sxs-lookup"><span data-stu-id="71fbf-184">This ensures that users always see up to date data.</span></span> <span data-ttu-id="71fbf-185">批准请求是一个典型的刷新用例：批准后，最好不要向用户显示一个卡片，提示他们在批准已完成后进行批准，而是提供请求得到批准的时间和批准者的信息。</span><span class="sxs-lookup"><span data-stu-id="71fbf-185">A typical refresh use case is an approval request: once approved, it is best that users are not presented with a card prompting them to approve when it's already been done, but instead provides information on the time the request was approved and by whom.</span></span>

<span data-ttu-id="71fbf-186">若要允许自适应卡片自动刷新，请定义其 `refresh` 属性，该属性嵌入 `Action.Execute` 类型的 `action` 和 `userIds` 数组。</span><span class="sxs-lookup"><span data-stu-id="71fbf-186">To allow an Adaptiver Card to automatically refresh, define its `refresh` property, which embeds an `action` of type `Action.Execute` as well as a `userIds` array.</span></span>

| <span data-ttu-id="71fbf-187">属性</span><span class="sxs-lookup"><span data-stu-id="71fbf-187">Property</span></span> | <span data-ttu-id="71fbf-188">类型</span><span class="sxs-lookup"><span data-stu-id="71fbf-188">Type</span></span> | <span data-ttu-id="71fbf-189">必需</span><span class="sxs-lookup"><span data-stu-id="71fbf-189">Required</span></span> | <span data-ttu-id="71fbf-190">说明</span><span class="sxs-lookup"><span data-stu-id="71fbf-190">Description</span></span> 
| -------- | ---- | -------- | ----------- 
| <span data-ttu-id="71fbf-191">**action**</span><span class="sxs-lookup"><span data-stu-id="71fbf-191">**action**</span></span> | `"Action.Execute"` | <span data-ttu-id="71fbf-192">是</span><span class="sxs-lookup"><span data-stu-id="71fbf-192">Yes</span></span> | <span data-ttu-id="71fbf-193">必须是 `"Action.Execute"` 类型的操作实例。</span><span class="sxs-lookup"><span data-stu-id="71fbf-193">Must be an action instance of type `"Action.Execute"`.</span></span> |
| <span data-ttu-id="71fbf-194">userIds</span><span class="sxs-lookup"><span data-stu-id="71fbf-194">**userIds**</span></span> | `Array<string>` | <span data-ttu-id="71fbf-195">是</span><span class="sxs-lookup"><span data-stu-id="71fbf-195">Yes</span></span> | <span data-ttu-id="71fbf-196">必须为其启用自动刷新的用户的 `MRI` 数组。</span><span class="sxs-lookup"><span data-stu-id="71fbf-196">An array of `MRI`s of users for whom Auto Refresh must be enabled.</span></span><br><br><span data-ttu-id="71fbf-197">重要事项：如果卡片的 `refresh` 部分中未包含 `userIds` 列表属性，则在显示时不会自动刷新此卡片。</span><span class="sxs-lookup"><span data-stu-id="71fbf-197">**IMPORTANT:** If the `userIds` list property isn't included in the `refresh` section of the card, the card will NOT be automatically refresh on display.</span></span> <span data-ttu-id="71fbf-198">而系统会向用户显示一个按钮，允许用户进行手动刷新。</span><span class="sxs-lookup"><span data-stu-id="71fbf-198">Instead, a button will be presented to the user to allow them to manually refresh.</span></span> <span data-ttu-id="71fbf-199">这样做的原因是 Teams 中的通道可以包含大量成员；如果许多成员同时查看该通道，无条件自动刷新将导致对机器人的许多并发调用，而这无法缩放。</span><span class="sxs-lookup"><span data-stu-id="71fbf-199">The reason for this is Channels in Teams can include a large number of members; if many members are all viewing the channel at the same time, and unconditional automatic refresh would results in many concurrent calls to the Bot, which would not scale.</span></span> <span data-ttu-id="71fbf-200">若要缓解潜在的缩放问题，应始终包含 `userIds` 属性，以确定哪些用户应进行自动刷新，目前最多允许 5 个用户标识。</span><span class="sxs-lookup"><span data-stu-id="71fbf-200">To alleviate the potential scale problem, the `userIds` property should always be included to identify which users should get an automatic refresh, with a maximum of **5** user IDs currently being allowed.</span></span><br><br><span data-ttu-id="71fbf-201">请注意，`userIds` 属性在 Outlook 中被忽略，而 `refresh` 属性始终自动生效。</span><span class="sxs-lookup"><span data-stu-id="71fbf-201">Note that the `userIds` property is ignored in Outlook, and the `refresh` property is always automatically honored.</span></span> <span data-ttu-id="71fbf-202">Outlook 中没有缩放问题，因为用户通常会在不同的时间查看卡片。</span><span class="sxs-lookup"><span data-stu-id="71fbf-202">There is no scale issue in Outlook because users will typically view the card at different times.</span></span> |

<span data-ttu-id="71fbf-203">示例 JSON</span><span class="sxs-lookup"><span data-stu-id="71fbf-203">**Sample JSON**</span></span>
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

#### <a name="important-note-for-outlook-actionable-message-developers"></a><span data-ttu-id="71fbf-204">面向 Outlook 可操作邮件开发人员的重要说明</span><span class="sxs-lookup"><span data-stu-id="71fbf-204">Important note for Outlook Actionable Message developers</span></span>

<span data-ttu-id="71fbf-205">开发 Outlook 可操作邮件场景时，必须指定自适应卡片的 `originator` 属性。</span><span class="sxs-lookup"><span data-stu-id="71fbf-205">When developing Outlook Actionable Message scenarios, the Adaptive Card's `originator` property must be specified.</span></span> <span data-ttu-id="71fbf-206">`originator` 是机器人订阅 Outlook 通道时生成的全局唯一标识符 (GUID)。</span><span class="sxs-lookup"><span data-stu-id="71fbf-206">`originator` is a Globally Unique Identified (GUID) generated at the time a Bot subscribes to the Outlook channel.</span></span> <span data-ttu-id="71fbf-207">Outlook 使用它来验证自适应卡片是由授权的机器人发送的。</span><span class="sxs-lookup"><span data-stu-id="71fbf-207">It is used by Outlook to validate that the Adaptive Card was sent by an authorized Bot.</span></span> <span data-ttu-id="71fbf-208">如果 `originator` 不存在，则不会在 Outlook 中呈现自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="71fbf-208">The Adaptive Card will not be rendered in Outlook if `originator` is absent.</span></span> <span data-ttu-id="71fbf-209">`originator` 在 Teams 中被忽略。</span><span class="sxs-lookup"><span data-stu-id="71fbf-209">`originator` is ignored in Teams.</span></span>

### <a name="adaptivecardaction-invoke-activity"></a><span data-ttu-id="71fbf-210">`adaptiveCard/action` Invoke 活动</span><span class="sxs-lookup"><span data-stu-id="71fbf-210">`adaptiveCard/action` Invoke activity</span></span>

<span data-ttu-id="71fbf-211">在客户端中执行 `Action.Execute` 时（无论它是刷新操作还是用户通过单击某按钮显式执行的操作），系统会对机器人执行一种新型的 Invoke 活动 - `adaptiveCard/action`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-211">When an `Action.Execute` is executed in the client (whether it's the refresh action or an action explicitly taken by a user by clicking a button), a new type of Invoke activity - `adaptiveCard/action` - is made to your Bot.</span></span> <span data-ttu-id="71fbf-212">典型的 `adaptiveCard/action` Invoke 活动请求如下所示：</span><span class="sxs-lookup"><span data-stu-id="71fbf-212">A typical `adaptiveCard/action` Invoke activity request will look like the following:</span></span>

#### <a name="request-format"></a><span data-ttu-id="71fbf-213">请求格式</span><span class="sxs-lookup"><span data-stu-id="71fbf-213">Request format</span></span>

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

| <span data-ttu-id="71fbf-214">字段</span><span class="sxs-lookup"><span data-stu-id="71fbf-214">Field</span></span> | <span data-ttu-id="71fbf-215">说明</span><span class="sxs-lookup"><span data-stu-id="71fbf-215">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="71fbf-216">value.action</span><span class="sxs-lookup"><span data-stu-id="71fbf-216">**value.action**</span></span> | <span data-ttu-id="71fbf-217">自适应卡片中定义的操作副本。</span><span class="sxs-lookup"><span data-stu-id="71fbf-217">A copy of the action as defined in the Adaptive Card.</span></span> <span data-ttu-id="71fbf-218">与 `Action.Submit` 一样，操作的 `data` 属性包括卡片中各种输入的值（如果有）</span><span class="sxs-lookup"><span data-stu-id="71fbf-218">Like with `Action.Submit`, the `data` property of the action includes the values of the various inputs in the card, if there are any</span></span> |
| <span data-ttu-id="71fbf-219">value.trigger</span><span class="sxs-lookup"><span data-stu-id="71fbf-219">**value.trigger**</span></span> | <span data-ttu-id="71fbf-220">指示操作是显式触发（通过用户单击按钮）还是隐式触发（通过自动刷新）</span><span class="sxs-lookup"><span data-stu-id="71fbf-220">Indicates if the action was triggered explicitly (by the user clicking a button) or implicitly (via automatic refresh)</span></span> |

#### <a name="response-format"></a><span data-ttu-id="71fbf-221">响应格式</span><span class="sxs-lookup"><span data-stu-id="71fbf-221">Response format</span></span>

<span data-ttu-id="71fbf-222">如果机器人确实处理了一个传入的 `adaptiveCard/action` Invoke 活动（例如，如果机器人的代码在处理请求时牵涉其中），则该机器人返回的 HTTP 响应的状态代码必须等于 200，并且该 HTTP 响应的正文必须如下进行格式设置:</span><span class="sxs-lookup"><span data-stu-id="71fbf-222">If the Bot did process an incoming `adaptiveCard/action` Invoke activity (i.e. if the Bot's code was involved at all in processing the request), the HTTP response's status code returned by the Bot must be equal to 200 and the body of the HTTP response must be formatted as follows:</span></span>

```JSON
{ 
    "statusCode": <number (200 – 599)>, 
    "type": "<string>", 
    "value": "<object>"
} 
```

| <span data-ttu-id="71fbf-223">字段</span><span class="sxs-lookup"><span data-stu-id="71fbf-223">Field</span></span> | <span data-ttu-id="71fbf-224">说明</span><span class="sxs-lookup"><span data-stu-id="71fbf-224">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="71fbf-225">**statusCode**</span><span class="sxs-lookup"><span data-stu-id="71fbf-225">**statusCode**</span></span> | <span data-ttu-id="71fbf-226">HTTP 响应状态代码 200 不一定意味着机器人能够成功地处理请求。</span><span class="sxs-lookup"><span data-stu-id="71fbf-226">An HTTP response status code of 200 does NOT necessarily mean the Bot was able to _successfully_ process the request.</span></span> <span data-ttu-id="71fbf-227">客户端应用程序必须始终在响应的正文中查看 `statucCode` 属性，了解机器人处理请求的情况如何。</span><span class="sxs-lookup"><span data-stu-id="71fbf-227">A client application MUST always look at the `statucCode` property in the response's body to know how the Bot processed the request.</span></span> <span data-ttu-id="71fbf-228">`statusCode` 是一个介于 200-599 之间的数字，用于镜像 HTTP 状态代码值，并且是机器人处理 Invoke 的结果的子状态。</span><span class="sxs-lookup"><span data-stu-id="71fbf-228">`statusCode` is a number ranging from 200-599 that mirrors HTTP status code values and is meant to be a sub-status for the result of the bot processing the Invoke.</span></span> <span data-ttu-id="71fbf-229">`statusCode` 的值缺失、为 null 或未定义表示 200（成功）。</span><span class="sxs-lookup"><span data-stu-id="71fbf-229">A missing, null, or undefined value for `statusCode` implies a 200 (Success).</span></span> |
| <span data-ttu-id="71fbf-230">type </span><span class="sxs-lookup"><span data-stu-id="71fbf-230">**type**</span></span> | <span data-ttu-id="71fbf-231">一组已知的字符串常量，用于描述 value 属性的预期形状</span><span class="sxs-lookup"><span data-stu-id="71fbf-231">A set of well-known string constants that describe the expected shape of the value property</span></span>  |
| <span data-ttu-id="71fbf-232">**value**</span><span class="sxs-lookup"><span data-stu-id="71fbf-232">**value**</span></span> | <span data-ttu-id="71fbf-233">一个特定于响应正文类型的对象</span><span class="sxs-lookup"><span data-stu-id="71fbf-233">An object that is specific to the type of response body</span></span>  |

<span data-ttu-id="71fbf-234">支持的状态代码</span><span class="sxs-lookup"><span data-stu-id="71fbf-234">**Supported status codes**</span></span>

<span data-ttu-id="71fbf-235">下表列出了机器人的响应正文中 `statusCode`、`type` 和 `value` 的允许值：</span><span class="sxs-lookup"><span data-stu-id="71fbf-235">The following table lists the allowed values for `statusCode`, `type`, and `value` in the Bot's response body:</span></span>

| <span data-ttu-id="71fbf-236">状态代码</span><span class="sxs-lookup"><span data-stu-id="71fbf-236">Status Code</span></span> | <span data-ttu-id="71fbf-237">类型</span><span class="sxs-lookup"><span data-stu-id="71fbf-237">Type</span></span> | <span data-ttu-id="71fbf-238">值架构</span><span class="sxs-lookup"><span data-stu-id="71fbf-238">Value Schema</span></span> | <span data-ttu-id="71fbf-239">备注</span><span class="sxs-lookup"><span data-stu-id="71fbf-239">Notes</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="71fbf-240">200</span><span class="sxs-lookup"><span data-stu-id="71fbf-240">200</span></span> | `application/vnd.microsoft.adaptive.card` | `Adaptive Card` | <span data-ttu-id="71fbf-241">请求已成功处理，响应包含一个自适应卡片，客户端应该显示该卡片来代替当前的卡片。</span><span class="sxs-lookup"><span data-stu-id="71fbf-241">The request was successfully processed, and the response includes an Adaptive Card that the client should display in place of the current one.</span></span> |
| <span data-ttu-id="71fbf-242">200</span><span class="sxs-lookup"><span data-stu-id="71fbf-242">200</span></span> | `application/vnd.microsoft.activity.message` | `string` | <span data-ttu-id="71fbf-243">请求已成功处理，响应包含客户端应显示的邮件。</span><span class="sxs-lookup"><span data-stu-id="71fbf-243">The request was successfully processed, and the response includes a message that the client should display.</span></span> |
| <span data-ttu-id="71fbf-244">400</span><span class="sxs-lookup"><span data-stu-id="71fbf-244">400</span></span> | `application/vnd.microsoft.error` | <span data-ttu-id="71fbf-245">错误对象（TODO：需要链接）</span><span class="sxs-lookup"><span data-stu-id="71fbf-245">Error Object (TODO: needs link)</span></span> | <span data-ttu-id="71fbf-246">传入的请求无效。</span><span class="sxs-lookup"><span data-stu-id="71fbf-246">The incoming request was invalid.</span></span> | 
| <span data-ttu-id="71fbf-247">401</span><span class="sxs-lookup"><span data-stu-id="71fbf-247">401</span></span> | `application/vnd.microsoft.activity.loginRequest` | <span data-ttu-id="71fbf-248">OAuthCard（TODO：需要链接）</span><span class="sxs-lookup"><span data-stu-id="71fbf-248">OAuthCard (TODO: needs link)</span></span> | <span data-ttu-id="71fbf-249">客户端需要提示用户进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="71fbf-249">The client needs to prompt the user to authenticate.</span></span> |
| <span data-ttu-id="71fbf-250">401</span><span class="sxs-lookup"><span data-stu-id="71fbf-250">401</span></span> | `application/vnd.microsoft.error.inccorectAuthCode` | <span data-ttu-id="71fbf-251">Null</span><span class="sxs-lookup"><span data-stu-id="71fbf-251">null</span></span> | <span data-ttu-id="71fbf-252">客户端传递的身份验证状态不正确，身份验证失败。</span><span class="sxs-lookup"><span data-stu-id="71fbf-252">The authentication state passed by the client was incorrect and authentication failed.</span></span> |
| <span data-ttu-id="71fbf-253">412</span><span class="sxs-lookup"><span data-stu-id="71fbf-253">412</span></span> | `application/vnd.microsoft.error.preconditionFailed` | <span data-ttu-id="71fbf-254">错误对象（TODO：需要链接）</span><span class="sxs-lookup"><span data-stu-id="71fbf-254">Error Object (TODO: needs link)</span></span> | <span data-ttu-id="71fbf-255">SSO 身份验证流失败。</span><span class="sxs-lookup"><span data-stu-id="71fbf-255">The SSO authentication flow failed.</span></span> |
| <span data-ttu-id="71fbf-256">500</span><span class="sxs-lookup"><span data-stu-id="71fbf-256">500</span></span> | `application/vnd.microsoft.error` | <span data-ttu-id="71fbf-257">错误对象（TODO：需要链接）</span><span class="sxs-lookup"><span data-stu-id="71fbf-257">Error Object (TODO: needs link)</span></span> | <span data-ttu-id="71fbf-258">发生了意外错误。</span><span class="sxs-lookup"><span data-stu-id="71fbf-258">An unexpected error occurred.</span></span> |

## <a name="summary-how-to-leverage-the-universal-bot-action-model"></a><span data-ttu-id="71fbf-259">摘要：如何利用通用机器人操作模型</span><span class="sxs-lookup"><span data-stu-id="71fbf-259">Summary: how to leverage the universal Bot action model</span></span>

1. <span data-ttu-id="71fbf-260">请使用 `Action.Execute`，而不是 `Action.Submit`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-260">Use `Action.Execute` instead of `Action.Submit`.</span></span> <span data-ttu-id="71fbf-261">若要更新 Teams 中的现有场景，请将所有的 `Action.Submit` 实例替换为 `Action.Execute`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-261">To update an existing scenario on teams, replace all instances of `Action.Submit` with `Action.Execute`.</span></span> <span data-ttu-id="71fbf-262">若要升级 Outlook 中的现有场景，请参阅下面的“后向兼容性”部分。</span><span class="sxs-lookup"><span data-stu-id="71fbf-262">For upgrading an existing scenario on Outlook please refer the backward compatibility section below.</span></span>
2. <span data-ttu-id="71fbf-263">对于要在 Outlook 上显示的卡片，请添加 `originator` 字段。</span><span class="sxs-lookup"><span data-stu-id="71fbf-263">For cards to surface on outlook add the `originator` field.</span></span> <span data-ttu-id="71fbf-264">请参阅上面的示例 JSON。</span><span class="sxs-lookup"><span data-stu-id="71fbf-264">Refer the Sample JSON above.</span></span>  
3. <span data-ttu-id="71fbf-265">如果要利用自动刷新机制或你的场景需要上下文视图，请将 `refresh` 子句添加到自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="71fbf-265">Add a `refresh` clause to your Adaptive Card if you want to leverage the automatic refresh mechanism or if your scenario requires contextual views.</span></span> <span data-ttu-id="71fbf-266">请确保指定 `userIds` 属性，以确定哪些用户（最多 5 名）将进行自动更新。</span><span class="sxs-lookup"><span data-stu-id="71fbf-266">Be sure to specify the `userIds` property to identify which users (maximum 5) will get automatic updates.</span></span> 
4. <span data-ttu-id="71fbf-267">在机器人中处理 `adaptiveCard/action` Invoke 请求</span><span class="sxs-lookup"><span data-stu-id="71fbf-267">Handle `adaptiveCard/action` Invoke requests in your Bot</span></span>
5. <span data-ttu-id="71fbf-268">每当机器人在处理 `Action.Execute` 后需要返回新的卡片时，你可使用 Invoke 请求的上下文来生成专门为给定用户制作的卡片。</span><span class="sxs-lookup"><span data-stu-id="71fbf-268">Whenever your Bot needs to return a new card as a result of processing an `Action.Execute`, you can use the Invoke request's context to generate cards that are specifically crafted for a given user.</span></span> <span data-ttu-id="71fbf-269">请确保响应符合上面定义的响应架构。</span><span class="sxs-lookup"><span data-stu-id="71fbf-269">Make sure the response conforms to the response schema defined above.</span></span>

## <a name="backward-compatibility"></a><span data-ttu-id="71fbf-270">向后兼容性</span><span class="sxs-lookup"><span data-stu-id="71fbf-270">Backward compatibility</span></span>

### <a name="outlook"></a><span data-ttu-id="71fbf-271">Outlook</span><span class="sxs-lookup"><span data-stu-id="71fbf-271">Outlook</span></span>

<span data-ttu-id="71fbf-272">新的 `Action.Execute` 通用操作模型不同于 Outlook 可操作邮件目前使用的 `Action.Http` 操作模型，后者将操作在自适应卡片中编码为显式 HTTP 调用。</span><span class="sxs-lookup"><span data-stu-id="71fbf-272">The new `Action.Execute` universal action model is a departure from the `Action.Http` action model currently used by Outlook Actionable Messages, where actions are encoded in the Adaptive Card as explicit HTTP calls.</span></span> <span data-ttu-id="71fbf-273">利用 `Action.Execute` 模型，开发人员可实现在 Outlook 和 Teams 中均可正常工作的场景。</span><span class="sxs-lookup"><span data-stu-id="71fbf-273">The `Action.Execute` model makes it possible for developers to implement scenarios that "just work" in both Outlook and Teams.</span></span> <span data-ttu-id="71fbf-274">可操作邮件场景既可使用 `Action.Http` 模型，也可使用新的 `Action.Execute` 模型，但不能同时使用两者。</span><span class="sxs-lookup"><span data-stu-id="71fbf-274">Actionable Message scenarios can either use the `Action.Http` model or the new `Action.Execute` model, but not both.</span></span> <span data-ttu-id="71fbf-275">使用通用 `Action.Execute` 模型的场景必须作为机器人实现，并订阅 `Outlook Actionable Messages` 通道。</span><span class="sxs-lookup"><span data-stu-id="71fbf-275">Scenarios that use the universal `Action.Execute` model must be implemented as Bots and subscribe to `Outlook Actionable Messages` channel.</span></span>

> #### <a name="important-notes"></a><span data-ttu-id="71fbf-276">重要事项</span><span class="sxs-lookup"><span data-stu-id="71fbf-276">Important notes</span></span>
> - <span data-ttu-id="71fbf-277">使用通用 `Action.Execute` 模型实现的场景与旧版 Outlook 不兼容</span><span class="sxs-lookup"><span data-stu-id="71fbf-277">Scenarios implemented using the universal `Action.Execute` model will not be compatible with older versions of Outlook</span></span>
> - <span data-ttu-id="71fbf-278">允许现有的可操作邮件场景无缝迁移到通用 `Action.Execute` 模型的工作正在进行中</span><span class="sxs-lookup"><span data-stu-id="71fbf-278">Work is in progress to allow existing Actionable Message scenarios to seamlessly migrate to the universal `Action.Execute` model</span></span>

### <a name="teams"></a><span data-ttu-id="71fbf-279">Teams</span><span class="sxs-lookup"><span data-stu-id="71fbf-279">Teams</span></span>

<span data-ttu-id="71fbf-280">为了使卡片能够后向兼容并适用于旧版 Teams 的用户，`Action.Execute` 操作应包含定义为 `Action.Submit` 的 `fallback` 属性。</span><span class="sxs-lookup"><span data-stu-id="71fbf-280">In order for your cards to be backward compatible and work for users on older versions of Teams, your `Action.Execute` actions should include a `fallback` property defined as an `Action.Submit`.</span></span> <span data-ttu-id="71fbf-281">机器人应以能够同时处理 `Action.Execute` 和 `Action.Submit` 的方式进行编码。</span><span class="sxs-lookup"><span data-stu-id="71fbf-281">Your Bot should be coded in such a way that it can process both `Action.Execute` and `Action.Submit`.</span></span> <span data-ttu-id="71fbf-282">请注意，机器人在处理 `Action.Submit` 时不能返回新卡片，因此通过 `Action.Submit` 的回退行为将为最终用户提供降级的体验。</span><span class="sxs-lookup"><span data-stu-id="71fbf-282">Note that it is not possible for your Bot to return a new card when processing an `Action.Submit`, so fallback behavior via `Action.Submit` will provide a degraded experience for the end user.</span></span>

> #### <a name="important-note"></a><span data-ttu-id="71fbf-283">重要说明</span><span class="sxs-lookup"><span data-stu-id="71fbf-283">Important note</span></span>
> <span data-ttu-id="71fbf-284">若 fallback 属性未包装在 `ActionSet` 中，某些旧版 Teams 客户端不支持该属性。</span><span class="sxs-lookup"><span data-stu-id="71fbf-284">Some older Teams clients do not support fallback property when not wrapped in an `ActionSet`.</span></span> <span data-ttu-id="71fbf-285">为了在此类客户端上不中断，强烈建议将所有 `Action.Execute` 包装在 `ActionSet` 中。</span><span class="sxs-lookup"><span data-stu-id="71fbf-285">In order to not break on such clients, it is **strongly recommended** that you wrap _all_ your `Action.Execute` in `ActionSet`.</span></span> <span data-ttu-id="71fbf-286">请参阅下面的示例，了解如何在 `ActionSet` 中包装 `Action.Execute`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-286">See example below on how to wrap `Action.Execute` in `ActionSet`.</span></span>

<span data-ttu-id="71fbf-287">在以下示例中，请注意，卡片的 `version` 属性设置为 `1.2`，并使用 `Action.Submit` 作为 `fallback` 来定义 `Action.Execute`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-287">In the below example, note the `version` property of the card is set to `1.2` and the `Action.Execute` is defined with an `Action.Submit` as its `fallback`.</span></span> <span data-ttu-id="71fbf-288">当在支持自适应卡片 1.4 的 Teams 客户端中呈现时，`Action.Execute` 将按预期方式呈现并工作。</span><span class="sxs-lookup"><span data-stu-id="71fbf-288">When rendered in a Teams client that supports Adaptive Cards 1.4, the `Action.Execute` will render and work as expected.</span></span> <span data-ttu-id="71fbf-289">在不支持自适应卡片 1.4 的 Teams 客户端中，将呈现 `Action.Submit` 来代替 `Action.Execute`。</span><span class="sxs-lookup"><span data-stu-id="71fbf-289">In Teams clients that do not support Adaptive Cards 1.4, the `Action.Submit` will be rendered in place of the `Action.Execute`.</span></span>

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

## <a name="references"></a><span data-ttu-id="71fbf-290">参考</span><span class="sxs-lookup"><span data-stu-id="71fbf-290">References</span></span>
- [<span data-ttu-id="71fbf-291">自适应卡片 @ Microsoft Build 2020</span><span class="sxs-lookup"><span data-stu-id="71fbf-291">Adaptive Cards @ Microsoft Build 2020</span></span>](https://youtu.be/hEBhwB72Qn4?t=1393)
- [<span data-ttu-id="71fbf-292">自适应卡片 @ Ignite 2020</span><span class="sxs-lookup"><span data-stu-id="71fbf-292">Adaptive Cards @ Ignite 2020</span></span>](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)


































