---
title: AdaptiveCard 类-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 0f64bf635023271d8b40bf55fce079300aae7652
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76146081"
---
# <a name="adaptivecard"></a><span data-ttu-id="4d75a-102">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="4d75a-102">AdaptiveCard</span></span>

```csharp
public class AdaptiveCard : Java.Lang.Object 
```

<span data-ttu-id="4d75a-103">**命名空间**</span><span class="sxs-lookup"><span data-stu-id="4d75a-103">**Namespace**</span></span>

```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.ObjectModel
```

## <a name="summary"></a><span data-ttu-id="4d75a-104">摘要</span><span class="sxs-lookup"><span data-stu-id="4d75a-104">Summary</span></span>

| <span data-ttu-id="4d75a-105">属性</span><span class="sxs-lookup"><span data-stu-id="4d75a-105">Attributes</span></span> | |
| ---- | --- |
| <span data-ttu-id="4d75a-106">“操作”</span><span class="sxs-lookup"><span data-stu-id="4d75a-106">Actions</span></span> | <span data-ttu-id="4d75a-107">要在卡片的操作栏中显示的操作。</span><span class="sxs-lookup"><span data-stu-id="4d75a-107">The Actions to show in the card’s action bar.</span></span> |
| <span data-ttu-id="4d75a-108">BackgroundImage</span><span class="sxs-lookup"><span data-stu-id="4d75a-108">BackgroundImage</span></span> | <span data-ttu-id="4d75a-109">指定卡的背景图像。</span><span class="sxs-lookup"><span data-stu-id="4d75a-109">Specifies the background image of the card.</span></span> |
| <span data-ttu-id="4d75a-110">正文</span><span class="sxs-lookup"><span data-stu-id="4d75a-110">Body</span></span> | <span data-ttu-id="4d75a-111">要在主要卡区域显示的卡片元素。</span><span class="sxs-lookup"><span data-stu-id="4d75a-111">The card elements to show in the primary card region.</span></span> |
| <span data-ttu-id="4d75a-112">{2&gt;ElementType&lt;2}</span><span class="sxs-lookup"><span data-stu-id="4d75a-112">ElementType</span></span> | <span data-ttu-id="4d75a-113">必须为 "AdaptiveCard"。</span><span class="sxs-lookup"><span data-stu-id="4d75a-113">Must be "AdaptiveCard".</span></span> |
| <span data-ttu-id="4d75a-114">FallbackText</span><span class="sxs-lookup"><span data-stu-id="4d75a-114">FallbackText</span></span> | <span data-ttu-id="4d75a-115">当客户端不支持指定的版本时显示的文本（可能包含 markdown）。</span><span class="sxs-lookup"><span data-stu-id="4d75a-115">Text shown when the client doesn’t support the version specified (may contain markdown).</span></span> |
| <span data-ttu-id="4d75a-116">Height</span><span class="sxs-lookup"><span data-stu-id="4d75a-116">Height</span></span> | |
| <span data-ttu-id="4d75a-117">InputNecessityIndicators</span><span class="sxs-lookup"><span data-stu-id="4d75a-117">InputNecessityIndicators</span></span> | |
| <span data-ttu-id="4d75a-118">“语言”</span><span class="sxs-lookup"><span data-stu-id="4d75a-118">Language</span></span> | <span data-ttu-id="4d75a-119">卡中使用的 2-字母 ISO-639-1 语言。</span><span class="sxs-lookup"><span data-stu-id="4d75a-119">The 2-letter ISO-639-1 language used in the card.</span></span> <span data-ttu-id="4d75a-120">用于本地化所有日期/时间函数。</span><span class="sxs-lookup"><span data-stu-id="4d75a-120">Used to localize any date/time functions.</span></span> |
| <span data-ttu-id="4d75a-121">MinHeight</span><span class="sxs-lookup"><span data-stu-id="4d75a-121">MinHeight</span></span> | <span data-ttu-id="4d75a-122">指定卡的最小高度。</span><span class="sxs-lookup"><span data-stu-id="4d75a-122">Specifies the minimum height of the card.</span></span> |
| <span data-ttu-id="4d75a-123">SelectAction</span><span class="sxs-lookup"><span data-stu-id="4d75a-123">SelectAction</span></span> | <span data-ttu-id="4d75a-124">在点击或选择卡时将调用的操作。</span><span class="sxs-lookup"><span data-stu-id="4d75a-124">An Action that will be invoked when the card is tapped or selected.</span></span> <span data-ttu-id="4d75a-125">不支持 ShowCard。</span><span class="sxs-lookup"><span data-stu-id="4d75a-125">Action.ShowCard is not supported.</span></span> |
| <span data-ttu-id="4d75a-126">Speak</span><span class="sxs-lookup"><span data-stu-id="4d75a-126">Speak</span></span> | <span data-ttu-id="4d75a-127">指定应为此整个卡口述的内容。</span><span class="sxs-lookup"><span data-stu-id="4d75a-127">Specifies what should be spoken for this entire card.</span></span> <span data-ttu-id="4d75a-128">这是简单文本或 SSML 片段。</span><span class="sxs-lookup"><span data-stu-id="4d75a-128">This is simple text or SSML fragment.</span></span> |
| <span data-ttu-id="4d75a-129">“造型”</span><span class="sxs-lookup"><span data-stu-id="4d75a-129">Style</span></span> | |
| <span data-ttu-id="4d75a-130">版本</span><span class="sxs-lookup"><span data-stu-id="4d75a-130">Version</span></span> | <span data-ttu-id="4d75a-131">此卡所需的架构版本。</span><span class="sxs-lookup"><span data-stu-id="4d75a-131">Schema version that this card requires.</span></span> <span data-ttu-id="4d75a-132">如果客户端低于此版本，将呈现 fallbackText。</span><span class="sxs-lookup"><span data-stu-id="4d75a-132">If a client is lower than this version, the fallbackText will be rendered.</span></span> <span data-ttu-id="4d75a-133">注意： ShowCard 中的卡不需要版本。</span><span class="sxs-lookup"><span data-stu-id="4d75a-133">NOTE: Version is not required for cards within an Action.ShowCard.</span></span> <span data-ttu-id="4d75a-134">但是，它对于顶级卡是必需的。</span><span class="sxs-lookup"><span data-stu-id="4d75a-134">However, it is required for the top-level card.</span></span> |
| <span data-ttu-id="4d75a-135">System.windows.controls.control.verticalcontentalignment</span><span class="sxs-lookup"><span data-stu-id="4d75a-135">VerticalContentAlignment</span></span> | <span data-ttu-id="4d75a-136">定义内容应在容器中垂直对齐的方式。</span><span class="sxs-lookup"><span data-stu-id="4d75a-136">Defines how the content should be aligned vertically within the container.</span></span> <span data-ttu-id="4d75a-137">仅适用于固定高度的卡，或指定了 minHeight 的卡。</span><span class="sxs-lookup"><span data-stu-id="4d75a-137">Only relevant for fixed-height cards, or cards with a minHeight specified.</span></span> |

