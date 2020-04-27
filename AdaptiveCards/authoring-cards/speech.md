---
title: 语音和高级自定义
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 1dfd9b0c45a280905223e3286998b333b0a6ec6a
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "76145338"
---
# <a name="speech-and-advanced-customization"></a><span data-ttu-id="73733-102">语音和高级自定义</span><span class="sxs-lookup"><span data-stu-id="73733-102">Speech and advanced customization</span></span>
<span data-ttu-id="73733-103">我们生活在一个可以通过 Cortana 之类的服务进行语音交互的时代。</span><span class="sxs-lookup"><span data-stu-id="73733-103">We live in an era of speech interaction via services like Cortana.</span></span>  <span data-ttu-id="73733-104">从第一天开始，自适应卡片在设计时就考虑到要支持语音，启用可应对用户超忙情况的全新超酷方案。</span><span class="sxs-lookup"><span data-stu-id="73733-104">Adaptive cards are designed from day one to support speech, enabling cool new hands-full scenarios.</span></span>

<span data-ttu-id="73733-105">可以通过 `speak` 标记为视觉显示不是主要体验的环境（例如，在驾驶时使用的汽车仪表板）提供自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="73733-105">The `speak` tag enables the adaptive card to be delivered to an environment where a visual display is not primary experience, such as to a car dashboard while driving.</span></span> 

## <a name="speak-property"></a><span data-ttu-id="73733-106">Speak 属性</span><span class="sxs-lookup"><span data-stu-id="73733-106">Speak property</span></span>
<span data-ttu-id="73733-107">为了支持语音，我们使用了 `speak` 属性，其中包含要说给用户听的文本。</span><span class="sxs-lookup"><span data-stu-id="73733-107">To support speech we have a `speak` property which contains text to say to the user.</span></span> <span data-ttu-id="73733-108">文本可以使用语音合成标记语言 ([SSML](https://msdn.microsoft.com/library/office/hh361578)) 进行标注。</span><span class="sxs-lookup"><span data-stu-id="73733-108">The text can be annotated using speech synthesis markup language ([SSML](https://msdn.microsoft.com/library/office/hh361578)).</span></span> <span data-ttu-id="73733-109">SSML 控制语音的速度、语气和音调。</span><span class="sxs-lookup"><span data-stu-id="73733-109">SSML controls the speed, tone, and inflection of the speech.</span></span>  <span data-ttu-id="73733-110">它甚至允许你流式传输音频，或者呈现由你自己的服务提供的 TTS 音频流，让你可以很灵活地进行自定义。</span><span class="sxs-lookup"><span data-stu-id="73733-110">It even allows you to stream audio or a render a TTS audio stream from your own service, giving you a great deal of flexibility for customization.</span></span>

<span data-ttu-id="73733-111">主机应用程序可以通过两种模式来使用 speak 属性：</span><span class="sxs-lookup"><span data-stu-id="73733-111">There are two patterns for speak property usage by a host application:</span></span>

* <span data-ttu-id="73733-112">**按交付** - 将卡片交付给客户时，客户可以选择让系统读出对卡片进行整体说明的卡片 Speak 属性。</span><span class="sxs-lookup"><span data-stu-id="73733-112">**On delivery** - When a card is delivered, the client may opt to read the Speak property for the card to describe the card as a whole.</span></span>
* <span data-ttu-id="73733-113">**按需** - 架构支持为每个元素设置一个 speak 标记，这样就可以支持内容更丰富的辅助功能模型。</span><span class="sxs-lookup"><span data-stu-id="73733-113">**On demand** - In order to support a richer accessibility model, the schema supports a speak tag for each element.</span></span> <span data-ttu-id="73733-114">客户可以让系统读出卡片中每个元素的 Speak 属性。</span><span class="sxs-lookup"><span data-stu-id="73733-114">The client may read a Speak property  for each element in the card.</span></span>

### <a name="examples"></a><span data-ttu-id="73733-115">示例</span><span class="sxs-lookup"><span data-stu-id="73733-115">Examples</span></span>

```json
    "speak":"hello world!"

    "speak":"<s>This is sentence 1.</s><s>This is sentence two</s>"

    "speak":"<speak><audio src='https://www.soundjay.com/misc/bell-ringing-04.mp3'/><s>Time to wake up!</s></speak>"
```

## <a name="speech-content-design"></a><span data-ttu-id="73733-116">语音内容设计</span><span class="sxs-lookup"><span data-stu-id="73733-116">Speech content design</span></span>

<span data-ttu-id="73733-117">为语音设计的内容不同于为视觉显示设计的内容。</span><span class="sxs-lookup"><span data-stu-id="73733-117">Content designed for speech is different from content designed for visual display.</span></span> <span data-ttu-id="73733-118">在设计卡片时，你是在设计整个视觉体验，需要以用户满意的方式将信息提供给用户。</span><span class="sxs-lookup"><span data-stu-id="73733-118">When you design a card, you are designing an entire visual experience to present information to a user in a way that delights them.</span></span> <span data-ttu-id="73733-119">针对语音进行设计时，应考虑如何以用户满意的方式口头介绍内容。</span><span class="sxs-lookup"><span data-stu-id="73733-119">When designing for speech, you should think about how to verbally describe the content in a way that delights the user.</span></span>  
