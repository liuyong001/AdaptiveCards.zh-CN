---
title: 输入验证
author: rebeccaanne
ms.author: rebecch
ms.date: 07/24/2020
ms.topic: article
ms.openlocfilehash: 4c8aa73a218946944b25557eae141e231e8a6ac5
ms.sourcegitcommit: 2a394b75439b382d7bc3134078ecff02429617b8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544957"
---
# <a name="input-validation"></a><span data-ttu-id="bf9dc-102">输入验证</span><span class="sxs-lookup"><span data-stu-id="bf9dc-102">Input Validation</span></span>

<span data-ttu-id="bf9dc-103">在架构版本 1.3 及更高版本中，自适应卡片支持对输入类型进行客户端输入验证。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-103">In versions 1.3 and later of the schema, AdaptiveCards supports client side input validation of Input types.</span></span>

### <a name="validation-properties"></a><span data-ttu-id="bf9dc-104">验证属性</span><span class="sxs-lookup"><span data-stu-id="bf9dc-104">Validation Properties</span></span>

<span data-ttu-id="bf9dc-105">自适应卡片中支持验证以下属性：</span><span class="sxs-lookup"><span data-stu-id="bf9dc-105">The following properties are supported for validation in AdaptiveCards:</span></span>

| <span data-ttu-id="bf9dc-106">输入</span><span class="sxs-lookup"><span data-stu-id="bf9dc-106">Input</span></span> | <span data-ttu-id="bf9dc-107">属性</span><span class="sxs-lookup"><span data-stu-id="bf9dc-107">Properties</span></span> |
| --- | --- | 
| `Input.ChoiceSet` | `isRequired` | 
| `Input.Date` | `isRequired` <br> `min`<br> `max` | 
| `Input.Number` | `isRequired` <br> `min`<br> `max` |
| `Input.Text` | `isRequired` <br> `regex` <br> `maxLength` |
| `Input.Time` | `isRequired` <br> `min`<br> `max` | 
| `Input.Toggle` | `isRequired` | 

<span data-ttu-id="bf9dc-108">所有输入类型都有 `errorMessage` 属性，用于指定在用户输入无效值时应向其显示的错误。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-108">An `errorMessage` property is available on all input types to specify what error a user should be shown if they enter an invalid value.</span></span> 

> [!NOTE]
>
> <span data-ttu-id="bf9dc-109">某些平台上的 min 和 max 属性（包括 maxLength）可能由控件直接强制实施。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-109">Min and max properties (including maxLength) on some platforms may be enforced directly by the control.</span></span> <span data-ttu-id="bf9dc-110">例如，可以在 Input.Date 上强制实施 min 属性，不允许用户在日期选取器中选择最小值之前的日期。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-110">For example, a min property on Input.Date may be enforced by not allowing users to select a date before the minimum in a date picker.</span></span> <span data-ttu-id="bf9dc-111">在这种情况下，可能不会显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-111">In that case, the error message may not be shown.</span></span>

## <a name="fields-to-be-validated-and-submitted"></a><span data-ttu-id="bf9dc-112">要验证和提交的字段</span><span class="sxs-lookup"><span data-stu-id="bf9dc-112">Fields to be validated and submitted</span></span>

<span data-ttu-id="bf9dc-113">当用户单击卡片中的 Action.Submit 操作时，将验证输入。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-113">Inputs will be validated when the user clicks on an Action.Submit action in the card.</span></span> <span data-ttu-id="bf9dc-114">对于给定 Action.Submit 操作，将验证和提交的输入包括：</span><span class="sxs-lookup"><span data-stu-id="bf9dc-114">Those inputs which will be validated and submitted for a given Action.Submit action are:</span></span>

 - <span data-ttu-id="bf9dc-115">与 Action.Submit 位于同一卡片上的输入</span><span class="sxs-lookup"><span data-stu-id="bf9dc-115">Inputs on the same card as the Action.Submit</span></span>
 - <span data-ttu-id="bf9dc-116">包含 Action.Submit 的卡片的任何父卡片上的输入（如果 Action.ShowCard 之下有卡片）</span><span class="sxs-lookup"><span data-stu-id="bf9dc-116">Inputs on any parent cards of the card containing the Action.Submit in the case of a card under an Action.ShowCard</span></span>

<span data-ttu-id="bf9dc-117">如果这些输入通过验证，则会将其字段中的值传递回客户端。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-117">If those inputs pass validation, the values in their fields will be passed back to the client.</span></span> <span data-ttu-id="bf9dc-118">如果未通过验证，则将显示无效输入的错误消息，并且不会发送提交。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-118">If they do not pass validation, the error messages for the invalid inputs will be shown, and the submit will not be sent.</span></span>

> [!NOTE]
>
> <span data-ttu-id="bf9dc-119">如果输入发生在包含 Action.Submit 的卡片的子卡片或同级卡片上，则不会验证或提交输入。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-119">Inputs will **not** be validated or submitted if they are on a card that is a child or sibling card of the card containing the Action.Submit.</span></span> <span data-ttu-id="bf9dc-120">这包括该卡片正文部分 ActionSets 中的 Action.ShowCards 所显示的卡片。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-120">This includes cards from Action.ShowCards in ActionSets in the body of that card.</span></span> <span data-ttu-id="bf9dc-121">此行为与 2.0 之前的呈现器版本中不同，适用于所有架构版本的卡片，无论是否使用输入验证属性。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-121">This is a change in behavior from renderer versions prior to 2.0, and applies to cards of all schema versions, regardless of whether input validation properties are used.</span></span> 

## <a name="other-considerations-and-known-issues"></a><span data-ttu-id="bf9dc-122">其他注意事项和已知问题</span><span class="sxs-lookup"><span data-stu-id="bf9dc-122">Other Considerations and Known Issues</span></span>

 - <span data-ttu-id="bf9dc-123">不推荐使用因 Action.ToggleVisibility 的交互而并非始终可见的验证属性来创建输入。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-123">It is not recommended to create inputs with validation properties that may not always be visible due to interaction with Action.ToggleVisibility.</span></span> <span data-ttu-id="bf9dc-124">如果输入当前不可见，则不会显示输入无效的错误消息和视觉指示，这可能会使用户不清楚为什么阻止其提交。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-124">Error messages and visual indications that the input is invalid will not be shown if the input is not currently visible, which may cause confusion for users as to why their submit is blocked.</span></span>

 - <span data-ttu-id="bf9dc-125">对于使用弹出显示卡片的主机，在主机配置中使用 `"actions":"showCard":"actionMode":"popup"` 值时，未明确定义其输入验证行为。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-125">Behavior of input validation for hosts using popup show cards using the  `"actions":"showCard":"actionMode":"popup"` value in their host config is not well defined.</span></span> <span data-ttu-id="bf9dc-126">在将来的版本中可能会弃用弹出显示卡片。</span><span class="sxs-lookup"><span data-stu-id="bf9dc-126">Popup show cards may be deprecated in a future release.</span></span>

