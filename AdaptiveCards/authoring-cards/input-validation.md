---
title: 输入验证
author: rebeccaanne
ms.author: rebecch
ms.date: 07/24/2020
ms.topic: article
ms.openlocfilehash: fe8602ecfb308afeb7a42b82c22b49c33911d20d
ms.sourcegitcommit: 65b792d73c264c943036343e05b75f2b0488e6e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "95001764"
---
# <a name="input-validation"></a><span data-ttu-id="57702-102">输入验证</span><span class="sxs-lookup"><span data-stu-id="57702-102">Input Validation</span></span>

<span data-ttu-id="57702-103">在架构版本 1.3 及更高版本中，自适应卡片支持对输入类型进行客户端输入验证。</span><span class="sxs-lookup"><span data-stu-id="57702-103">In versions 1.3 and later of the schema, AdaptiveCards supports client side input validation of Input types.</span></span>

### <a name="validation-properties"></a><span data-ttu-id="57702-104">验证属性</span><span class="sxs-lookup"><span data-stu-id="57702-104">Validation Properties</span></span>

<span data-ttu-id="57702-105">自适应卡片中支持验证以下属性：</span><span class="sxs-lookup"><span data-stu-id="57702-105">The following properties are supported for validation in AdaptiveCards:</span></span>

| <span data-ttu-id="57702-106">输入</span><span class="sxs-lookup"><span data-stu-id="57702-106">Input</span></span> | <span data-ttu-id="57702-107">属性</span><span class="sxs-lookup"><span data-stu-id="57702-107">Properties</span></span> |
| --- | --- | 
| `Input.ChoiceSet` | `isRequired` | 
| `Input.Date` | `isRequired` <br> `min`<br> `max` | 
| `Input.Number` | `isRequired` <br> `min`<br> `max` |
| `Input.Text` | `isRequired` <br> `regex` <br> `maxLength` |
| `Input.Time` | `isRequired` <br> `min`<br> `max` | 
| `Input.Toggle` | `isRequired` | 

<span data-ttu-id="57702-108">所有输入类型都有 `errorMessage` 属性，用于指定在用户输入无效值时应向其显示的错误。</span><span class="sxs-lookup"><span data-stu-id="57702-108">An `errorMessage` property is available on all input types to specify what error a user should be shown if they enter an invalid value.</span></span> 

> [!NOTE]
>
> <span data-ttu-id="57702-109">某些平台上的 min 和 max 属性（包括 maxLength）可能由控件直接强制实施。</span><span class="sxs-lookup"><span data-stu-id="57702-109">Min and max properties (including maxLength) on some platforms may be enforced directly by the control.</span></span> <span data-ttu-id="57702-110">例如，可以在 Input.Date 上强制实施 min 属性，不允许用户在日期选取器中选择最小值之前的日期。</span><span class="sxs-lookup"><span data-stu-id="57702-110">For example, a min property on Input.Date may be enforced by not allowing users to select a date before the minimum in a date picker.</span></span> <span data-ttu-id="57702-111">在这种情况下，可能不会显示错误消息。</span><span class="sxs-lookup"><span data-stu-id="57702-111">In that case, the error message may not be shown.</span></span>

## <a name="labels"></a><span data-ttu-id="57702-112">标签</span><span class="sxs-lookup"><span data-stu-id="57702-112">Labels</span></span>

<span data-ttu-id="57702-113">架构版本 1.3 中为所有输入元素添加的另一属性是 `label` 字符串属性。</span><span class="sxs-lookup"><span data-stu-id="57702-113">Another property added in schema version 1.3 for all input elements is the `label` string property.</span></span> <span data-ttu-id="57702-114">要在自适应卡中标记输入项，建议使用 `label` 属性，而不是 `placeholder` 属性。</span><span class="sxs-lookup"><span data-stu-id="57702-114">Using the `label` property is the recommended way of tagging inputs in an Adaptive Card, vis-a-vis the `placeholder` property.</span></span> <span data-ttu-id="57702-115">对于卡片作者，这是添加输入项标签的一种简单、简洁的方式，它具有以下优势：</span><span class="sxs-lookup"><span data-stu-id="57702-115">It is a simple and concise way of labelling inputs for card authors and has the following benefits:</span></span>

