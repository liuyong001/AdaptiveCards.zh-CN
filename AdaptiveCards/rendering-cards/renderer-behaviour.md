---
title: 呈现器行为准则
author: manujai
ms.openlocfilehash: e0daa8eb57cc423fa1d4fc48c6d71faf16013efd
ms.sourcegitcommit: 0ed81e04d8cdcf8f8bf6f854edf53b7eb9f67d2a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/16/2021
ms.locfileid: "100532679"
---
# <a name="adaptive-card-renderer-behaviour-guideline"></a><span data-ttu-id="de316-102">自适应卡片呈现器行为准则</span><span class="sxs-lookup"><span data-stu-id="de316-102">Adaptive Card Renderer Behaviour Guideline</span></span>

<span data-ttu-id="de316-103">以下规范介绍了在实现与分析卡片元素之间的关系有关的呈现器行为时要遵循的设计准则。</span><span class="sxs-lookup"><span data-stu-id="de316-103">The following specification describes the design guideline to be followed when implementing the behaviour of a renderer with respect to parsing the relationship between the card elements.</span></span> 
> [!IMPORTANT]
> 
> <span data-ttu-id="de316-104">此内容尚未完成。</span><span class="sxs-lookup"><span data-stu-id="de316-104">This content is not finished yet.</span></span> <span data-ttu-id="de316-105">请稍后再回来查看。</span><span class="sxs-lookup"><span data-stu-id="de316-105">Check back shortly.</span></span>


## <a name="behaviours"></a><span data-ttu-id="de316-106">行为</span><span class="sxs-lookup"><span data-stu-id="de316-106">Behaviours</span></span> 

<span data-ttu-id="de316-107">在呈现与本文档中提到的特性相关的卡片元素时，呈现器必须注意以下行为。</span><span class="sxs-lookup"><span data-stu-id="de316-107">The Renderer **MUST** take care to the following behaviours when rendering card elements with respect to the attributes mentioned in this doc.</span></span> 

1. <span data-ttu-id="de316-108">**约束**</span><span class="sxs-lookup"><span data-stu-id="de316-108">**Constraints**</span></span>
2. <span data-ttu-id="de316-109">图像大小</span><span class="sxs-lookup"><span data-stu-id="de316-109">**Image Size**</span></span>
3. <span data-ttu-id="de316-110">**Action.Submit**</span><span class="sxs-lookup"><span data-stu-id="de316-110">**Action.Submit**</span></span>

## <a name="constraints"></a><span data-ttu-id="de316-111">约束</span><span class="sxs-lookup"><span data-stu-id="de316-111">Constraints</span></span>

<span data-ttu-id="de316-112">呈现器应考虑各种因素（如边距、填充、高度和宽度等卡片元素及其子元素的配置）来管理约束。</span><span class="sxs-lookup"><span data-stu-id="de316-112">The renderer should manage **Constraints** taking into account the various factors such as margin, padding, height and width etc configuration of the card elements and its children.</span></span>

## <a name="width"></a><span data-ttu-id="de316-113">宽度</span><span class="sxs-lookup"><span data-stu-id="de316-113">Width</span></span> 

1. <span data-ttu-id="de316-114">允许的值 - `auto`、`stretch` 和 `pixels` 方面的固定值和 `weight`</span><span class="sxs-lookup"><span data-stu-id="de316-114">Allowed values - `auto`, `stretch` and fixed values in terms of `pixels` and `weight`</span></span>
2. <span data-ttu-id="de316-115">`auto` 为宽度扩展提供足够的空间（支持最小扩展）</span><span class="sxs-lookup"><span data-stu-id="de316-115">`auto` provides sufficient space for expansion of width (supports min expansion)</span></span>
3. <span data-ttu-id="de316-116">`stretch` 占用剩余宽度（支持最大扩展）</span><span class="sxs-lookup"><span data-stu-id="de316-116">`stretch` takes up the remaining width (supports max expansion)</span></span>

<span data-ttu-id="de316-117">以下场景描述了不同的列宽度组合如何影响约束</span><span class="sxs-lookup"><span data-stu-id="de316-117">Below below scenarios describes how the constraints are affected with different width combinations for columns</span></span>

