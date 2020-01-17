---
title: RenderedAdaptiveCard 类-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 608b28638ce6ed0a218cfc8dbbe73f22de1ab8cb
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145991"
---
# <a name="renderedadaptivecard"></a><span data-ttu-id="05e5b-102">RenderedAdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="05e5b-102">RenderedAdaptiveCard</span></span>

```csharp
public class RenderedAdaptiveCard : Java.Lang.Object
```

<span data-ttu-id="05e5b-103">**命名空间**</span><span class="sxs-lookup"><span data-stu-id="05e5b-103">**Namespace**</span></span>

```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.Renderer
```

### <a name="summary"></a><span data-ttu-id="05e5b-104">摘要</span><span class="sxs-lookup"><span data-stu-id="05e5b-104">Summary</span></span>

| <span data-ttu-id="05e5b-105">属性</span><span class="sxs-lookup"><span data-stu-id="05e5b-105">Attributes</span></span> | |
| ---- | --- |
| <span data-ttu-id="05e5b-106">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="05e5b-106">AdaptiveCard</span></span> | <span data-ttu-id="05e5b-107">呈现的自适应卡的逻辑表示形式。</span><span class="sxs-lookup"><span data-stu-id="05e5b-107">Logical representation of the rendered adaptive card.</span></span> |
| <span data-ttu-id="05e5b-108">输入</span><span class="sxs-lookup"><span data-stu-id="05e5b-108">Inputs</span></span> | <span data-ttu-id="05e5b-109">输入元素的字典和用户添加的信息。</span><span class="sxs-lookup"><span data-stu-id="05e5b-109">Dictionary of input element and information added by the user.</span></span> |
| <span data-ttu-id="05e5b-110">“查看”</span><span class="sxs-lookup"><span data-stu-id="05e5b-110">View</span></span> | <span data-ttu-id="05e5b-111">呈现过程的视觉效果。</span><span class="sxs-lookup"><span data-stu-id="05e5b-111">Visual result from the rendering process.</span></span> |
| <span data-ttu-id="05e5b-112">警告</span><span class="sxs-lookup"><span data-stu-id="05e5b-112">Warnings</span></span> | <span data-ttu-id="05e5b-113">呈现过程中生成的警告的列表。</span><span class="sxs-lookup"><span data-stu-id="05e5b-113">List of warnings produced from the rendering process.</span></span> |

&nbsp;

| <span data-ttu-id="05e5b-114">公共方法</span><span class="sxs-lookup"><span data-stu-id="05e5b-114">Public methods</span></span> | |
| --- | ---- |
| ```void``` | [```AddWarning AdaptiveCards.Rendering.Xamarin.Android.Renderer.AdaptiveWarning warning)```](#addwarning) |

## <a name="public-methods"></a><span data-ttu-id="05e5b-115">公共方法</span><span class="sxs-lookup"><span data-stu-id="05e5b-115">Public Methods</span></span>

---

### <a id="addwarning"></a><span data-ttu-id="05e5b-116">AddWarning</span><span class="sxs-lookup"><span data-stu-id="05e5b-116">AddWarning</span></span>
<p style='text-align:right'><span data-ttu-id="05e5b-117">在版本0.1 中添加</span><span class="sxs-lookup"><span data-stu-id="05e5b-117">Added in version 0.1</span></span></p>

```csharp
public void AddWarning (AdaptiveWarning warning)

```

<span data-ttu-id="05e5b-118">向警告列表添加警告。</span><span class="sxs-lookup"><span data-stu-id="05e5b-118">Adds a warning to the warning list.</span></span>

| <span data-ttu-id="05e5b-119">参数</span><span class="sxs-lookup"><span data-stu-id="05e5b-119">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="05e5b-120">警告</span><span class="sxs-lookup"><span data-stu-id="05e5b-120">warning</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.Renderer.AdaptiveWarning``` |
