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
# <a name="speech-and-advanced-customization"></a>语音和高级自定义
我们生活在某个时间段的语音交互通过 Cortana 等服务。  从第一天使用的自适应卡旨在支持语音，实现很酷的新手完整方案。

`speak`标记允许要发送到的环境可视显示不主体验，如对汽车的仪表板时的自适应卡。 

## <a name="speak-property"></a>说出属性
若要支持的语音，我们`speak`属性，其中包含要向用户说出的文本。 可以使用语音合成标记语言批注文本 ([SSML](https://msdn.microsoft.com/en-us/library/office/hh361578))。 SSML 控制速度、 风格和语音的转折点。  它甚至允许您对音频进行流式处理或呈现 TTS 音频流从你自己的服务，为你提供自定义来很好大的灵活性。

有两种模式来朗读属性使用由主机应用程序：

* **交付**-卡传递时，客户端可以选择读取 Speak 属性来描述作为一个整体的卡的卡。
* **按需**-为了支持更丰富的可访问性模型，speak 标记的每个元素的架构支持。 客户端可以读取在卡片中的每个元素的 Speak 属性。

### <a name="examples"></a>示例

```json
    "speak":"hello world!"

    "speak":"<s>This is sentence 1.</s><s>This is sentence two</s>"

    "speak":"<speak><audio src='https://www.soundjay.com/misc/bell-ringing-04.mp3'/><s>Time to wake up!</s></speak>"
```

## <a name="speech-content-design"></a>语音内容设计

设计为语音的内容与设计进行可视显示的内容不同。 在设计时数据卡，您正在设计整个的视觉体验，以向 delights 它们一种方法中的用户显示信息。 语音的设计时，您应考虑如何口头描述 delights 用户一种方法中的内容。  