### <a name="auto-vs-stretch"></a><span data-ttu-id="de316-118">`auto` 与 `stretch`</span><span class="sxs-lookup"><span data-stu-id="de316-118">`auto` vs `stretch`</span></span>
1. <span data-ttu-id="de316-119">具有 `auto` 和 `stretch` 宽度的列。</span><span class="sxs-lookup"><span data-stu-id="de316-119">Columns with `auto` and `stretch` width.</span></span>

![具有 auto 和 stretch 宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width_1_auto_stretch.png)

* <span data-ttu-id="de316-121">宽度为 `auto` 的第一列占用足够的空间来显示内容，宽度为 `stretch` 的第二列占用整个空间。</span><span class="sxs-lookup"><span data-stu-id="de316-121">The first column with `auto` width takes sufficient space to display the content and the second column with `stretch` width takes up the entire space.</span></span>

2. <span data-ttu-id="de316-122">仅具有 `stretch` 宽度的列</span><span class="sxs-lookup"><span data-stu-id="de316-122">Columns with only `stretch` width</span></span>

![仅具有 stretch 宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width_2_stretch_stretch.png)

* <span data-ttu-id="de316-124">仅具有 stretch 宽度的列在等分后占用剩余的空间。</span><span class="sxs-lookup"><span data-stu-id="de316-124">Columns with only stretch width takes up the remaining spaces after dividing it equally.</span></span>

3. <span data-ttu-id="de316-125">`auto`、`stretch` 和 `auto`</span><span class="sxs-lookup"><span data-stu-id="de316-125">`auto`,`stretch` and `auto`</span></span> 

![具有 auto 和 stretch 组合宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width3_auto_stretch_auto.png)

<span data-ttu-id="de316-127">首先调整第一列和第三列的宽度以充分容纳元素，而具有伸展宽度的第二列占据剩余的空间  。</span><span class="sxs-lookup"><span data-stu-id="de316-127">The **first** and **third** columns width is adjusted first to accommodate the elements sufficiently and the **second** column with stretched width takes up the remaining space.</span></span> 

4. <span data-ttu-id="de316-128">使用宽度为 `auto` 的列显示元素的顺序</span><span class="sxs-lookup"><span data-stu-id="de316-128">Order of displaying elements with `auto` width columns</span></span>

![具有 auto 宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width6_all_auto.png)

* <span data-ttu-id="de316-130">具有 `auto` 的列将自行定位，以便为要呈现的内容提供足够的空间。</span><span class="sxs-lookup"><span data-stu-id="de316-130">Columns with `auto` will position themselves to provide ample space for the content to render.</span></span> 
* <span data-ttu-id="de316-131">对于“图像视图”，图像将缩小以适应剩余宽度。</span><span class="sxs-lookup"><span data-stu-id="de316-131">In case of **Image views**, images will downscale to fit the remaining width.</span></span> 
* <span data-ttu-id="de316-132">**注意：** 图像仅针对 `stretch` 和 `auto` 图像大小进行缩减，而不会针对以像素为单位的固定宽度和高度进行缩减。</span><span class="sxs-lookup"><span data-stu-id="de316-132">**Note:** Images will downscale only for `stretch` and `auto` image size, but not for fixed width and height in pixels.</span></span>    

### <a name="weights-vs-pixels"></a><span data-ttu-id="de316-133">`weights` 与 `pixels`</span><span class="sxs-lookup"><span data-stu-id="de316-133">`weights` vs `pixels`</span></span>

1. <span data-ttu-id="de316-134">具有 `weight` 和 `pixel` 宽度组合的列</span><span class="sxs-lookup"><span data-stu-id="de316-134">Columns with `weight` and `pixel` width combination</span></span>

![具有 weight 和 pixel 宽度组合的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width_4_w50_p100_w50.png)

