---
title: “操作”
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 34283b52f0c4902c71ea33634676832c7dfec5c9
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454940"
---
# <a name="actions"></a><span data-ttu-id="6c7c2-102">“操作”</span><span class="sxs-lookup"><span data-stu-id="6c7c2-102">Actions</span></span>

<span data-ttu-id="6c7c2-103">默认情况下，操作在卡上会呈现为按钮，但应用可以根据你的需要来定义操作的行为。</span><span class="sxs-lookup"><span data-stu-id="6c7c2-103">By default, the actions will render as buttons on the card, but it's up to your app to make them behave as you expect.</span></span> <span data-ttu-id="6c7c2-104">每个 SDK 都有 `OnAction` 事件的等效项，必须对其进行处理。</span><span class="sxs-lookup"><span data-stu-id="6c7c2-104">Each SDK has the equivalent of an `OnAction` event that you must handle.</span></span>

* <span data-ttu-id="6c7c2-105">**Action.OpenUrl** - 打开指定的 `url`。</span><span class="sxs-lookup"><span data-stu-id="6c7c2-105">**Action.OpenUrl** - open the specified `url`.</span></span>  
* <span data-ttu-id="6c7c2-106">**Action.Submit** - 获取提交的结果并将其发送到源。</span><span class="sxs-lookup"><span data-stu-id="6c7c2-106">**Action.Submit** - take the result of the submit and send it to the source.</span></span> <span data-ttu-id="6c7c2-107">如何将其发送到卡片的源完全取决于你自己。</span><span class="sxs-lookup"><span data-stu-id="6c7c2-107">How you send it to the source of the card is entirely up to you.</span></span>
* <span data-ttu-id="6c7c2-108">**Action.ShowCard** - 调用某个对话并将子卡呈现到该对话中。</span><span class="sxs-lookup"><span data-stu-id="6c7c2-108">**Action.ShowCard** - invokes a dialog and renders the sub-card into that dialog.</span></span> <span data-ttu-id="6c7c2-109">请注意，只有在 `ShowCardActionMode` 设置为 `popup` 的情况下，才需要对此进行处理。</span><span class="sxs-lookup"><span data-stu-id="6c7c2-109">Note that you only need to handle this if `ShowCardActionMode` is set to `popup`.</span></span>