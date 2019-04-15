---
title: 语音和高级自定义
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 19e77b86da9d163f5fcf6a6074071a4638a8d793
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552609"
---
# <a name="speech-and-advanced-customization"></a><span data-ttu-id="4950e-102">语音和高级自定义</span><span class="sxs-lookup"><span data-stu-id="4950e-102">Speech and advanced customization</span></span>
<span data-ttu-id="4950e-103">我们生活在某个时间段的语音交互通过 Cortana 等服务。</span><span class="sxs-lookup"><span data-stu-id="4950e-103">We live in an era of speech interaction via services like Cortana.</span></span>  <span data-ttu-id="4950e-104">从第一天使用的自适应卡旨在支持语音，实现很酷的新手完整方案。</span><span class="sxs-lookup"><span data-stu-id="4950e-104">Adaptive cards are designed from day one to support speech, enabling cool new hands-full scenarios.</span></span>

<span data-ttu-id="4950e-105">`speak`标记允许要发送到的环境可视显示不主体验，如对汽车的仪表板时的自适应卡。</span><span class="sxs-lookup"><span data-stu-id="4950e-105">The `speak` tag enables the adaptive card to be delivered to an environment where a visual display is not primary experience, such as to a car dashboard while driving.</span></span> 

## <a name="speak-property"></a><span data-ttu-id="4950e-106">说出属性</span><span class="sxs-lookup"><span data-stu-id="4950e-106">Speak property</span></span>
<span data-ttu-id="4950e-107">若要支持的语音，我们`speak`属性，其中包含要向用户说出的文本。</span><span class="sxs-lookup"><span data-stu-id="4950e-107">To support speech we have a `speak` property which contains text to say to the user.</span></span> <span data-ttu-id="4950e-108">可以使用语音合成标记语言批注文本 ([SSML](https://msdn.microsoft.com/en-us/library/office/hh361578))。</span><span class="sxs-lookup"><span data-stu-id="4950e-108">The text can be annotated using speech synthesis markup language ([SSML](https://msdn.microsoft.com/en-us/library/office/hh361578)).</span></span> <span data-ttu-id="4950e-109">SSML 控制速度、 风格和语音的转折点。</span><span class="sxs-lookup"><span data-stu-id="4950e-109">SSML controls the speed, tone, and inflection of the speech.</span></span>  <span data-ttu-id="4950e-110">它甚至允许您对音频进行流式处理或呈现 TTS 音频流从你自己的服务，为你提供自定义来很好大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="4950e-110">It even allows you to stream audio or a render a TTS audio stream from your own service, giving you a great deal of flexibility for customization.</span></span>

<span data-ttu-id="4950e-111">有两种模式来朗读属性使用由主机应用程序：</span><span class="sxs-lookup"><span data-stu-id="4950e-111">There are two patterns for speak property usage by a host application:</span></span>

* <span data-ttu-id="4950e-112">**交付**-卡传递时，客户端可以选择读取 Speak 属性来描述作为一个整体的卡的卡。</span><span class="sxs-lookup"><span data-stu-id="4950e-112">**On delivery** - When a card is delivered, the client may opt to read the Speak property for the card to describe the card as a whole.</span></span>
* <span data-ttu-id="4950e-113">**按需**-为了支持更丰富的可访问性模型，speak 标记的每个元素的架构支持。</span><span class="sxs-lookup"><span data-stu-id="4950e-113">**On demand** - In order to support a richer accessibility model, the schema supports a speak tag for each element.</span></span> <span data-ttu-id="4950e-114">客户端可以读取在卡片中的每个元素的 Speak 属性。</span><span class="sxs-lookup"><span data-stu-id="4950e-114">The client may read a Speak property  for each element in the card.</span></span>

### <a name="examples"></a><span data-ttu-id="4950e-115">示例</span><span class="sxs-lookup"><span data-stu-id="4950e-115">Examples</span></span>

```json
    "speak":"hello world!"

    "speak":"<s>This is sentence 1.</s><s>This is sentence two</s>"

    "speak":"<speak><audio src='https://www.soundjay.com/misc/bell-ringing-04.mp3'/><s>Time to wake up!</s></speak>"
```

## <a name="speech-content-design"></a><span data-ttu-id="4950e-116">语音内容设计</span><span class="sxs-lookup"><span data-stu-id="4950e-116">Speech content design</span></span>

<span data-ttu-id="4950e-117">设计为语音的内容与设计进行可视显示的内容不同。</span><span class="sxs-lookup"><span data-stu-id="4950e-117">Content designed for speech is different from content designed for visual display.</span></span> <span data-ttu-id="4950e-118">在设计时数据卡，您正在设计整个的视觉体验，以向 delights 它们一种方法中的用户显示信息。</span><span class="sxs-lookup"><span data-stu-id="4950e-118">When you design a card, you are designing an entire visual experience to present information to a user in a way that delights them.</span></span> <span data-ttu-id="4950e-119">语音的设计时，您应考虑如何口头描述 delights 用户一种方法中的内容。</span><span class="sxs-lookup"><span data-stu-id="4950e-119">When designing for speech, you should think about how to verbally describe the content in a way that delights the user.</span></span>  