* <span data-ttu-id="de316-136">上面的卡片包含三列，宽度配置如下：</span><span class="sxs-lookup"><span data-stu-id="de316-136">The above card has three columns with the following width configuration -</span></span> 
* <span data-ttu-id="de316-137">`Column1: Weight 50`, `Column2: 100px`, `Column3: Weight 50`</span><span class="sxs-lookup"><span data-stu-id="de316-137">`Column1: Weight 50`, `Column2: 100px`, `Column3: Weight 50`</span></span>
* <span data-ttu-id="de316-138">列 2 的宽度由 `pixel value` 确定</span><span class="sxs-lookup"><span data-stu-id="de316-138">The width of Column 2 is determined by the `pixel value`</span></span>
* <span data-ttu-id="de316-139">列 1 和列 3 的宽度根据 `weights` 和计算的 `weight ratio` 进行调整。</span><span class="sxs-lookup"><span data-stu-id="de316-139">The width of Column 1 and 3 is adjusted based on the `weights` and the calculated `weight ratio`.</span></span>

2. <span data-ttu-id="de316-140">具有 `weight`、`pixel width` 和`auto` 特性的列</span><span class="sxs-lookup"><span data-stu-id="de316-140">Columns with `weight`, `pixel width` and `auto` attributes</span></span>

![具有 weight、pixel 和 auto 宽度组合的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width5_w50_p100_w50_auto.png)

* <span data-ttu-id="de316-142">上面的卡片包含四列，宽度配置如下：</span><span class="sxs-lookup"><span data-stu-id="de316-142">The above card has four columns with the following width configuration -</span></span> 
* <span data-ttu-id="de316-143">`Column1: Weight 50`、`Column2: 100px`、`Column3: Weight 50` 和 `Column4: auto`</span><span class="sxs-lookup"><span data-stu-id="de316-143">`Column1: Weight 50`, `Column2: 100px`, `Column3: Weight 50`, and `Column4: auto`</span></span>
* <span data-ttu-id="de316-144">**注意：** 使用宽度为 `auto` 的列的图像视图缩减，以适应剩余空间。</span><span class="sxs-lookup"><span data-stu-id="de316-144">**Note:** Image view with `auto` width column downscales to adjust to the remaining space.</span></span> 

### <a name="precedence-order-of-displaying-elements-with-the-width-attribute"></a><span data-ttu-id="de316-145">使用 Width 特性显示元素的优先顺序</span><span class="sxs-lookup"><span data-stu-id="de316-145">Precedence order of displaying elements with the width attribute</span></span>
`px` > `weight` > `auto` > `stretch`


## <a name="height"></a><span data-ttu-id="de316-146">高度</span><span class="sxs-lookup"><span data-stu-id="de316-146">Height</span></span> 

 <span data-ttu-id="de316-147">允许的值 - `auto` 和 `stretch`</span><span class="sxs-lookup"><span data-stu-id="de316-147">Allowed values - `auto` and `stretch`</span></span> 

<span data-ttu-id="de316-148">以下场景描述了不同的卡片元素高度组合如何影响约束</span><span class="sxs-lookup"><span data-stu-id="de316-148">Below  scenarios describes how the constraints are affected with different height combinations for card elements</span></span>

1. <span data-ttu-id="de316-149">当卡片的高度不固定时，元素可自由地垂直扩展</span><span class="sxs-lookup"><span data-stu-id="de316-149">Elements expand freely vertically when card is not of fixed height</span></span>

![具有 auto 和 stretch 高度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/height1_text_wrap_off.png)

* <span data-ttu-id="de316-151">无论 `auto` 和 `stretch` 值如何，这两列都可以充分垂直扩展</span><span class="sxs-lookup"><span data-stu-id="de316-151">Both the columns can expand sufficiently vertically irrespective of `auto` and `stretch` values</span></span>
* <span data-ttu-id="de316-152">这是对文本块禁用了 `wrap` 属性的情况。</span><span class="sxs-lookup"><span data-stu-id="de316-152">This is with the `wrap` property disabled for the text block.</span></span>

2. <span data-ttu-id="de316-153">下面的卡片为文本块启用了 `wrap` 属性。</span><span class="sxs-lookup"><span data-stu-id="de316-153">The card below has the `wrap` property enabled for the text block.</span></span> 

![具有文本块的 wrap 属性的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/height2_text_wrap_on.png)


