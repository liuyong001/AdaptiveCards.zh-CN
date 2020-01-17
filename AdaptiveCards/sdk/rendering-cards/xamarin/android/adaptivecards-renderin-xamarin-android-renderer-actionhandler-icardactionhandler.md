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
# <a name="icardactionhandler"></a><span data-ttu-id="1934f-102">ICardActionHandler</span><span class="sxs-lookup"><span data-stu-id="1934f-102">ICardActionHandler</span></span>

```csharp
public interface ICardActionHandler : IJavaObject 
```

<span data-ttu-id="1934f-103">**命名空间**</span><span class="sxs-lookup"><span data-stu-id="1934f-103">**Namespace**</span></span>
```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.Renderer.ActionHandler
```

### <a name="summary"></a><span data-ttu-id="1934f-104">摘要</span><span class="sxs-lookup"><span data-stu-id="1934f-104">Summary</span></span>

| <span data-ttu-id="1934f-105">公共方法</span><span class="sxs-lookup"><span data-stu-id="1934f-105">Public methods</span></span> | |
| --- | ---- |
| ```abstract void``` | [```OnAction (BaseActionElement p0, RenderedAdaptiveCard p1)```](#onaction) |
| ```abstract void``` | [```OnMediaPlay (BaseCardElement p0, RenderedAdaptiveCard p1)```](#onmediaplay) |
| ```abstract void``` | [```OnMediaStop (BaseCardElement p0, RenderedAdaptiveCard p1)```](#onmediastop) |

## <a name="public-methods"></a><span data-ttu-id="1934f-106">公共方法</span><span class="sxs-lookup"><span data-stu-id="1934f-106">Public Methods</span></span>
--- 
### <a id="onaction"></a><span data-ttu-id="1934f-107">OnAction</span><span class="sxs-lookup"><span data-stu-id="1934f-107">OnAction</span></span>
<p style='text-align:right'><span data-ttu-id="1934f-108">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="1934f-108">Added in version 0.1.0</span></span></p>

```csharp
void OnAction (BaseActionElement p0, RenderedAdaptiveCard p1)
```

<span data-ttu-id="1934f-109">当单击 OpenUrlAction、SubmitAction 或 ShowCardAction （如果未内联）时调用的侦听器。</span><span class="sxs-lookup"><span data-stu-id="1934f-109">Listener called when a OpenUrlAction, SubmitAction or ShowCardAction (if not inline) are clicked.</span></span>

| <span data-ttu-id="1934f-110">参数</span><span class="sxs-lookup"><span data-stu-id="1934f-110">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="1934f-111">p0</span><span class="sxs-lookup"><span data-stu-id="1934f-111">p0</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseActionElement``` |
| <span data-ttu-id="1934f-112">p1</span><span class="sxs-lookup"><span data-stu-id="1934f-112">p1</span></span> | [```AdaptiveCards.Rendering.Xamarin.Android.Renderer.RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md) |

#### <a name="sample"></a><span data-ttu-id="1934f-113">示例</span><span class="sxs-lookup"><span data-stu-id="1934f-113">Sample</span></span>

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
### <a id="onmediaplay"></a><span data-ttu-id="1934f-114">OnMediaPlay</span><span class="sxs-lookup"><span data-stu-id="1934f-114">OnMediaPlay</span></span>
<p style='text-align:right'><span data-ttu-id="1934f-115">在版本0.1 中添加</span><span class="sxs-lookup"><span data-stu-id="1934f-115">Added in version 0.1</span></span></p>

```csharp
void OnMediaPlay (BaseCardElement p0, RenderedAdaptiveCard p1)
```

<span data-ttu-id="1934f-116">媒体元素开始播放时调用的侦听器。</span><span class="sxs-lookup"><span data-stu-id="1934f-116">Listener called when the media element starts playing.</span></span>

| <span data-ttu-id="1934f-117">参数</span><span class="sxs-lookup"><span data-stu-id="1934f-117">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="1934f-118">p0</span><span class="sxs-lookup"><span data-stu-id="1934f-118">p0</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElement``` |
| <span data-ttu-id="1934f-119">p1</span><span class="sxs-lookup"><span data-stu-id="1934f-119">p1</span></span> | [```AdaptiveCards.Rendering.Xamarin.Android.Renderer.RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md) |

#### <a name="sample"></a><span data-ttu-id="1934f-120">示例</span><span class="sxs-lookup"><span data-stu-id="1934f-120">Sample</span></span>

```csharp
public class MyCardActionHandler : ICardActionHandler
{
    public void OnMediaPlay(BaseCardElement element, RenderedAdaptiveCard renderedCard)
    {
    }
}
```

--- 

### <a id="onmediastop"></a><span data-ttu-id="1934f-121">OnMediaStop</span><span class="sxs-lookup"><span data-stu-id="1934f-121">OnMediaStop</span></span>
<p style='text-align:right'><span data-ttu-id="1934f-122">在版本0.1 中添加</span><span class="sxs-lookup"><span data-stu-id="1934f-122">Added in version 0.1</span></span></p>

```csharp
void OnMediaStop (BaseCardElement p0, RenderedAdaptiveCard p1)
```

<span data-ttu-id="1934f-123">媒体元素停止播放时调用的侦听器。</span><span class="sxs-lookup"><span data-stu-id="1934f-123">Listener called when the media element stops playing.</span></span>

| <span data-ttu-id="1934f-124">参数</span><span class="sxs-lookup"><span data-stu-id="1934f-124">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="1934f-125">p0</span><span class="sxs-lookup"><span data-stu-id="1934f-125">p0</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElement``` |
| <span data-ttu-id="1934f-126">p1</span><span class="sxs-lookup"><span data-stu-id="1934f-126">p1</span></span> | [```AdaptiveCards.Rendering.Xamarin.Android.Renderer.RenderedAdaptiveCard```](adaptivecards-rendering-xamarin-android-renderer-renderedadaptivecard.md) |

#### <a name="sample"></a><span data-ttu-id="1934f-127">示例</span><span class="sxs-lookup"><span data-stu-id="1934f-127">Sample</span></span>

```csharp
public class MyCardActionHandler : ICardActionHandler
{
    public void OnMediaStop(BaseCardElement element, RenderedAdaptiveCard renderedCard)
    {
    }
}
```