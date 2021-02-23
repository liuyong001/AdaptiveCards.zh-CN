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
# <a name="adaptive-card-renderer-behaviour-guideline"></a>自适应卡片呈现器行为准则

以下规范介绍了在实现与分析卡片元素之间的关系有关的呈现器行为时要遵循的设计准则。 
> [!IMPORTANT]
> 
> 此内容尚未完成。 请稍后再回来查看。


## <a name="behaviours"></a>行为 

在呈现与本文档中提到的特性相关的卡片元素时，呈现器必须注意以下行为。 

1. **约束**
2. 图像大小
3. **Action.Submit**

## <a name="constraints"></a>约束

呈现器应考虑各种因素（如边距、填充、高度和宽度等卡片元素及其子元素的配置）来管理约束。

## <a name="width"></a>宽度 

1. 允许的值 - `auto`、`stretch` 和 `pixels` 方面的固定值和 `weight`
2. `auto` 为宽度扩展提供足够的空间（支持最小扩展）
3. `stretch` 占用剩余宽度（支持最大扩展）

以下场景描述了不同的列宽度组合如何影响约束

### <a name="auto-vs-stretch"></a>`auto` 与 `stretch`
1. 具有 `auto` 和 `stretch` 宽度的列。

![具有 auto 和 stretch 宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width_1_auto_stretch.png)

* 宽度为 `auto` 的第一列占用足够的空间来显示内容，宽度为 `stretch` 的第二列占用整个空间。

2. 仅具有 `stretch` 宽度的列

![仅具有 stretch 宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width_2_stretch_stretch.png)

* 仅具有 stretch 宽度的列在等分后占用剩余的空间。

3. `auto`、`stretch` 和 `auto` 

![具有 auto 和 stretch 组合宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width3_auto_stretch_auto.png)

首先调整第一列和第三列的宽度以充分容纳元素，而具有伸展宽度的第二列占据剩余的空间  。 

4. 使用宽度为 `auto` 的列显示元素的顺序

![具有 auto 宽度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width6_all_auto.png)

* 具有 `auto` 的列将自行定位，以便为要呈现的内容提供足够的空间。 
* 对于“图像视图”，图像将缩小以适应剩余宽度。 
* **注意：** 图像仅针对 `stretch` 和 `auto` 图像大小进行缩减，而不会针对以像素为单位的固定宽度和高度进行缩减。    

### <a name="weights-vs-pixels"></a>`weights` 与 `pixels`

1. 具有 `weight` 和 `pixel` 宽度组合的列

![具有 weight 和 pixel 宽度组合的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width_4_w50_p100_w50.png)

* 上面的卡片包含三列，宽度配置如下： 
* `Column1: Weight 50`, `Column2: 100px`, `Column3: Weight 50`
* 列 2 的宽度由 `pixel value` 确定
* 列 1 和列 3 的宽度根据 `weights` 和计算的 `weight ratio` 进行调整。

2. 具有 `weight`、`pixel width` 和`auto` 特性的列

![具有 weight、pixel 和 auto 宽度组合的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/width5_w50_p100_w50_auto.png)

* 上面的卡片包含四列，宽度配置如下： 
* `Column1: Weight 50`、`Column2: 100px`、`Column3: Weight 50` 和 `Column4: auto`
* **注意：** 使用宽度为 `auto` 的列的图像视图缩减，以适应剩余空间。 

### <a name="precedence-order-of-displaying-elements-with-the-width-attribute"></a>使用 Width 特性显示元素的优先顺序
`px` > `weight` > `auto` > `stretch`


## <a name="height"></a>高度 

 允许的值 - `auto` 和 `stretch` 

以下场景描述了不同的卡片元素高度组合如何影响约束

1. 当卡片的高度不固定时，元素可自由地垂直扩展

![具有 auto 和 stretch 高度的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/height1_text_wrap_off.png)

* 无论 `auto` 和 `stretch` 值如何，这两列都可以充分垂直扩展
* 这是对文本块禁用了 `wrap` 属性的情况。

2. 下面的卡片为文本块启用了 `wrap` 属性。 

![具有文本块的 wrap 属性的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/height2_text_wrap_on.png)


## <a name="spacing-and-separator"></a>间距和分隔符

 1. 间距 - 允许的值有 `none`、`small`、`default`、`medium`、`large`、`extra large` 和 `padding` 

* Spacing 特性增加了此元素和前一个元素之间的间距。

![具有不同间距组合的元素](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing1.png)

* 当 Spacing 特性是视图容器中的第一个元素时，它不起任何作用。 

![间距不起作用的元素](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing_no_effect.png)

* 标记有箭头的元素是其同级元素中的第一个元素，因此间距不起作用。 

 2. 分隔符 - 可能的值（打开/关闭切换）

* 在元素的顶部绘制一条分隔线。

