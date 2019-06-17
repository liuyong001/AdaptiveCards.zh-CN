---
title: 处理语音
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 64eeaefbc2ac775b69bd48cc853beb729cb2c37f
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67137990"
---
# <a name="handling-speech"></a>处理语音

为自适应卡具有支持语音`speak`属性，其中包含如何卡应被朗读用户的信息。

可以使用带批注的语音标记[SSML 标记](https://msdn.microsoft.com/en-us/library/office/hh361578(v=office.14).aspx)。 SSML 提供功能控制的速度，音、 语音的转折点。  它甚至允许您对音频进行流式处理或呈现 TTS 音频流从你自己的服务，为您提供了大量的自定义项。

有 2 个模式由主机应用程序朗读属性用法：
* **交付**-卡传递客户端时可能会选择读取 Speak 属性来描述作为一个整体的卡的卡。
* **按需**-为了支持更丰富的可访问性模型 speak 标记每个元素的架构支持。  
这允许客户端向具有辅助功能要求收件人读取每个元素。

