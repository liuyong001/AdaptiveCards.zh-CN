---
title: 操作-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 6175bd4dc0709cc808a92e42f1b87d9a5f74ba0c
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76146071"
---
# <a name="actions---xamarinandroid"></a><span data-ttu-id="403ac-102">操作-Xamarin</span><span class="sxs-lookup"><span data-stu-id="403ac-102">Actions - Xamarin.Android</span></span>

<span data-ttu-id="403ac-103">执行卡操作时，会调用传递给实现[```ICardActionHandler```](adaptivecards-renderin-xamarin-android-renderer-actionhandler-icardactionhandler.md)接口的呈现调用的类。</span><span class="sxs-lookup"><span data-stu-id="403ac-103">When a cards action is executed, the class that was passed to the render call that implements the [```ICardActionHandler```](adaptivecards-renderin-xamarin-android-renderer-actionhandler-icardactionhandler.md) interface gets invoked.</span></span> <span data-ttu-id="403ac-104">下面介绍如何定义操作处理程序：</span><span class="sxs-lookup"><span data-stu-id="403ac-104">Here is how to define your action handler:</span></span>

```csharp
using AdaptiveCards.Rendering.Xamarin.Android.ObjectModel;
using AdaptiveCards.Rendering.Xamarin.Android.Renderer.ActionHandler;

// ...

public class CardActionHandlerImpl : ICardActionHandler
{

    public void OnAction(BaseActionElement element, RenderedAdaptiveCard renderedCard)
    {
        ActionType actionType = element.ElementType;
        if (actionType == ActionType.Submit)
        {
            var submitAction = SubmitAction.Dynamic_cast(element);
            var data = submitAction.DataJson;
            Toast.MakeText(this, data + "\n" + inputValues, ToastLength.Short).Show();
        }
        else if (actionType == ActionType.ShowCard)
        {           
            showCard(card);
        }
        else if (actionType == ActionType.OpenUrl)
        {
            openUrl(url);
        }
    }

    public void OnMediaPlay(BaseCardElement element, RenderedAdaptiveCard renderedCard) { }

    public void OnMediaStop(BaseCardElement element, RenderedAdaptiveCard renderedCard) { }
}
```