* <span data-ttu-id="57702-116">验证指示器：如上所述，现可将输入项标记为“必需”，必需输入项的标签旁边有一个视觉指示器。</span><span class="sxs-lookup"><span data-stu-id="57702-116">Validation indicators: as mentioned above inputs can be now marked as required, labels for required inputs will have a visual indicator next to them.</span></span> <span data-ttu-id="57702-117">该视觉指示器是在 `HostConfig` 中定义的，默认呈现为星号 `*`。</span><span class="sxs-lookup"><span data-stu-id="57702-117">This visual indicator is defined in the `HostConfig` and by default is rendered as an asterisk `*`.</span></span>
* <span data-ttu-id="57702-118">辅助功能：通过在标签与输入项之间建立连接，呈现器库可设置必要的属性，来使采用辅助技术（屏幕阅读器）的用户能够在自适应卡中与输入项正确交互。</span><span class="sxs-lookup"><span data-stu-id="57702-118">Accessibility: by having a connection between labels and inputs, renderer libraries can set the necessary properties to allow users using assistive technologies (screen readers) to be able to interact correctly with inputs inside adaptive cards.</span></span>
    * <span data-ttu-id="57702-119">标签与占位符：如 Katie Sherwin 在 [Placeholders in form fields are harmful](https://www.nngroup.com/articles/form-design-placeholders/)（窗体字段中的占位符是有害的）一文中阐释的，使用占位符会产生很多负面后果，例如考验用户的短期记忆、让用户更难在提交前验证其输入、使用户很难阅读它们，这是因为占位符文本通常与其背景的颜色对比度较差，或者屏幕阅读器根本没法读取占位符文本等等。</span><span class="sxs-lookup"><span data-stu-id="57702-119">Labels vs Placeholders: as Katie Sherwin explains in the article [Placeholders in form fields are harmful](https://www.nngroup.com/articles/form-design-placeholders/) using placeholders has many negative consequences such as straining users' short term memory, making it harder for users to verify their inputs before submitting, providing difficulties for users to read them as, usually, placeholder text has poor color contrast against it's background or screen readers not reading the placeholder text at all, just to name a few.</span></span>
    * <span data-ttu-id="57702-120">TextBlock 和 RichTextBlock：虽然使用其他卡片元素作为标签可能看起来是一种很好的解决方案，但它会造成问题，也就是没法在输入项和标签之间强制实施邻近度，而在另一方面，通过使用 `label` 标签，我们可确保可视元素呈现在彼此的旁边，这有助于需要屏幕放大器的用户。</span><span class="sxs-lookup"><span data-stu-id="57702-120">TextBlock and RichTextBlock: while using other card elements as labels may seem as a good solution it presents the issue of not being able to enforce proximity between inputs and labels, on the other hand by using the `label` property, we can ensure that both visual elements are rendered next to each other which helps users who need screen magnifiers.</span></span>

## <a name="fields-to-be-validated-and-submitted"></a><span data-ttu-id="57702-121">要验证和提交的字段</span><span class="sxs-lookup"><span data-stu-id="57702-121">Fields to be validated and submitted</span></span>

<span data-ttu-id="57702-122">当用户单击卡片中的 Action.Submit 操作时，将验证输入。</span><span class="sxs-lookup"><span data-stu-id="57702-122">Inputs will be validated when the user clicks on an Action.Submit action in the card.</span></span> <span data-ttu-id="57702-123">对于给定 Action.Submit 操作，将验证和提交的输入包括：</span><span class="sxs-lookup"><span data-stu-id="57702-123">Those inputs which will be validated and submitted for a given Action.Submit action are:</span></span>

 - <span data-ttu-id="57702-124">与 Action.Submit 位于同一卡片上的输入</span><span class="sxs-lookup"><span data-stu-id="57702-124">Inputs on the same card as the Action.Submit</span></span>
 - <span data-ttu-id="57702-125">包含 Action.Submit 的卡片的任何父卡片上的输入（如果 Action.ShowCard 之下有卡片）</span><span class="sxs-lookup"><span data-stu-id="57702-125">Inputs on any parent cards of the card containing the Action.Submit in the case of a card under an Action.ShowCard</span></span>

<span data-ttu-id="57702-126">如果这些输入通过验证，则会将其字段中的值传递回客户端。</span><span class="sxs-lookup"><span data-stu-id="57702-126">If those inputs pass validation, the values in their fields will be passed back to the client.</span></span> <span data-ttu-id="57702-127">如果未通过验证，则将显示无效输入的错误消息，并且不会发送提交。</span><span class="sxs-lookup"><span data-stu-id="57702-127">If they do not pass validation, the error messages for the invalid inputs will be shown, and the submit will not be sent.</span></span>

> [!NOTE]
>
> <span data-ttu-id="57702-128">如果输入发生在包含 Action.Submit 的卡片的子卡片或同级卡片上，则不会验证或提交输入。</span><span class="sxs-lookup"><span data-stu-id="57702-128">Inputs will **not** be validated or submitted if they are on a card that is a child or sibling card of the card containing the Action.Submit.</span></span> <span data-ttu-id="57702-129">这包括该卡片正文部分 ActionSets 中的 Action.ShowCards 所显示的卡片。</span><span class="sxs-lookup"><span data-stu-id="57702-129">This includes cards from Action.ShowCards in ActionSets in the body of that card.</span></span> <span data-ttu-id="57702-130">此行为与 2.0 之前的呈现器版本中不同，适用于所有架构版本的卡片，无论是否使用输入验证属性。</span><span class="sxs-lookup"><span data-stu-id="57702-130">This is a change in behavior from renderer versions prior to 2.0, and applies to cards of all schema versions, regardless of whether input validation properties are used.</span></span> 

## <a name="other-considerations-and-known-issues"></a><span data-ttu-id="57702-131">其他注意事项和已知问题</span><span class="sxs-lookup"><span data-stu-id="57702-131">Other Considerations and Known Issues</span></span>

 - <span data-ttu-id="57702-132">不推荐使用因 Action.ToggleVisibility 的交互而并非始终可见的验证属性来创建输入。</span><span class="sxs-lookup"><span data-stu-id="57702-132">It is not recommended to create inputs with validation properties that may not always be visible due to interaction with Action.ToggleVisibility.</span></span> <span data-ttu-id="57702-133">如果输入当前不可见，则不会显示输入无效的错误消息和视觉指示，这可能会使用户不清楚为什么阻止其提交。</span><span class="sxs-lookup"><span data-stu-id="57702-133">Error messages and visual indications that the input is invalid will not be shown if the input is not currently visible, which may cause confusion for users as to why their submit is blocked.</span></span>

 - <span data-ttu-id="57702-134">对于使用弹出显示卡片的主机，在主机配置中使用 `"actions":"showCard":"actionMode":"popup"` 值时，未明确定义其输入验证行为。</span><span class="sxs-lookup"><span data-stu-id="57702-134">Behavior of input validation for hosts using popup show cards using the  `"actions":"showCard":"actionMode":"popup"` value in their host config is not well defined.</span></span> <span data-ttu-id="57702-135">在将来的版本中可能会弃用弹出显示卡片。</span><span class="sxs-lookup"><span data-stu-id="57702-135">Popup show cards may be deprecated in a future release.</span></span>