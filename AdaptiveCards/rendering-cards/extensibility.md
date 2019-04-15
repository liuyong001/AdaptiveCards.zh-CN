---
title: 扩展性
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 9359db59201d3ddb27f7cb31bdf22985b73d29d1
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552569"
---
# <a name="extensibility"></a><span data-ttu-id="835eb-102">扩展性</span><span class="sxs-lookup"><span data-stu-id="835eb-102">Extensibility</span></span>

<span data-ttu-id="835eb-103">每个 SDK，可重写的呈现任何元素，或者甚至添加对您定义的整个新元素的支持。</span><span class="sxs-lookup"><span data-stu-id="835eb-103">Each SDK allows you to override the rendering of any element, or even add support for entirely new elements that you define.</span></span>  <span data-ttu-id="835eb-104">例如，可以更改`Input.Date`呈现器仍保留的呈现器输出的其余部分的同时发出自定义控件。</span><span class="sxs-lookup"><span data-stu-id="835eb-104">For example, you can change the `Input.Date` renderer to emit your own custom control while still retaining the rest of the output of the renderer.</span></span> <span data-ttu-id="835eb-105">也可以添加对自定义支持`Rating`给您的元素定义。</span><span class="sxs-lookup"><span data-stu-id="835eb-105">Or you can add support for a custom `Rating` element to you define.</span></span>