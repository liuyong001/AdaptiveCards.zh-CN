---
title: 语音和高级自定义
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 1dfd9b0c45a280905223e3286998b333b0a6ec6a
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145338"
---
# <a name="speech-and-advanced-customization"></a>语音和高级自定义
我们生活在一个可以通过 Cortana 之类的服务进行语音交互的时代。  从第一天开始，自适应卡片在设计时就考虑到要支持语音，启用可应对用户超忙情况的全新超酷方案。

可以通过 `speak` 标记为视觉显示不是主要体验的环境（例如，在驾驶时使用的汽车仪表板）提供自适应卡片。 

## <a name="speak-property"></a>Speak 属性
为了支持语音，我们使用了 `speak` 属性，其中包含要说给用户听的文本。 文本可以使用语音合成标记语言 ([SSML](https://msdn.microsoft.com/library/office/hh361578)) 进行标注。 SSML 控制语音的速度、语气和音调。  它甚至允许你流式传输音频，或者呈现由你自己的服务提供的 TTS 音频流，让你可以很灵活地进行自定义。

主机应用程序可以通过两种模式来使用 speak 属性：

* **按交付** - 将卡片交付给客户时，客户可以选择让系统读出对卡片进行整体说明的卡片 Speak 属性。
* **按需** - 架构支持为每个元素设置一个 speak 标记，这样就可以支持内容更丰富的辅助功能模型。 客户可以让系统读出卡片中每个元素的 Speak 属性。

### <a name="examples"></a>示例

```json
    "speak":"hello world!"

    "speak":"<s>This is sentence 1.</s><s>This is sentence two</s>"

    "speak":"<speak><audio src='https://www.soundjay.com/misc/bell-ringing-04.mp3'/><s>Time to wake up!</s></speak>"
```

## <a name="speech-content-design"></a>语音内容设计

为语音设计的内容不同于为视觉显示设计的内容。 在设计卡片时，你是在设计整个视觉体验，需要以用户满意的方式将信息提供给用户。 针对语音进行设计时，应考虑如何以用户满意的方式口头介绍内容。  
