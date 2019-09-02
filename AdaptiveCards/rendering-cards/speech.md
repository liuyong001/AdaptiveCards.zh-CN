---
title: 处理语音
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 64eeaefbc2ac775b69bd48cc853beb729cb2c37f
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67137990"
---
# <a name="handling-speech"></a><span data-ttu-id="322eb-102">处理语音</span><span class="sxs-lookup"><span data-stu-id="322eb-102">Handling speech</span></span>

<span data-ttu-id="322eb-103">自适应卡片有一个支持语音功能的 `speak` 属性，其中包含的信息会告知卡片如何向用户大声朗读相关内容。</span><span class="sxs-lookup"><span data-stu-id="322eb-103">To support speech adaptive Cards has the `speak` property which contains information on how a card should be read aloud to a user.</span></span>

<span data-ttu-id="322eb-104">可以使用 [SSML 标记](https://msdn.microsoft.com/en-us/library/office/hh361578(v=office.14).aspx)来标注语音标记。</span><span class="sxs-lookup"><span data-stu-id="322eb-104">The speech tag can be annotated using  [SSML markup](https://msdn.microsoft.com/en-us/library/office/hh361578(v=office.14).aspx).</span></span> <span data-ttu-id="322eb-105">可以通过 SSML 控制语音的速度、语气和音调。</span><span class="sxs-lookup"><span data-stu-id="322eb-105">SSML gives you the ability control the speed, tone, inflection of the speech.</span></span>  <span data-ttu-id="322eb-106">它甚至允许你流式传输音频，或者呈现由你自己的服务提供的 TTS 音频流，让你可以进行自定义。</span><span class="sxs-lookup"><span data-stu-id="322eb-106">It even allows you to stream audio or a render a TTS audio stream from your own service, giving you a great deal of customization.</span></span>

<span data-ttu-id="322eb-107">主机应用程序可以通过 2 种模式来使用 speak 属性：</span><span class="sxs-lookup"><span data-stu-id="322eb-107">There are 2 patterns for speak property usage by a host application:</span></span>
* <span data-ttu-id="322eb-108">**按交付** - 将卡片交付给客户时，客户可以选择让系统读出对卡片进行整体说明的卡片 Speak 属性。</span><span class="sxs-lookup"><span data-stu-id="322eb-108">**on delivery** - When a card is delivered a client may opt to read the Speak property for the card to describe the card as a whole.</span></span>
* <span data-ttu-id="322eb-109">**按需** - 架构支持为每个元素设置一个 speak 标记，这样就可以支持内容更丰富的辅助功能模型。</span><span class="sxs-lookup"><span data-stu-id="322eb-109">**on demand** - In order to support a richer accessibility model the schema supports a speak tag per element.</span></span>  
<span data-ttu-id="322eb-110">这样客户端就可以按照辅助功能要求将每个元素读给接收者。</span><span class="sxs-lookup"><span data-stu-id="322eb-110">This allows for clients to read each element to recipients with accessibility requirements.</span></span>

