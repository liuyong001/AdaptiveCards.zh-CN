---
title: 输入验证
author: rebeccaanne
ms.author: rebecch
ms.date: 07/24/2020
ms.topic: article
ms.openlocfilehash: 08fb2cb5b2b6fa1f227ec5a530f8063dc26b40e3
ms.sourcegitcommit: 19c08b1370305fb2965de0140c5e632356e78513
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879138"
---
# <a name="input-validation"></a>输入验证

在架构版本 1.3 及更高版本中，自适应卡片支持对输入类型进行客户端输入验证。

### <a name="validation-properties"></a>验证属性

自适应卡片中支持验证以下属性：

| 输入 | 属性 |
| --- | --- | 
| `Input.ChoiceSet` | `isRequired` | 
| `Input.Date` | `isRequired` <br> `min`<br> `max` | 
| `Input.Number` | `isRequired` <br> `min`<br> `max` |
| `Input.Text` | `isRequired` <br> `regex` <br> `maxLength` |
| `Input.Time` | `isRequired` <br> `min`<br> `max` | 
| `Input.Toggle` | `isRequired` | 

所有输入类型都有 `errorMessage` 属性，用于指定在用户输入无效值时应向其显示的错误。 

> [!NOTE]
>
> 某些平台上的 min 和 max 属性（包括 maxLength）可能由控件直接强制实施。 例如，可以在 Input.Date 上强制实施 min 属性，不允许用户在日期选取器中选择最小值之前的日期。 在这种情况下，可能不会显示错误消息。

## <a name="labels"></a>标签

架构版本 1.3 中为所有输入元素添加的另一属性是 `label` 字符串属性。 要在自适应卡中标记输入项，建议使用 `label` 属性，而不是 `placeholder` 属性。 对于卡片作者，这是添加输入项标签的一种简单、简洁的方式，它具有以下优势：
* 验证指示器：如上所述，现可将输入项标记为“必需”，必需输入项的标签旁边有一个视觉指示器。 该视觉指示器是在 `HostConfig` 中定义的，默认呈现为星号 `*`。
* 辅助功能：通过在标签与输入项之间建立连接，呈现器库可设置必要的属性，来使采用辅助技术（屏幕阅读器）的用户能够在自适应卡中与输入项正确交互。
    * 标签与占位符：如 Katie Sherwin 在 [Placeholders in form fields are harmful](https://www.nngroup.com/articles/form-design-placeholders/)（窗体字段中的占位符是有害的）一文中阐释的，使用占位符会产生很多负面后果，例如考验用户的短期记忆、让用户更难在提交前验证其输入、使用户很难阅读它们，这是因为占位符文本通常与其背景的颜色对比度较差，或者屏幕阅读器根本没法读取占位符文本等等。
    * TextBlock 和 RichTextBlock：虽然使用其他卡片元素作为标签可能看起来是一种很好的解决方案，但它会造成问题，也就是没法在输入项和标签之间强制实施邻近度，而在另一方面，通过使用 `label` 标签，我们可确保可视元素呈现在彼此的旁边，这有助于需要屏幕放大器的用户。

## <a name="fields-to-be-validated-and-submitted"></a>要验证和提交的字段

当用户单击卡片中的 Action.Submit 操作时，将验证输入。 对于给定 Action.Submit 操作，将验证和提交的输入包括：

 - 与 Action.Submit 位于同一卡片上的输入
 - 包含 Action.Submit 的卡片的任何父卡片上的输入（如果 Action.ShowCard 之下有卡片）

如果这些输入通过验证，则会将其字段中的值传递回客户端。 如果未通过验证，则将显示无效输入的错误消息，并且不会发送提交。

> [!NOTE]
>
> 如果输入发生在包含 Action.Submit 的卡片的子卡片或同级卡片上，则不会验证或提交输入。 这包括该卡片正文部分 ActionSets 中的 Action.ShowCards 所显示的卡片。 此行为与 2.0 之前的呈现器版本中不同，适用于所有架构版本的卡片，无论是否使用输入验证属性。 

## <a name="other-considerations-and-known-issues"></a>其他注意事项和已知问题

 - 不推荐使用因 Action.ToggleVisibility 的交互而并非始终可见的验证属性来创建输入。 如果输入当前不可见，则不会显示输入无效的错误消息和视觉指示，这可能会使用户不清楚为什么阻止其提交。

 - 对于使用弹出显示卡片的主机，在主机配置中使用 `"actions":"showCard":"actionMode":"popup"` 值时，未明确定义其输入验证行为。 在将来的版本中可能会弃用弹出显示卡片。