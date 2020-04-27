---
title: 扩展性
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 423971a4beec7a8bfce48ecdf530ffea4dbb54e7
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "77454950"
---
# <a name="extensibility"></a><span data-ttu-id="401b3-102">扩展性</span><span class="sxs-lookup"><span data-stu-id="401b3-102">Extensibility</span></span>

<span data-ttu-id="401b3-103">每个 SDK 都允许你重写任何元素的呈现，甚至允许你为自己定义的全新元素添加支持。</span><span class="sxs-lookup"><span data-stu-id="401b3-103">Each SDK allows you to override the rendering of any element, or even add support for entirely new elements that you define.</span></span>  <span data-ttu-id="401b3-104">例如，可以更改 `Input.Date` 呈现器，以便在仍然保留呈现器的其余输出的情况下，发出你自己的自定义控制。</span><span class="sxs-lookup"><span data-stu-id="401b3-104">For example, you can change the `Input.Date` renderer to emit your own custom control while still retaining the rest of the output of the renderer.</span></span> <span data-ttu-id="401b3-105">也可添加对你定义的自定义 `Rating` 元素的支持。</span><span class="sxs-lookup"><span data-stu-id="401b3-105">Or you can add support for a custom `Rating` element to you define.</span></span>

<span data-ttu-id="401b3-106">如需示例代码，请展开左侧的 **SDK** 节点，然后单击“呈现卡片”   -> “要使用的 SDK”   ->   “可扩展性”</span><span class="sxs-lookup"><span data-stu-id="401b3-106">For example code, please expand the **SDK** node on the left -> **Rendering Cards** -> **the SDK you'd like to use** -> **Extensibility**</span></span>
