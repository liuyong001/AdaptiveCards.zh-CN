---
title: 处理语音
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: fb56c97da3cca776da0fc7ea65a9726c8826e910
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145537"
---
# <a name="handling-speech"></a>处理语音

自适应卡片有一个支持语音功能的 `speak` 属性，其中包含的信息会告知卡片如何向用户大声朗读相关内容。

可以使用 [SSML 标记](https://msdn.microsoft.com/library/office/hh361578(v=office.14).aspx)来标注语音标记。 可以通过 SSML 控制语音的速度、语气和音调。  它甚至允许你流式传输音频，或者呈现由你自己的服务提供的 TTS 音频流，让你可以进行自定义。

主机应用程序可以通过 2 种模式来使用 speak 属性：
* **按交付** - 将卡片交付给客户时，客户可以选择让系统读出对卡片进行整体说明的卡片 Speak 属性。
* **按需** - 架构支持为每个元素设置一个 speak 标记，这样就可以支持内容更丰富的辅助功能模型。  
这样客户端就可以按照辅助功能要求将每个元素读给接收者。