## <a name="spacing-and-separator"></a><span data-ttu-id="de316-155">间距和分隔符</span><span class="sxs-lookup"><span data-stu-id="de316-155">Spacing and Separator</span></span>

 1. <span data-ttu-id="de316-156">间距 - 允许的值有 `none`、`small`、`default`、`medium`、`large`、`extra large` 和 `padding`</span><span class="sxs-lookup"><span data-stu-id="de316-156">**Spacing** - Allowed values `none`, `small`, `default`, `medium`, `large`, `extra large` and `padding`</span></span> 

* <span data-ttu-id="de316-157">Spacing 特性增加了此元素和前一个元素之间的间距。</span><span class="sxs-lookup"><span data-stu-id="de316-157">Spacing attribute adds spacing between this element and the preceding element.</span></span>

![具有不同间距组合的元素](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing1.png)

* <span data-ttu-id="de316-159">当 Spacing 特性是视图容器中的第一个元素时，它不起任何作用。</span><span class="sxs-lookup"><span data-stu-id="de316-159">Spacing attribute does not have any effect when its the first element in the view container.</span></span> 

![间距不起作用的元素](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing_no_effect.png)

* <span data-ttu-id="de316-161">标记有箭头的元素是其同级元素中的第一个元素，因此间距不起作用。</span><span class="sxs-lookup"><span data-stu-id="de316-161">The elements marked with arrow are the first elements among its siblings, so spacing has no effect.</span></span> 

 2. <span data-ttu-id="de316-162">分隔符 - 可能的值（打开/关闭切换）</span><span class="sxs-lookup"><span data-stu-id="de316-162">**Separator** - Possible values (on/off toggle)</span></span>

* <span data-ttu-id="de316-163">在元素的顶部绘制一条分隔线。</span><span class="sxs-lookup"><span data-stu-id="de316-163">Draws a seperating line at the top of the element.</span></span>

![具有 Seperator 特性的元素](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing3_seperator.png)

3. <span data-ttu-id="de316-165">间距和分隔符组合</span><span class="sxs-lookup"><span data-stu-id="de316-165">**Spacing and Seperator combination**</span></span>

* <span data-ttu-id="de316-166">间距和分隔符组合的约束如下所示。</span><span class="sxs-lookup"><span data-stu-id="de316-166">The constraints of the spacing and the seperator combination are illustrated below.</span></span> 

![间距和分隔符组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing4_with_seperator.png)

* <span data-ttu-id="de316-168">总间距距离相对于所提供的值保持不变。</span><span class="sxs-lookup"><span data-stu-id="de316-168">The overall spacing distance is maintained with respect to the values provided.</span></span>
* <span data-ttu-id="de316-169">在间距距离的中间添加分隔符。</span><span class="sxs-lookup"><span data-stu-id="de316-169">The seperator is added halfway in the middle of the spaced distance.</span></span>

<span data-ttu-id="de316-170">[注意：</span><span class="sxs-lookup"><span data-stu-id="de316-170">[Note.</span></span> <span data-ttu-id="de316-171">需要确认在间距区插入分隔符的距离。</span><span class="sxs-lookup"><span data-stu-id="de316-171">Need to confirm the distance where the seperator is inserted in the spacing area.</span></span> <span data-ttu-id="de316-172">似乎应是中间]</span><span class="sxs-lookup"><span data-stu-id="de316-172">Seems like the middle]</span></span>

## <a name="container-styles"></a><span data-ttu-id="de316-173">容器样式</span><span class="sxs-lookup"><span data-stu-id="de316-173">Container Styles</span></span>

* <span data-ttu-id="de316-174">为列和列集等容器提供样式提示</span><span class="sxs-lookup"><span data-stu-id="de316-174">Provides styling hints for containers such as columns and columnset</span></span>
* <span data-ttu-id="de316-175">允许的值 - `none`、`default`、`emphasis`、`good`、`attention`、`warning` 和 `accent`</span><span class="sxs-lookup"><span data-stu-id="de316-175">Allowed values `none`, `default`, `emphasis`, `good`, `attention`, `warning` and `accent`</span></span>
* <span data-ttu-id="de316-176">这些预定义的样式选项为容器内的元素和背景色提供了填充</span><span class="sxs-lookup"><span data-stu-id="de316-176">These predefined style options provides padding for the elements within the container and background color</span></span>


