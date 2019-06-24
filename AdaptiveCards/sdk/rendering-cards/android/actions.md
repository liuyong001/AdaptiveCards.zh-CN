---
title: 操作 - Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: e21c03e069e7ab29dd7d2724d49a2d439c67e5a1
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67134259"
---
# <a name="actions---android"></a><span data-ttu-id="b8bea-102">操作 - Android</span><span class="sxs-lookup"><span data-stu-id="b8bea-102">Actions - Android</span></span>

<span data-ttu-id="b8bea-103">执行卡片操作时，会调用已传递给呈现调用（用于实现 ICardActionHandler 接口）的类。</span><span class="sxs-lookup"><span data-stu-id="b8bea-103">When a cards action is executed, the class that was passed to the render call that implements the ICardActionHandler interface gets invoked.</span></span> <span data-ttu-id="b8bea-104">下面介绍如何定义操作处理程序：</span><span class="sxs-lookup"><span data-stu-id="b8bea-104">Here is how to define your action handler:</span></span>

```java
public class ActionHandler implements ICardActionHandler
{
    @Override
    public void onAction(BaseActionElement actionElement, RenderedAdaptiveCard renderedCard)
    {
        ActionType actionType = actionElement.GetElementType();
        if (actionType == ActionType.Submit)
        {
            onSubmit(actionElement, renderedCard);
        }
        else if (actionType == ActionType.ShowCard)
        {
            onShowCard(actionElement);
        }
        else if (actionType == ActionType.OpenUrl)
        {
            onOpenUrl(actionElement);
        }
        else if (actionType == ActionType.Custom)
        {
            //Handle activation of custom actions
            ...
        }
    }

    private void onSubmit(BaseActionElement actionElement, RenderedAdaptiveCard renderedAdaptiveCard)
    {
        SubmitAction submitAction = null;
        if (actionElement instanceof SubmitAction)
        {
            submitAction = (SubmitAction) actionElement;
        }
        else if ((submitAction = SubmitAction.dynamic_cast(actionElement)) == null)
        {
            throw new InternalError("Unable to convert BaseActionElement to ShowCardAction object model.");
        }

        String data = submitAction.GetDataJson();
        Map<String, String> keyValueMap = renderedAdaptiveCard.getInputs();
        if (!data.isEmpty())
        {
            try
            {
                JSONObject object = new JSONObject(data);
                showToast("Submit data: " + object.toString() + "\nInput: " + keyValueMap.toString(), Toast.LENGTH_LONG);
            }
            catch (JSONException e)
            {
                showToast(e.toString(), Toast.LENGTH_LONG);
            }
        }
        else
        {
            showToast("Submit input: " + keyValueMap.toString(), Toast.LENGTH_LONG);
        }
    }

    private void onShowCard(BaseActionElement actionElement)
    {
        ShowCardAction showCardAction = null;
        if (actionElement instanceof ShowCardAction)
        {
            showCardAction = (ShowCardAction) actionElement;
        }
        else if ((showCardAction = ShowCardAction.dynamic_cast(actionElement)) == null)
        {
            throw new InternalError("Unable to convert BaseActionElement to ShowCardAction object model.");
        }

        //Get the card from show card and create a view
        RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, showCardAction.GetCard(), cardActionHandler, hostConfig);

        ViewGroup viewGroup = (ViewGroup) renderedCard.getView();
        ...
    }

    private void onOpenUrl(BaseActionElement actionElement)
    {
        OpenUrlAction openUrlAction = null;
        if (actionElement instanceof ShowCardAction)
        {
            openUrlAction = (OpenUrlAction) actionElement;
        }
        else if ((openUrlAction = OpenUrlAction.dynamic_cast(actionElement)) == null)
        {
            throw new InternalError("Unable to convert BaseActionElement to ShowCardAction object model.");
        }

        Intent browserIntent = new Intent(Intent.ACTION_VIEW, Uri.parse(openUrlAction.GetUrl()));
        this.startActivity(browserIntent);
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="b8bea-105">**v1.1 的重大更改**</span><span class="sxs-lookup"><span data-stu-id="b8bea-105">**Breaking changes for v1.1**</span></span>
> 
> 1. <span data-ttu-id="b8bea-106">包括在此版本中的媒体元素要求通过用于实现 ICardActionHandler 的类来实现两个新方法，这两个方法是</span><span class="sxs-lookup"><span data-stu-id="b8bea-106">The media element included in this version requires two new methods to be implemented by the classes that implement ICardActionHandler, these methods are</span></span>
>
> ```java
> public void onMediaPlay(BaseCardElement mediaElement, RenderedAdaptiveCard renderedAdaptiveCard)
> public void onMediaStop(BaseCardElement mediaElement, RenderedAdaptiveCard renderedAdaptiveCard)
> ```
>
> <span data-ttu-id="b8bea-107">在任何媒体元素中首次按下播放按钮时会调用 onMediaPlay，当媒体播放完毕时会调用 onMediaStop</span><span class="sxs-lookup"><span data-stu-id="b8bea-107">onMediaPlay is invoked when the play button is pressed for the first time in any media element, meanwhile onMediaStop is invoked when the media reaches it's end</span></span>
