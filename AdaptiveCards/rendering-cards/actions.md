---
title: 操作
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 42ba1ca4ba2ecd508bdee2f04061293d48349aab
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553369"
---
# <a name="actions"></a><span data-ttu-id="882d2-102">操作</span><span class="sxs-lookup"><span data-stu-id="882d2-102">Actions</span></span>

<span data-ttu-id="882d2-103">默认情况下，操作将呈现为在卡上的按钮，但这取决于您的应用程序以使其按预期工作。</span><span class="sxs-lookup"><span data-stu-id="882d2-103">By default, the actions will render as buttons on the card, but it's up to your app to make them behave as you expect.</span></span> <span data-ttu-id="882d2-104">每个 SDK 有相当于`OnAction`必须处理的事件。</span><span class="sxs-lookup"><span data-stu-id="882d2-104">Each SDK has the equivalent of an `OnAction` event that you must handle.</span></span>

* <span data-ttu-id="882d2-105">**Action.OpenUrl** -打开指定`url`。</span><span class="sxs-lookup"><span data-stu-id="882d2-105">**Action.OpenUrl** - open the specified `url`.</span></span>  
* <span data-ttu-id="882d2-106">**Action.Submit** -提取的提交结果，并将其发送到源。</span><span class="sxs-lookup"><span data-stu-id="882d2-106">**Action.Submit** - take the result of the submit and send it to the source.</span></span> <span data-ttu-id="882d2-107">如何向的源发送它是卡片的完全取决于您。</span><span class="sxs-lookup"><span data-stu-id="882d2-107">How you send it to the source of the card is entirely up to you.</span></span>
* <span data-ttu-id="882d2-108">**Action.ShowCard** -调用一个对话框，并将子卡呈现到该对话框。</span><span class="sxs-lookup"><span data-stu-id="882d2-108">**Action.ShowCard** - invokes a dialog and renders the sub-card into that dialog.</span></span> <span data-ttu-id="882d2-109">请注意，只需处理此 if`ShowCardActionMode`设置为`popup`。</span><span class="sxs-lookup"><span data-stu-id="882d2-109">Note that you only need to handle this if `ShowCardActionMode` is set to `popup`.</span></span>