![列和列集样式组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/style1.png)

1. <span data-ttu-id="de316-178">卡片 A 说明了没有样式选项的列和列集</span><span class="sxs-lookup"><span data-stu-id="de316-178">Card A illustrates columns and columnset with no style options</span></span>
2. <span data-ttu-id="de316-179">卡片 B 说明了具有 Attention 样式的列集。</span><span class="sxs-lookup"><span data-stu-id="de316-179">Card B illustrates columnset with **Attention** style.</span></span> <span data-ttu-id="de316-180">请注意列集容器中的填充和背景色的更改。</span><span class="sxs-lookup"><span data-stu-id="de316-180">Notice the padding within the columnset container and the change in background color.</span></span> 
3. <span data-ttu-id="de316-181">卡片 C 仅说明了具有样式的列。</span><span class="sxs-lookup"><span data-stu-id="de316-181">Card C illustrates columns with styling only.</span></span> <span data-ttu-id="de316-182">与上一项类似，列包含填充和背景更改。</span><span class="sxs-lookup"><span data-stu-id="de316-182">Similar to the previous one, column includes padding and background change.</span></span> 
4. <span data-ttu-id="de316-183">卡片 D 说明了具有样式选项的列和列集。</span><span class="sxs-lookup"><span data-stu-id="de316-183">Card D illustrates columns and columnset both with style options.</span></span>

<span data-ttu-id="de316-184">[注意：</span><span class="sxs-lookup"><span data-stu-id="de316-184">[Note.</span></span> <span data-ttu-id="de316-185">需要检查如何确定填充量。</span><span class="sxs-lookup"><span data-stu-id="de316-185">Need to check how the padding amount is determined.</span></span> <span data-ttu-id="de316-186">它是由主机决定的吗？</span><span class="sxs-lookup"><span data-stu-id="de316-186">Is it determined by the host?</span></span> <span data-ttu-id="de316-187">]</span><span class="sxs-lookup"><span data-stu-id="de316-187">]</span></span>

## <a name="bleed"></a><span data-ttu-id="de316-188">出血</span><span class="sxs-lookup"><span data-stu-id="de316-188">Bleed</span></span>

* <span data-ttu-id="de316-189">此属性允许列和列集等容器通过其父项出血。</span><span class="sxs-lookup"><span data-stu-id="de316-189">This property allows the container such as columns and columnset to bleed through its parent.</span></span> 
* <span data-ttu-id="de316-190">可能的值有 `on` 和 `off`。</span><span class="sxs-lookup"><span data-stu-id="de316-190">Possible values `on` and `off`.</span></span>


![具有 Bleed 属性的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/style2_withBleed.png)

1. <span data-ttu-id="de316-192">卡片 A 说明了具有常规样式的列和列集。</span><span class="sxs-lookup"><span data-stu-id="de316-192">Card A illustrates columns and columnset with regular styling.</span></span>
2. <span data-ttu-id="de316-193">卡片 B 说明了具有出血选项的第一列。</span><span class="sxs-lookup"><span data-stu-id="de316-193">Card B illustrates the first column with bleed option.</span></span> <span data-ttu-id="de316-194">内容只是通过它的边界出血到它的父边界。</span><span class="sxs-lookup"><span data-stu-id="de316-194">The content just bleeds through its boundaries to its parent's.</span></span> 
 
## <a name="image-size"></a><span data-ttu-id="de316-195">映像大小</span><span class="sxs-lookup"><span data-stu-id="de316-195">Image Size</span></span>

