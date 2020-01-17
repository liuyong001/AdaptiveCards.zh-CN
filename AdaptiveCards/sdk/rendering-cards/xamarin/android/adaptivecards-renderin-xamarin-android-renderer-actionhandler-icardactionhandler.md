---
title: ICardActionHandler 类-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 8b526ccb66be3a261384d6c4f68a850558e2549e
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76146151"
---
# <a name="icardactionhandler"></a>ICardActionHandler

```csharp
public interface ICardActionHandler : IJavaObject 
```

**命名空间**
```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.Renderer.ActionHandler
```

### <a name="summary"></a>摘要

| 公共方法 | |
| --- | ---- |
| ```abstract void``` | [```OnAction (BaseActionElement p0, RenderedAdaptiveCard p1)```](#onaction) |
| ```abstract void``` | [```OnMediaPlay (BaseCardElement p0, RenderedAdaptiveCard p1)```](#onmediaplay) |
| ```abstract void``` | [```OnMediaStop (BaseCardElement p0, RenderedAdaptiveCard p1)```](#onmediastop) |

## <a name="public-methods"></a>公共方法
--- 
### <a id="onaction"></a>OnAction
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
void OnAction (BaseActionElement p0, RenderedAdaptiveCard p1)
```

当单击 OpenUrlAction、SubmitAction 或 ShowCardAction （如果未内联）时调用的侦听器。

| 参数 | |
| --- | --- |
| p0 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseActionElement``` |
| p1 | [```AdaptiveCards.Rendering.Xamarin.Android.Renderer.RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md) |

#### <a name="sample"></a>示例

```csharp
public class MyCardActionHandler : ICardActionHandler
{

    public void OnAction(BaseActionElement element, RenderedAdaptiveCard renderedCard)
    {
        ActionType actionType = element.ElementType;
        if (actionType == ActionType.Submit)
        {
            var inputs = renderedCard.Inputs;
            string inputValues = string.Empty;
            foreach (var inputString in inputs)
            {
                inputValues += $"{{{inputString.Key} : {inputString.Value}}}\n";
            }
            submitData(inputValues);
        }
        else if (actionType == ActionType.ShowCard)
        {
            var showcardAction = ShowCardAction.Dynamic_cast(element);
            showCard(showcardAction.Card)
        }
        else if (actionType == ActionType.OpenUrl)
        {
            var openUrlAction = OpenUrlAction.Dynamic_cast(element);
            openUrl(openUrlAction.Url);
        }
    }
}
```

---
### <a id="onmediaplay"></a>OnMediaPlay
<p style='text-align:right'>在版本0.1 中添加</p>

```csharp
void OnMediaPlay (BaseCardElement p0, RenderedAdaptiveCard p1)
```

媒体元素开始播放时调用的侦听器。

| 参数 | |
| --- | --- |
| p0 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElement``` |
| p1 | [```AdaptiveCards.Rendering.Xamarin.Android.Renderer.RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md) |

#### <a name="sample"></a>示例

```csharp
public class MyCardActionHandler : ICardActionHandler
{
    public void OnMediaPlay(BaseCardElement element, RenderedAdaptiveCard renderedCard)
    {
    }
}
```

--- 

### <a id="onmediastop"></a>OnMediaStop
<p style='text-align:right'>在版本0.1 中添加</p>

```csharp
void OnMediaStop (BaseCardElement p0, RenderedAdaptiveCard p1)
```

媒体元素停止播放时调用的侦听器。

| 参数 | |
| --- | --- |
| p0 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElement``` |
| p1 | [```AdaptiveCards.Rendering.Xamarin.Android.Renderer.RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md) |

#### <a name="sample"></a>示例

```csharp
public class MyCardActionHandler : ICardActionHandler
{
    public void OnMediaStop(BaseCardElement element, RenderedAdaptiveCard renderedCard)
    {
    }
}
```