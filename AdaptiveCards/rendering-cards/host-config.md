---
title: 自适应卡片的 HostConfig
author: paulcam206
ms.author: paulcam
ms.date: 09/18/2018
ms.topic: reference
ms.openlocfilehash: 46ba9987cf162e95ab86dcdafa55e10df29b1121
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552589"
---
# <a name="what-is-hostconfig"></a>什么是 HostConfig？
`HostConfig` 是一个**跨平台配置对象**，用于指定自适应卡片呈现器生成 UI 的方式。

这样，那些跨平台的属性就可以在不同平台和设备的呈现器中共享。 另外还可以创建工具，让你了解该卡片在给定环境下的外观。

请查看 [HostConfig.json](https://github.com/Microsoft/AdaptiveCards/blob/master/samples/HostConfig/sample.json) 示例，了解其内容。

---

   * [`AdaptiveCardConfig`](#schema-adaptivecardconfig) - `AdaptiveCards` 的顶级选项
   * [`ActionsConfig`](#schema-actionsconfig) - `Action` 的选项
   * [`ContainerStylesConfig`](#schema-containerstylesconfig) - 控制默认的强调容器的样式设置
   * [`FactSetConfig`](#schema-factsetconfig) - 控制 `FactSet` 的显示
   * [`FontSizesConfig`](#schema-fontsizesconfig) - 控制不同文本样式的字体大小指标
   * [`FontWeightsConfig`](#schema-fontweightsconfig) - 控制字体粗细指标
   * [`ForegroundColorsConfig`](#schema-foregroundcolorsconfig) - 控制各种字体颜色
   * [`ImageSetConfig`](#schema-imagesetconfig) - 控制 `ImageSet` 的显示方式
   * [`ImageSizesConfig`](#schema-imagesizesconfig) - 控制 `Image` 大小
   * [`MediaConfig`](#schema-mediaconfig) - 控制 `Media` 元素的显示和行为
   * [`SeparatorConfig`](#schema-separatorconfig) - 控制分隔符的显示方式
   * [`ShowCardConfig`](#schema-showcardconfig) - 控制 `Action.ShowCard` 的行为和样式设置
   * [`SpacingsConfig`](#schema-spacingsconfig) - 控制元素的布局方式
   * [`TextBlockConfig`](#schema-textblockconfig) - 控制文本显示的参数

# <a name="card-configuration"></a>卡片配置

<a name="schema-adaptivecardconfig"></a>
## <a name="adaptivecardconfig"></a>AdaptiveCardConfig

`AdaptiveCards` 的顶级选项

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**allowCustomStyle**|`boolean`| 否，默认值为：`true`|控制是否允许自定义样式设置|1.0
|**supportsInteractivity**|`boolean`| 否，默认值为：`true`|控制是否允许调用交互式 `Action`|1.0
|**imageBaseUrl**|`string`| 否|在加载资源时需要使用的 URL|1.0
|**fontFamily**|`string`| 否，默认值为：`"Calibri"`|呈现文本时需要使用的字体|1.0
|**actions**|`object`| 否|`Action` 的选项|1.0
|**adaptiveCard**|`object`| 否|`AdaptiveCards` 的顶级选项|1.0
|**containerStyles**|`object`| 否|控制默认的强调容器的样式设置|1.0
|**imageSizes**|`object`| 否|控制 `Image` 大小|1.0
|**imageSet**|`object`| 否|控制 `ImageSet` 的显示方式|1.0
|**factSet**|`object`| 否|控制 `FactSet` 的显示|1.0
|**fontSizes**|`object`| 否|控制不同文本样式的字体大小指标|1.0
|**fontWeights**|`object`| 否|控制字体粗细指标|1.0
|**spacing**|`object`| 否|控制元素的布局方式|1.0
|**separator**|`object`| 否|控制分隔符的显示方式|1.0
|**media**|`object`| 否|控制 `Media` 元素的显示和行为|1.1


<a name="schema-actionsconfig"></a>
## <a name="actionsconfig"></a>ActionsConfig

`Action` 的选项

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**actionsOrientation**|`string`| 否，默认值为：`"horizontal"`|控制按钮的布局方式|1.0
|**actionAlignment**|`string`| 否，默认值为：`"stretch"`|控制按钮的布局|1.0
|**buttonSpacing**|`integer`| 否，默认值为：`10`|控制在按钮之间使用的空间量|1.0
|**maxActions**|`integer`| 否，默认值为：`5`|控制允许的操作总数|1.0
|**spacing**|`string`| 否，默认值为：`"default"`|控制操作元素的总体间距|1.0
|**showCard**|`object`| 否|控制 `Action.ShowCard` 的行为和样式设置|1.0
|**iconPlacement**|`string`| 否，默认值为：`"aboveTitle"`|控制操作图标的放置位置|1.0
|**iconSize**|`integer`| 否，默认值为：`30`|控制操作图标的大小|1.0


<a name="schema-containerstylesconfig"></a>
## <a name="containerstylesconfig"></a>ContainerStylesConfig

控制默认的强调容器的样式设置

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**default**|`object`| 否|默认的容器样式|1.0
|**emphasis**|`object`| 否|用于强调的容器样式|1.0


<a name="schema-factsetconfig"></a>
## <a name="factsetconfig"></a>FactSetConfig

控制 `FactSet` 的显示

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**title**|`object`| 否，默认值为：`{"weight":"bolder","size":"default","color":"default","isSubtle":false,"wrap":true,"maxWidth":150}`|控制文本显示的参数|1.0
|**value**|`object`| 否，默认值为：`{"weight":"default","size":"default","color":"default","isSubtle":false,"wrap":true,"maxWidth":0}`|控制文本显示的参数|1.0
|**spacing**|`integer`| 否，默认值为：`10`|&nbsp;|1.0


<a name="schema-fontsizesconfig"></a>
## <a name="fontsizesconfig"></a>FontSizesConfig

控制不同文本样式的字体大小指标

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**small**|`integer`| 否，默认值为：`10`|小字号|1.0
|**default**|`integer`| 否，默认值为：`12`|默认字号|1.0
|**medium**|`integer`| 否，默认值为：`14`|中字号|1.0
|**large**|`integer`| 否，默认值为：`17`|大字号|1.0
|**extraLarge**|`integer`| 否，默认值为：`20`|超大字号|1.0


<a name="schema-fontweightsconfig"></a>
## <a name="fontweightsconfig"></a>FontWeightsConfig

控制字体粗细指标

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**lighter**|`integer`| 否，默认值为：`200`|&nbsp;|1.0
|**default**|`integer`| 否，默认值为：`400`|&nbsp;|1.0
|**bolder**|`integer`| 否，默认值为：`800`|&nbsp;|1.0


<a name="schema-foregroundcolorsconfig"></a>
## <a name="foregroundcolorsconfig"></a>ForegroundColorsConfig

控制各种字体颜色

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**default**|`object`| 否，默认值为：`{"default":"#FF000000","subtle":"#B2000000"}`|&nbsp;|1.0
|**accent**|`object`| 否，默认值为：`{"default":"#FF0000FF","subtle":"#B20000FF"}`|&nbsp;|1.0
|**dark**|`object`| 否，默认值为：`{"default":"#FF101010","subtle":"#B2101010"}`|&nbsp;|1.0
|**light**|`object`| 否，默认值为：`{"default":"#FFFFFFFF","subtle":"#B2FFFFFF"}`|&nbsp;|1.0
|**good**|`object`| 否，默认值为：`{"default":"#FF008000","subtle":"#B2008000"}`|&nbsp;|1.0
|**warning**|`object`| 否，默认值为：`{"default":"#FFFFD700","subtle":"#B2FFD700"}`|&nbsp;|1.0
|**attention**|`object`| 否，默认值为：`{"default":"#FF8B0000","subtle":"#B28B0000"}`|&nbsp;|1.0


<a name="schema-imagesetconfig"></a>
## <a name="imagesetconfig"></a>ImageSetConfig

控制 `ImageSet` 的显示方式

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**imageSize**|`string`| 否，默认值为：`"auto"`|控制单个图像大小|1.0
|**maxImageHeight**|`integer`| 否，默认值为：`100`|将图像高度限制为此值|1.0


<a name="schema-imagesizesconfig"></a>
## <a name="imagesizesconfig"></a>ImageSizesConfig

控制 `Image` 大小

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**small**|`integer`| 否，默认值为：`80`|小型图像大小值|1.0
|**medium**|`integer`| 否，默认值为：`120`|中型图像大小值|1.0
|**large**|`integer`| 否，默认值为：`180`|大型图像大小值|1.0


<a name="schema-mediaconfig"></a>
## <a name="mediaconfig"></a>MediaConfig

控制 `Media` 元素的显示和行为

#### <a name="introduced-in-version-11"></a>在版本 1.1 中引入

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**defaultPoster**|`string`| 否|在播放按钮尚未调用时需显示的图像的 URI|1.1
|**playButton**|`string`| 否|将显示为播放按钮的图像|1.1
|**allowInlinePlayback**|`boolean`| 否，默认值为：`true`|是以内联方式显示媒体，还是通过外部方式进行调用|1.1


<a name="schema-separatorconfig"></a>
## <a name="separatorconfig"></a>SeparatorConfig

控制分隔符的显示方式

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**lineThickness**|`integer`| 否，默认值为：`1`|分隔线的粗细|1.0
|**lineColor**|`string,null`| 否，默认值为：`#B2000000`|绘制分隔线时需使用的颜色|1.0


<a name="schema-showcardconfig"></a>
## <a name="showcardconfig"></a>ShowCardConfig

控制 `Action.ShowCard` 的行为和样式设置

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**actionMode**|`string`| 否，默认值为：`"inline"`|控制卡的显示方式|1.0
|**style**|`object`| 否，默认值为：`emphasis`|控制容器的样式设置|1.0
|**inlineTopMargin**|`integer`| 否，默认值为：`16`|显示卡片时需使用的边距|1.0


<a name="schema-spacingsconfig"></a>
## <a name="spacingsconfig"></a>SpacingsConfig

控制元素的布局方式

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**small**|`integer`| 否，默认值为：`3`|小间距值|1.0
|**default**|`integer`| 否，默认值为：`8`|默认间距值|1.0
|**medium**|`integer`| 否，默认值为：`20`|中间距值|1.0
|**large**|`integer`| 否，默认值为：`30`|大间距值|1.0
|**extraLarge**|`integer`| 否，默认值为：`40`|超大间距值|1.0
|**padding**|`integer`| 否，默认值为：`20`|填充值|1.0


<a name="schema-textblockconfig"></a>
## <a name="textblockconfig"></a>TextBlockConfig

控制文本显示的参数

|属性|在任务栏的搜索框中键入|必需|描述|版本|
|--------|----|--------|-----------|-------|
|**size**|`string`| 否，默认值为：`"default"`|卡片未指定时需使用的字号|1.0
|**weight**|`string`| 否，默认值为：`"normal"`|卡片未指定时需使用的字体粗细|1.0
|**color**|`string`| 否，默认值为：`"default"`|卡片未指定时需使用的字体颜色|1.0
|**isSubtle**|`boolean`| 否，默认值为：`false`|卡片未指定时文本是否为细微|1.0
|**wrap**|`boolean`| 否，默认值为：`true`|卡片未指定时文本是否换行|1.0
|**maxWidth**|`integer`| 否，默认值为：`0`|卡片未指定时要使用的最大宽度|1.0