### <a name="size-attribute"></a><span data-ttu-id="de316-196">`Size` 特性</span><span class="sxs-lookup"><span data-stu-id="de316-196">`Size` attribute</span></span>
* <span data-ttu-id="de316-197">允许的值 - `auto`、`stretch`、`small`、`medium`、`large`</span><span class="sxs-lookup"><span data-stu-id="de316-197">Allowed values - `auto`, `stretch`, `small`, `medium`, `large`</span></span>
* <span data-ttu-id="de316-198">`auto`：图像将纵向缩减以适应需要，但不会纵向扩展以填充该区域。</span><span class="sxs-lookup"><span data-stu-id="de316-198">`auto` : Images will scale down to fit if needed, but will not scale up to fill the area.</span></span>
* <span data-ttu-id="de316-199">`stretch`：图像纵向缩减和扩展以适应需要。</span><span class="sxs-lookup"><span data-stu-id="de316-199">`stretch` : Image with both scale down and up to fit as needed.</span></span>
* <span data-ttu-id="de316-200">`small`、`medium` 和 `large`：图像以固定宽度显示，宽度由主机决定。</span><span class="sxs-lookup"><span data-stu-id="de316-200">`small`, `medium` and `large`: Image is displayed with a fixed width, where the width is determined by the host.</span></span>

1. <span data-ttu-id="de316-201">`auto` 与 `stretch`</span><span class="sxs-lookup"><span data-stu-id="de316-201">`auto` vs `stretch`</span></span>

![具有 auto 和 stretch 行为的图像](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/image_size_auto_stretch.png)

2. <span data-ttu-id="de316-203">列宽度和图像大小组合</span><span class="sxs-lookup"><span data-stu-id="de316-203">Column width and Image Size combination</span></span>

![列宽度和图像大小组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/imagesize2.png)

* <span data-ttu-id="de316-205">通常情况下，具有 `stretch` 宽度的列允许图像以 `stretch` 大小自由放大。</span><span class="sxs-lookup"><span data-stu-id="de316-205">Generally, Columns with `stretch` width allow images to upscale freely with `stretch` size.</span></span>
* <span data-ttu-id="de316-206">宽度为 `auto` 的列允许图像占用精确的空间，而不考虑图像的 `auto` 和 `stretch` 大小。</span><span class="sxs-lookup"><span data-stu-id="de316-206">Columns with `auto` width allows image to occupy exact space irrespective of `auto` and `stretch` size of image.</span></span>
* <span data-ttu-id="de316-207">在这种排列中，列宽度在确定图像大小方面更为优先。</span><span class="sxs-lookup"><span data-stu-id="de316-207">Column width takes more precedence in determining the image size in this arrangement.</span></span>

### <a name="image-width-in-pixels-attribute"></a><span data-ttu-id="de316-208">图像 `Width (in pixels)` 特性</span><span class="sxs-lookup"><span data-stu-id="de316-208">Image `Width (in pixels)` attribute</span></span>
* <span data-ttu-id="de316-209">这提供了所需的图像屏幕宽度。</span><span class="sxs-lookup"><span data-stu-id="de316-209">This provides the desired on-screen width of the image.</span></span> 
* <span data-ttu-id="de316-210">若指定了一个值，`size` 属性会被替代</span><span class="sxs-lookup"><span data-stu-id="de316-210">`size` property is overriden when a value is specified</span></span>

![列宽度和图像宽度（以像素为单位）组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/image_size_3.png)
* <span data-ttu-id="de316-212">在这种排列中，宽度为 `auto` 的列在为图像内容提供空间方面将比 `stretch` 更优先。</span><span class="sxs-lookup"><span data-stu-id="de316-212">The column with `auto` width will have more precedence than `stretch` in providing room for image content in this arrangement.</span></span> 

### <a name="column-width-weight-and-pixel-and-image-size-auto-and-stretch-combination"></a><span data-ttu-id="de316-213">列宽度（weight 和 pixel）和图像大小（auto 和 stretch）组合</span><span class="sxs-lookup"><span data-stu-id="de316-213">Column Width (weight and pixel) and Image size (auto and stretch) Combination</span></span>

