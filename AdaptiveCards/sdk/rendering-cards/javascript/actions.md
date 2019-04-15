---
title: 操作-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: bd80c45e791244c4c3a930f96a91b66512cfbbb5
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553109"
---
# <a name="actions---javascript"></a><span data-ttu-id="29664-102">操作-JavaScript</span><span class="sxs-lookup"><span data-stu-id="29664-102">Actions - JavaScript</span></span>

```js
// Set the adaptive card's event handlers. onExecuteAction is invoked
// whenever an action is clicked in the card
adaptiveCard.onExecuteAction = function(action) { alert("Ow!"); }
```