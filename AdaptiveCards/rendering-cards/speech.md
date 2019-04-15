---
title: 处理语音
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: daea48607376c84f0e0f0af9450cac7dcdf67c0e
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552479"
---
# <a name="handling-speech"></a><span data-ttu-id="c05b9-102">处理语音</span><span class="sxs-lookup"><span data-stu-id="c05b9-102">Handling speech</span></span>

<span data-ttu-id="c05b9-103">为自适应卡具有支持语音`speak`属性，其中包含如何卡应被朗读用户的信息。</span><span class="sxs-lookup"><span data-stu-id="c05b9-103">To support speech adaptive Cards has the `speak` property which contains information on how a card shoudl be read aloud to a user.</span></span>

<span data-ttu-id="c05b9-104">可以使用带批注的语音标记[SSML 标记](https://msdn.microsoft.com/en-us/library/office/hh361578(v=office.14).aspx)。</span><span class="sxs-lookup"><span data-stu-id="c05b9-104">The speech tag can be annotated using  [SSML markup](https://msdn.microsoft.com/en-us/library/office/hh361578(v=office.14).aspx).</span></span> <span data-ttu-id="c05b9-105">SSML 提供功能控制的速度，音、 语音的转折点。</span><span class="sxs-lookup"><span data-stu-id="c05b9-105">SSML gives you the ability control the speed, tone, inflection of the speech.</span></span>  <span data-ttu-id="c05b9-106">它甚至允许您对音频进行流式处理或呈现 TTS 音频流从你自己的服务，为您提供了大量的自定义项。</span><span class="sxs-lookup"><span data-stu-id="c05b9-106">It even allows you to stream audio or a render a TTS audio stream from your own service, giving you a great deal of customization.</span></span>

<span data-ttu-id="c05b9-107">有 2 个模式由主机应用程序朗读属性用法：</span><span class="sxs-lookup"><span data-stu-id="c05b9-107">There are 2 patterns for speak property usage by a host application:</span></span>
* <span data-ttu-id="c05b9-108">**交付**-卡传递客户端时可能会选择读取 Speak 属性来描述作为一个整体的卡的卡。</span><span class="sxs-lookup"><span data-stu-id="c05b9-108">**on delivery** - When a card is delivered a client may opt to read the Speak property for the card to describe the card as a whole.</span></span>
* <span data-ttu-id="c05b9-109">**按需**-为了支持更丰富的可访问性模型 speak 标记每个元素的架构支持。</span><span class="sxs-lookup"><span data-stu-id="c05b9-109">**on demand** - In order to support a richer accessibility model the schema supports a speak tag per element.</span></span>  
<span data-ttu-id="c05b9-110">这允许客户端向具有辅助功能要求收件人读取每个元素。</span><span class="sxs-lookup"><span data-stu-id="c05b9-110">This allows for clients to read each element to recipients with accessibility requirements.</span></span>