![列宽度和图像大小组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/column_width_image_width_2.png)
* <span data-ttu-id="de316-215">在 `weight` 和 `pixel` 列宽的约束范围内，大小为 `auto` 的图像使用足够的空间进行扩展（或缩小）。</span><span class="sxs-lookup"><span data-stu-id="de316-215">Images with `auto` size takes sufficient space for expansion (or downscales) within the column constraints of `weight` and `pixel` width.</span></span> 
* <span data-ttu-id="de316-216">在 `weight` 和 `pixel` 列宽的约束范围内，大小为 `stretch` 的图像可扩展以填充剩余空间。</span><span class="sxs-lookup"><span data-stu-id="de316-216">Images with `stretch` size can expand to fill the remaining space within the constraints of column `weight` and `pixel` width.</span></span> 

## <a name="actionsubmit"></a><span data-ttu-id="de316-217">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="de316-217">Action.Submit</span></span>
* <span data-ttu-id="de316-218">`Action.Submit` 元素收集输入字段、与可选数据字段合并，并将事件发送到客户端。</span><span class="sxs-lookup"><span data-stu-id="de316-218">`Action.Submit` element gathers input fields, merges with optional data field, and sends an event to the client.</span></span>
* <span data-ttu-id="de316-219">ACL 呈现器的 1.x 和 2.x 版本之间的元素行为存在显著差异。</span><span class="sxs-lookup"><span data-stu-id="de316-219">A significant difference in the element behaviour is present between 1.x and 2.x version of the ACL renderer.</span></span>

![列宽度和图像宽度组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/action_submit_behaviour.png)

* <span data-ttu-id="de316-221">`1.x Renderer` - 输入是从所有字段收集的，与输入字段在层次结构中的位置无关。</span><span class="sxs-lookup"><span data-stu-id="de316-221">`1.x Renderer` - The inputs are collected from all fields irrespective of the where in the hierarchy the input field is present.</span></span> 
* <span data-ttu-id="de316-222">`2.x Renderer` - 输入是从父容器中的字段收集的，或作为 `Action.Submit` 元素的同级元素收集的。</span><span class="sxs-lookup"><span data-stu-id="de316-222">`2.x Renderer` - The inputs are collected from fields present in parent container or as a sibling of the `Action.Submit` element.</span></span> 

## <a name="summary"></a><span data-ttu-id="de316-223">总结</span><span class="sxs-lookup"><span data-stu-id="de316-223">Summary</span></span>
* <span data-ttu-id="de316-224">在确定图像大小时，列宽度比图像大小（auto、stretch、min 宽度等）更为优先。</span><span class="sxs-lookup"><span data-stu-id="de316-224">Column width takes more precedence in determining the size of the image than its image size (auto, stretch, min width etc).</span></span> 
* <span data-ttu-id="de316-225">用于充分显示内容所采用的列宽度优先级 - `px` > `weight` > `auto` > `stretch`</span><span class="sxs-lookup"><span data-stu-id="de316-225">The precedence of the column width taken to display its content sufficiently - `px` > `weight` > `auto` > `stretch`</span></span>
* <span data-ttu-id="de316-226">若提供了以像素为单位的图像 `width` 和 `height`，图像 `size`（auto、stretch）将被忽略。</span><span class="sxs-lookup"><span data-stu-id="de316-226">Image `size` (auto, stretch) is **ignored** when Image `width` and `height` in px is provided.</span></span> 
* <span data-ttu-id="de316-227">图像 `stretch` 大小特性仅在有剩余空间且列不是 `auto` 时才会放大图像。</span><span class="sxs-lookup"><span data-stu-id="de316-227">Image `stretch` size attribute will upscale the image only when there is remaining space and column auto is **not** `auto`.</span></span>
* <span data-ttu-id="de316-228">在列的可用空间中，图像会将其自身拉伸到它能保持其纵横比的极限。</span><span class="sxs-lookup"><span data-stu-id="de316-228">An image stretches itself to the limit where it maintain its aspect ratio in the space available in the column.</span></span> <span data-ttu-id="de316-229">而高度则自由扩展。</span><span class="sxs-lookup"><span data-stu-id="de316-229">In turn, the height expands freely.</span></span>
* <span data-ttu-id="de316-230">当 `Spacing` 特性是其同级元素中的第一个或唯一元素时，它不起任何作用。</span><span class="sxs-lookup"><span data-stu-id="de316-230">`Spacing` attribute will not have any effect when its the first or the only element among its sibling.</span></span> 