&nbsp;

<span data-ttu-id="4d75a-138">**公共构造函数**</span><span class="sxs-lookup"><span data-stu-id="4d75a-138">**Public Constructors**</span></span>

---

<a href="#ctor0"><div>
```csharp
AdaptiveCard(string version, string fallbackText, BackgroundImage backgroundImage, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight)
```
</div></a>

<a href="#ctor1"><div>
```csharp
AdaptiveCard(string version, string fallbackText, BackgroundImage backgroundImage, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight, BaseCardElementVector body, BaseActionElementVector actions)
```
</div></a>

<a href="#ctor2"><div>
```csharp
AdaptiveCard(string version, string fallbackText, string backgroundImageUrl, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight)
```
</div></a>

<a href="#ctor3"><div>
```csharp
AdaptiveCard(string version, string fallbackText, string backgroundImageUrl, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight, BaseCardElementVector body, BaseActionElementVector actions)
```
</div></a>

&nbsp;
| <span data-ttu-id="4d75a-139">公共方法</span><span class="sxs-lookup"><span data-stu-id="4d75a-139">Public methods</span></span> | |
| --- | ---- |
| ```static ParseResult``` | [```DeserializeFromString(string jsonString, string rendererVersion)```](#deserializefromstring0) |
| ```static ParseResult``` | [```DeserializeFromString(string jsonString, string rendererVersion, ParseContext context)```](#deserializefromstring1) |
| ```static AdaptiveCard``` | [```MakeFallbackTextCard(string fallbackText, string language, string speak)```](#makefallbacktextcard) |
| ```string``` | [```Serialize()```](#serialize) |
| ```JsonValue``` | [```SerializeToJsonValue()```](#serializetojsonvalue) |

&nbsp;
## <a name="public-constructors"></a><span data-ttu-id="4d75a-140">公共构造函数</span><span class="sxs-lookup"><span data-stu-id="4d75a-140">Public Constructors</span></span>
---

### <a id="ctor0"></a><span data-ttu-id="4d75a-141">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="4d75a-141">AdaptiveCard</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-142">在版本0.1 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-142">Added in version 0.1</span></span></p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    BackgroundImage backgroundImage, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment, 
                    HeightType height, 
                    long minHeight) 
```

| <span data-ttu-id="4d75a-143">参数</span><span class="sxs-lookup"><span data-stu-id="4d75a-143">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="4d75a-144">version</span><span class="sxs-lookup"><span data-stu-id="4d75a-144">version</span></span> | ```string``` |
| <span data-ttu-id="4d75a-145">fallbackText</span><span class="sxs-lookup"><span data-stu-id="4d75a-145">fallbackText</span></span> | ```string``` |
| <span data-ttu-id="4d75a-146">backgroundImage</span><span class="sxs-lookup"><span data-stu-id="4d75a-146">backgroundImage</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BackgroundImage``` |
| <span data-ttu-id="4d75a-147">样式</span><span class="sxs-lookup"><span data-stu-id="4d75a-147">style</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| <span data-ttu-id="4d75a-148">speak</span><span class="sxs-lookup"><span data-stu-id="4d75a-148">speak</span></span> | ```string``` |
| <span data-ttu-id="4d75a-149">language</span><span class="sxs-lookup"><span data-stu-id="4d75a-149">language</span></span> | ```string``` |
| <span data-ttu-id="4d75a-150">System.windows.controls.control.verticalcontentalignment</span><span class="sxs-lookup"><span data-stu-id="4d75a-150">verticalContentAlignment</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| <span data-ttu-id="4d75a-151">height</span><span class="sxs-lookup"><span data-stu-id="4d75a-151">height</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| <span data-ttu-id="4d75a-152">minHeight</span><span class="sxs-lookup"><span data-stu-id="4d75a-152">minHeight</span></span> | ```long``` |

&nbsp;&nbsp;

### <a id="ctor1"></a><span data-ttu-id="4d75a-153">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="4d75a-153">AdaptiveCard</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-154">在版本0.1 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-154">Added in version 0.1</span></span></p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    BackgroundImage backgroundImage, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment, 
                    HeightType height, 
                    long minHeight, 
                    BaseCardElementVector body, 
                    BaseActionElementVector actions)
```

| <span data-ttu-id="4d75a-155">参数</span><span class="sxs-lookup"><span data-stu-id="4d75a-155">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="4d75a-156">version</span><span class="sxs-lookup"><span data-stu-id="4d75a-156">version</span></span> | ```string``` |
| <span data-ttu-id="4d75a-157">fallbackText</span><span class="sxs-lookup"><span data-stu-id="4d75a-157">fallbackText</span></span> | ```string``` |
| <span data-ttu-id="4d75a-158">backgroundImage</span><span class="sxs-lookup"><span data-stu-id="4d75a-158">backgroundImage</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BackgroundImage``` |
| <span data-ttu-id="4d75a-159">样式</span><span class="sxs-lookup"><span data-stu-id="4d75a-159">style</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| <span data-ttu-id="4d75a-160">speak</span><span class="sxs-lookup"><span data-stu-id="4d75a-160">speak</span></span> | ```string``` |
| <span data-ttu-id="4d75a-161">language</span><span class="sxs-lookup"><span data-stu-id="4d75a-161">language</span></span> | ```string``` |
| <span data-ttu-id="4d75a-162">System.windows.controls.control.verticalcontentalignment</span><span class="sxs-lookup"><span data-stu-id="4d75a-162">verticalContentAlignment</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| <span data-ttu-id="4d75a-163">height</span><span class="sxs-lookup"><span data-stu-id="4d75a-163">height</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| <span data-ttu-id="4d75a-164">minHeight</span><span class="sxs-lookup"><span data-stu-id="4d75a-164">minHeight</span></span> | ```long``` |
| <span data-ttu-id="4d75a-165">正文</span><span class="sxs-lookup"><span data-stu-id="4d75a-165">body</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElementVector``` |
| <span data-ttu-id="4d75a-166">操作</span><span class="sxs-lookup"><span data-stu-id="4d75a-166">actions</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseActionElementVector``` |

&nbsp;&nbsp;

### <a id="ctor2"></a><span data-ttu-id="4d75a-167">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="4d75a-167">AdaptiveCard</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-168">在版本0.1 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-168">Added in version 0.1</span></span></p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    string backgroundImageUrl, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment,
                    HeightType height, 
                    long minHeight) 
```

| <span data-ttu-id="4d75a-169">参数</span><span class="sxs-lookup"><span data-stu-id="4d75a-169">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="4d75a-170">version</span><span class="sxs-lookup"><span data-stu-id="4d75a-170">version</span></span> | ```string``` |
| <span data-ttu-id="4d75a-171">fallbackText</span><span class="sxs-lookup"><span data-stu-id="4d75a-171">fallbackText</span></span> | ```string``` |
| <span data-ttu-id="4d75a-172">backgroundImage</span><span class="sxs-lookup"><span data-stu-id="4d75a-172">backgroundImage</span></span> | ```string``` |
| <span data-ttu-id="4d75a-173">样式</span><span class="sxs-lookup"><span data-stu-id="4d75a-173">style</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| <span data-ttu-id="4d75a-174">speak</span><span class="sxs-lookup"><span data-stu-id="4d75a-174">speak</span></span> | ```string``` |
| <span data-ttu-id="4d75a-175">language</span><span class="sxs-lookup"><span data-stu-id="4d75a-175">language</span></span> | ```string``` |
| <span data-ttu-id="4d75a-176">System.windows.controls.control.verticalcontentalignment</span><span class="sxs-lookup"><span data-stu-id="4d75a-176">verticalContentAlignment</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| <span data-ttu-id="4d75a-177">height</span><span class="sxs-lookup"><span data-stu-id="4d75a-177">height</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| <span data-ttu-id="4d75a-178">minHeight</span><span class="sxs-lookup"><span data-stu-id="4d75a-178">minHeight</span></span> | ```long``` |

&nbsp;&nbsp;

### <a id="ctor3"></a><span data-ttu-id="4d75a-179">AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="4d75a-179">AdaptiveCard</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-180">在版本0.1 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-180">Added in version 0.1</span></span></p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    string backgroundImageUrl, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment,
                    HeightType height, 
                    long minHeight, 
                    BaseCardElementVector body,
                    BaseActionElementVector actions)

```

| <span data-ttu-id="4d75a-181">参数</span><span class="sxs-lookup"><span data-stu-id="4d75a-181">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="4d75a-182">version</span><span class="sxs-lookup"><span data-stu-id="4d75a-182">version</span></span> | ```string``` |
| <span data-ttu-id="4d75a-183">fallbackText</span><span class="sxs-lookup"><span data-stu-id="4d75a-183">fallbackText</span></span> | ```string``` |
| <span data-ttu-id="4d75a-184">backgroundImage</span><span class="sxs-lookup"><span data-stu-id="4d75a-184">backgroundImage</span></span> | ```string``` |
| <span data-ttu-id="4d75a-185">样式</span><span class="sxs-lookup"><span data-stu-id="4d75a-185">style</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| <span data-ttu-id="4d75a-186">speak</span><span class="sxs-lookup"><span data-stu-id="4d75a-186">speak</span></span> | ```string``` |
| <span data-ttu-id="4d75a-187">language</span><span class="sxs-lookup"><span data-stu-id="4d75a-187">language</span></span> | ```string``` |
| <span data-ttu-id="4d75a-188">System.windows.controls.control.verticalcontentalignment</span><span class="sxs-lookup"><span data-stu-id="4d75a-188">verticalContentAlignment</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| <span data-ttu-id="4d75a-189">height</span><span class="sxs-lookup"><span data-stu-id="4d75a-189">height</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| <span data-ttu-id="4d75a-190">minHeight</span><span class="sxs-lookup"><span data-stu-id="4d75a-190">minHeight</span></span> | ```long``` |
| <span data-ttu-id="4d75a-191">正文</span><span class="sxs-lookup"><span data-stu-id="4d75a-191">body</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElementVector``` |
| <span data-ttu-id="4d75a-192">操作</span><span class="sxs-lookup"><span data-stu-id="4d75a-192">actions</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseActionElementVector``` |

&nbsp;

## <a name="public-methods"></a><span data-ttu-id="4d75a-193">公共方法</span><span class="sxs-lookup"><span data-stu-id="4d75a-193">Public Methods</span></span>
---
### <a id="deserializefromstring0"></a><span data-ttu-id="4d75a-194">DeserializeFromString</span><span class="sxs-lookup"><span data-stu-id="4d75a-194">DeserializeFromString</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-195">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-195">Added in version 0.1.0</span></span></p>

```csharp
public static ParseResult DeserializeFromString (string jsonString, string rendererVersion)
```

<span data-ttu-id="4d75a-196">反序列化给定的自适应卡作为指定呈现器版本的 json 字符串。</span><span class="sxs-lookup"><span data-stu-id="4d75a-196">Deserializes the given adaptive card as a json string for the specified renderer version.</span></span>

| <span data-ttu-id="4d75a-197">参数</span><span class="sxs-lookup"><span data-stu-id="4d75a-197">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="4d75a-198">jsonString</span><span class="sxs-lookup"><span data-stu-id="4d75a-198">jsonString</span></span> | ```string``` |
| <span data-ttu-id="4d75a-199">rendererVersion</span><span class="sxs-lookup"><span data-stu-id="4d75a-199">rendererVersion</span></span> | ```string``` |

| <span data-ttu-id="4d75a-200">Returns</span><span class="sxs-lookup"><span data-stu-id="4d75a-200">Returns</span></span> | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ParseResult``` | |

#### <a name="sample"></a><span data-ttu-id="4d75a-201">示例</span><span class="sxs-lookup"><span data-stu-id="4d75a-201">Sample</span></span>

```csharp
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.Version);
```

--- 
### <a id="deserializefromstring1"></a><span data-ttu-id="4d75a-202">DeserializeFromString</span><span class="sxs-lookup"><span data-stu-id="4d75a-202">DeserializeFromString</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-203">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-203">Added in version 0.1.0</span></span></p>

```csharp
public static ParseResult DeserializeFromString(string jsonString, string rendererVersion, ParseContext context)
```

<span data-ttu-id="4d75a-204">使用[ParseContext]()对象将给定的自适应卡反序列化为指定呈现器版本的 json 字符串，以处理自定义元素分析。</span><span class="sxs-lookup"><span data-stu-id="4d75a-204">Deserializes the given adaptive card as a json string for the specified renderer version using a [ParseContext]() object to handle custom element parsing.</span></span>

| <span data-ttu-id="4d75a-205">参数</span><span class="sxs-lookup"><span data-stu-id="4d75a-205">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="4d75a-206">jsonString</span><span class="sxs-lookup"><span data-stu-id="4d75a-206">jsonString</span></span> | ```string``` |
| <span data-ttu-id="4d75a-207">rendererVersion</span><span class="sxs-lookup"><span data-stu-id="4d75a-207">rendererVersion</span></span> | ```string``` |
| <span data-ttu-id="4d75a-208">context</span><span class="sxs-lookup"><span data-stu-id="4d75a-208">context</span></span> | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ParseContext``` |

| <span data-ttu-id="4d75a-209">Returns</span><span class="sxs-lookup"><span data-stu-id="4d75a-209">Returns</span></span> | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ParseResult``` | |

#### <a name="sample"></a><span data-ttu-id="4d75a-210">示例</span><span class="sxs-lookup"><span data-stu-id="4d75a-210">Sample</span></span>

```csharp
ParseContext parseContext = new ParseContext(elementParserRegistration, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.Version, parseContext);
```

---

### <a id="makefallbacktextcard"></a><span data-ttu-id="4d75a-211">MakeFallbackTextCard</span><span class="sxs-lookup"><span data-stu-id="4d75a-211">MakeFallbackTextCard</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-212">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-212">Added in version 0.1.0</span></span></p>

```csharp
public static AdaptiveCard MakeFallbackTextCard (string fallbackText, string language, string speak)
```

<span data-ttu-id="4d75a-213">反序列化给定的自适应卡作为指定呈现器版本的 json 字符串。</span><span class="sxs-lookup"><span data-stu-id="4d75a-213">Deserializes the given adaptive card as a json string for the specified renderer version.</span></span>

| <span data-ttu-id="4d75a-214">参数</span><span class="sxs-lookup"><span data-stu-id="4d75a-214">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="4d75a-215">fallbackText</span><span class="sxs-lookup"><span data-stu-id="4d75a-215">fallbackText</span></span> | ```string``` |
| <span data-ttu-id="4d75a-216">language</span><span class="sxs-lookup"><span data-stu-id="4d75a-216">language</span></span> | ```string``` |
| <span data-ttu-id="4d75a-217">speak</span><span class="sxs-lookup"><span data-stu-id="4d75a-217">speak</span></span> | ```string``` |

| <span data-ttu-id="4d75a-218">Returns</span><span class="sxs-lookup"><span data-stu-id="4d75a-218">Returns</span></span> | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.AdaptiveCard``` | <span data-ttu-id="4d75a-219">包含 unrendereable 卡的回退文本的自适应卡</span><span class="sxs-lookup"><span data-stu-id="4d75a-219">Adaptive card that contains the fallback text for an unrendereable card</span></span> |

#### <a name="sample"></a><span data-ttu-id="4d75a-220">示例</span><span class="sxs-lookup"><span data-stu-id="4d75a-220">Sample</span></span>

```csharp
AdaptiveCard adaptiveCard = AdaptiveCard.MakeFallbackTextCard("This card failed to render", "es", "Unrendereable card");
```

---

### <a id="serialize"></a><span data-ttu-id="4d75a-221">序列</span><span class="sxs-lookup"><span data-stu-id="4d75a-221">Serialize</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-222">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-222">Added in version 0.1.0</span></span></p>

```csharp
public string Serialize ()
```

<span data-ttu-id="4d75a-223">将自适应卡序列化为其 json 字符串格式。</span><span class="sxs-lookup"><span data-stu-id="4d75a-223">Serializes the adaptive card into it's json string form.</span></span>

| <span data-ttu-id="4d75a-224">Returns</span><span class="sxs-lookup"><span data-stu-id="4d75a-224">Returns</span></span> | |
| --- | --- |
| ```string``` | <span data-ttu-id="4d75a-225">作为 json 字符串的自适应卡</span><span class="sxs-lookup"><span data-stu-id="4d75a-225">Adaptive card as a json string</span></span> |

#### <a name="sample"></a><span data-ttu-id="4d75a-226">示例</span><span class="sxs-lookup"><span data-stu-id="4d75a-226">Sample</span></span>

```csharp
string jsonString = parseResult.AdaptiveCard.Serialize();
```

---

### <a id="serializetojsonvalue"></a><span data-ttu-id="4d75a-227">SerializeToJsonValue</span><span class="sxs-lookup"><span data-stu-id="4d75a-227">SerializeToJsonValue</span></span>
<p style='text-align:right'><span data-ttu-id="4d75a-228">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="4d75a-228">Added in version 0.1.0</span></span></p>

```csharp
public JsonValue SerializeToJsonValue ()
```

<span data-ttu-id="4d75a-229">将自适应卡序列化到 json 值对象中。</span><span class="sxs-lookup"><span data-stu-id="4d75a-229">Serializes the adaptive card into a json value object.</span></span>

| <span data-ttu-id="4d75a-230">Returns</span><span class="sxs-lookup"><span data-stu-id="4d75a-230">Returns</span></span> | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.JsonValue``` | |

#### <a name="sample"></a><span data-ttu-id="4d75a-231">示例</span><span class="sxs-lookup"><span data-stu-id="4d75a-231">Sample</span></span>

```csharp
JsonValue value = parseResult.AdaptiveCard.SerializeToJsonValue();
```