![具有 Seperator 特性的元素](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing3_seperator.png)

3. 间距和分隔符组合

* 间距和分隔符组合的约束如下所示。 

![间距和分隔符组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/spacing4_with_seperator.png)

* 总间距距离相对于所提供的值保持不变。
* 在间距距离的中间添加分隔符。

[注意： 需要确认在间距区插入分隔符的距离。 似乎应是中间]

## <a name="container-styles"></a>容器样式

* 为列和列集等容器提供样式提示
* 允许的值 - `none`、`default`、`emphasis`、`good`、`attention`、`warning` 和 `accent`
* 这些预定义的样式选项为容器内的元素和背景色提供了填充


![列和列集样式组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/style1.png)

1. 卡片 A 说明了没有样式选项的列和列集
2. 卡片 B 说明了具有 Attention 样式的列集。 请注意列集容器中的填充和背景色的更改。 
3. 卡片 C 仅说明了具有样式的列。 与上一项类似，列包含填充和背景更改。 
4. 卡片 D 说明了具有样式选项的列和列集。

[注意： 需要检查如何确定填充量。 它是由主机决定的吗？ ]

## <a name="bleed"></a>出血

* 此属性允许列和列集等容器通过其父项出血。 
* 可能的值有 `on` 和 `off`。


![具有 Bleed 属性的列](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/style2_withBleed.png)

1. 卡片 A 说明了具有常规样式的列和列集。
2. 卡片 B 说明了具有出血选项的第一列。 内容只是通过它的边界出血到它的父边界。 
 
## <a name="image-size"></a>映像大小

### <a name="size-attribute"></a>`Size` 特性
* 允许的值 - `auto`、`stretch`、`small`、`medium`、`large`
* `auto`：图像将纵向缩减以适应需要，但不会纵向扩展以填充该区域。
* `stretch`：图像纵向缩减和扩展以适应需要。
* `small`、`medium` 和 `large`：图像以固定宽度显示，宽度由主机决定。

1. `auto` 与 `stretch`

![具有 auto 和 stretch 行为的图像](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/image_size_auto_stretch.png)

2. 列宽度和图像大小组合

![列宽度和图像大小组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/imagesize2.png)

* 通常情况下，具有 `stretch` 宽度的列允许图像以 `stretch` 大小自由放大。
* 宽度为 `auto` 的列允许图像占用精确的空间，而不考虑图像的 `auto` 和 `stretch` 大小。
* 在这种排列中，列宽度在确定图像大小方面更为优先。

### <a name="image-width-in-pixels-attribute"></a>图像 `Width (in pixels)` 特性
* 这提供了所需的图像屏幕宽度。 
* 若指定了一个值，`size` 属性会被替代

![列宽度和图像宽度（以像素为单位）组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/image_size_3.png)
* 在这种排列中，宽度为 `auto` 的列在为图像内容提供空间方面将比 `stretch` 更优先。 

### <a name="column-width-weight-and-pixel-and-image-size-auto-and-stretch-combination"></a>列宽度（weight 和 pixel）和图像大小（auto 和 stretch）组合

![列宽度和图像大小组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/column_width_image_width_2.png)
* 在 `weight` 和 `pixel` 列宽的约束范围内，大小为 `auto` 的图像使用足够的空间进行扩展（或缩小）。 
* 在 `weight` 和 `pixel` 列宽的约束范围内，大小为 `stretch` 的图像可扩展以填充剩余空间。 

## <a name="actionsubmit"></a>Action.Submit
* `Action.Submit` 元素收集输入字段、与可选数据字段合并，并将事件发送到客户端。
* ACL 呈现器的 1.x 和 2.x 版本之间的元素行为存在显著差异。

![列宽度和图像宽度组合](https://github.com/manujai/AdaptiveCards/blob/doc_renderer_behaviour/AdaptiveCards/content/action_submit_behaviour.png)

* `1.x Renderer` - 输入是从所有字段收集的，与输入字段在层次结构中的位置无关。 
* `2.x Renderer` - 输入是从父容器中的字段收集的，或作为 `Action.Submit` 元素的同级元素收集的。 

## <a name="summary"></a>总结
* 在确定图像大小时，列宽度比图像大小（auto、stretch、min 宽度等）更为优先。 
* 用于充分显示内容所采用的列宽度优先级 - `px` > `weight` > `auto` > `stretch`
* 若提供了以像素为单位的图像 `width` 和 `height`，图像 `size`（auto、stretch）将被忽略。 
* 图像 `stretch` 大小特性仅在有剩余空间且列不是 `auto` 时才会放大图像。
* 在列的可用空间中，图像会将其自身拉伸到它能保持其纵横比的极限。 而高度则自由扩展。
* 当 `Spacing` 特性是其同级元素中的第一个或唯一元素时，它不起任何作用。 



