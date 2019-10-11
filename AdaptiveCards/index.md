---
title: 自适应卡片概述
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 27c7d5ac7da3ae182667cbf8efa90d29f110d1d3
ms.sourcegitcommit: ef03c0eff3272a36cfa88daf99c4d57e4bae9599
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72042534"
---
# <a name="adaptive-cards-overview"></a>自适应卡片概述 

自适应卡片是一种开放的卡片交换格式，可以让开发人员通过常见且一致的方式交换 UI 内容。

<video controls width="100%" poster="./content/videoposter.png">
    <source src="https://adaptivecardsblob.blob.core.windows.net/assets/AdaptiveCardsOverviewVideo.mp4" type="video/mp4">
</video>

## <a name="how-they-work"></a>工作原理

[**卡片作者**](authoring-cards/getting-started.md)一文将卡片内容描述为简单的 JSON 对象。 该内容随后可以在[**主机应用程序**](rendering-cards/getting-started.md)中以本机方式呈现，自动适应主机的外观。

例如，Contoso 机器人可以通过 Bot Framework 创作一张自适应卡片。将该卡片发送到 Skype 时，它看起来就像一张 Skype 卡片。 将这个相同的有效负载发送到 Microsoft Teams 时，它看起来就像 Microsoft Teams。 当更多的主机应用开始支持自适应卡片时，这个相同的有效负载会自动在这些应用程序中启用，但其外观就像完全是该应用原生的一样。

这有利于用户，因为他们会感到一切都很熟悉。 这有利于主机应用，因为它们可以控制用户体验。 这有利于卡片作者，因为他们不需任何额外的工作就可以推广其内容。

## <a name="goals"></a>目标 

自适应卡片的目标是：

* **可移植** - 移植到任何应用、设备和 UI 框架
* **开放** - 库和架构采取开源和共享的形式
* **低成本** - 易于定义，易于使用
* **表达性强** - 其目标是开发人员希望生成的长尾内容
* **纯声明性** - 不需要代码，也不允许使用代码
* **自动调整样式** - 根据主机应用程序 UX 和品牌准则进行调整

## <a name="for-card-authors"></a>面向卡片作者
对卡片作者来说，自适应卡片具有以下优点：

* **一种架构** - 只有一种格式，可以将创建卡片的成本降至最低，同时又可以尽量扩大能够使用该卡片的场所。
* **更丰富的表达** - 内容可以与你要表达的意思更接近，因为你的表达方式更丰富。
* **广泛的覆盖面** - 内容将适用于更广泛的应用程序集，而你不需学习新架构。
* **输入控件** - 卡片可以包含输入控件，用于从查看卡片的用户处收集信息。
* **更好的工具** - 开放的卡片生态系统意味着更好的可供所有人共享的工具。

## <a name="for-experience-owners"></a>面向体验所有者
如果你是应用开发人员，希望探索第三方内容的生态系统，则会喜欢自适应卡片，原因在于：

* **一致的用户体验** - 可以保证为用户提供一致的体验，因为你拥有所呈现卡片的样式。
* **本机性能** - 可以获得本机性能，因为它直接以 UI 框架为目标。
* **安全** - 内容在安全的有效负载中传送，因此不需将 UI 框架开放给原始的标记和脚本。
* **易于实现** - 获得现成的库以后，即可将其轻松集成到支持的任何平台上。 
* **免费文档** - 可以节省时间，因为不需创造、实现和记录专有架构。
* **共享工具** - 可以节省时间，因为不需创建自定义工具。

## <a name="core-design-principles"></a>核心设计原则 

自适应卡片遵循一系列[指导原则](resources/principles.md)，这些原则可以让设计保持正轨。 

### <a name="semantic-instead-of-pixel-perfect"></a>追求语义价值而非像素完美
我们一直致力于追求语义价值和概念，而不是单纯的像素完美布局。 语义表达式的示例显示在颜色、大小和元素中，例如 FactSet 和 ImageSet。 这样主机应用程序就可以在实际外观方面进行更好的决策。

### <a name="card-authors-own-the-content-host-app-owns-the-look-and-feel"></a>卡片作者拥有内容，主机应用拥有外观
卡片作者拥有其所要表达的内容，而显示内容的应用程序则拥有卡片在应用程序上下文中呈现的外观。

### <a name="keep-it-simple-but-expressive"></a>在保持简单的同时增强表达能力
我们希望自适应卡片表达能力强且通用，但我们并不想要构建一个 UI 框架。  我们的目标是创建一个“具有足够表达力”的中间层，这与 Markdown 是相同的，后者对于文档来说具有足够的表达力。

Markdown 的目标也是在保持简单的同时增强表达能力，可以轻松地对文档内容进行一致的描述。  我们相信，自适应卡片同样可以通过简单但表达力强的方式来描述卡片内容。

### <a name="when-in-doubt-keep-it-out"></a>疑则不用
如果对某样功能没有把握，可以稍后添加相关内容，不必忍受其中的错误。 如果我们发现自己在争论是否应添加某项内容，则可以选择暂时不用它。通常情况下，与其使用我们不希望支持的旧属性，不如以后再添加相关内容。


## <a name="build-2019-session"></a>Build 2019 会议

Microsoft Build 大会上的以下会议在各种用例中展示了自适应卡片。 

<iframe width="560" height="315" src="https://www.youtube.com/embed/wT1yFr_j6IM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
