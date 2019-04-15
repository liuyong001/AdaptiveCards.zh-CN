---
title: 自适应卡 HostConfig
author: paulcam206
ms.author: paulcam
ms.date: 09/18/2018
ms.topic: reference
ms.openlocfilehash: 46ba9987cf162e95ab86dcdafa55e10df29b1121
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552589"
---
# <a name="what-is-hostconfig"></a>什么是 HostConfig？
`HostConfig` 是**跨平台配置对象**，它指定如何为自适应的卡片呈现器生成 UI。

这样，是平台不可知的在不同平台和设备上的呈现器之间共享的属性。 它还允许工具创建这您的卡外观和感觉会为给定的环境。

查看示例[HostConfig.json](https://github.com/Microsoft/AdaptiveCards/blob/master/samples/HostConfig/sample.json)若要获取其内容的缘由。

---

   * [`AdaptiveCardConfig`](#schema-adaptivecardconfig) -Toplevel 选项 `AdaptiveCards`
   * [`ActionsConfig`](#schema-actionsconfig) -选项`Action`s
   * [`ContainerStylesConfig`](#schema-containerstylesconfig) 的设置容器样式的默认实例和焦点控件
   * [`FactSetConfig`](#schema-factsetconfig) -控制是否显示`FactSet`s
   * [`FontSizesConfig`](#schema-fontsizesconfig) -控制不同的文本样式的字体大小度量值
   * [`FontWeightsConfig`](#schema-fontweightsconfig) -控制字体粗细指标
   * [`ForegroundColorsConfig`](#schema-foregroundcolorsconfig) -控制各种字体颜色
   * [`ImageSetConfig`](#schema-imagesetconfig) -控制如何`ImageSet`显示
   * [`ImageSizesConfig`](#schema-imagesizesconfig) -控制`Image`大小
   * [`MediaConfig`](#schema-mediaconfig) -控制显示和行为的`Media`元素
   * [`SeparatorConfig`](#schema-separatorconfig) -控制分隔符的显示方式
   * [`ShowCardConfig`](#schema-showcardconfig) -控制行为和样式 `Action.ShowCard`
   * [`SpacingsConfig`](#schema-spacingsconfig) -控制元素的方式进行布局
   * [`TextBlockConfig`](#schema-textblockconfig) -参数控制中文本的显示

# <a name="card-configuration"></a>卡配置

<a name="schema-adaptivecardconfig"></a>
## <a name="adaptivecardconfig"></a>AdaptiveCardConfig

Toplevel 选项 `AdaptiveCards`

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**allowCustomStyle**|`boolean`| 否，默认值： `true`|控制是否允许自定义样式|1.0
|**supportsInteractivity**|`boolean`| 否，默认值： `true`|控制是否交互式`Action`被允许进行调用|1.0
|**imageBaseUrl**|`string`| 否|加载资源时要使用的基 URL|1.0
|**fontFamily**|`string`| 否，默认值： `"Calibri"`|若要呈现文本时所使用的字体|1.0
|**actions**|`object`| 否|选项为`Action`s|1.0
|**adaptiveCard**|`object`| 否|Toplevel 选项 `AdaptiveCards`|1.0
|**containerStyles**|`object`| 否|设置容器样式的默认实例和焦点的控件|1.0
|**imageSizes**|`object`| 否|控件`Image`大小|1.0
|**imageSet**|`object`| 否|控件如何`ImageSet`显示|1.0
|**factSet**|`object`| 否|控制是否显示`FactSet`s|1.0
|**fontSizes**|`object`| 否|不同的文本样式的控件的字体大小度量值|1.0
|**fontWeights**|`object`| 否|控件的字体粗细指标|1.0
|**spacing**|`object`| 否|控制元素的方式进行布局|1.0
|**separator**|`object`| 否|控制分隔符的显示方式|1.0
|**media**|`object`| 否|控制显示和行为的`Media`元素|1.1


<a name="schema-actionsconfig"></a>
## <a name="actionsconfig"></a>ActionsConfig

选项为`Action`s

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**actionsOrientation**|`string`| 否，默认值： `"horizontal"`|控制按钮的布局方式|1.0
|**actionAlignment**|`string`| 否，默认值： `"stretch"`|按钮的控件布局|1.0
|**buttonSpacing**|`integer`| 否，默认值： `10`|控制之间使用多少间距按钮|1.0
|**maxActions**|`integer`| 否，默认值： `5`|控制在总计中允许多少操作|1.0
|**spacing**|`string`| 否，默认值： `"default"`|总体操作元素的间距的控件|1.0
|**showCard**|`object`| 否|控件的行为和样式 `Action.ShowCard`|1.0
|**iconPlacement**|`string`| 否，默认值： `"aboveTitle"`|控制在何处放置操作图标|1.0
|**iconSize**|`integer`| 否，默认值： `30`|控件大小的操作图标|1.0


<a name="schema-containerstylesconfig"></a>
## <a name="containerstylesconfig"></a>ContainerStylesConfig

设置容器样式的默认实例和焦点的控件

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**默认**|`object`| 否|默认容器样式|1.0
|**emphasis**|`object`| 否|用于强调的容器样式|1.0


<a name="schema-factsetconfig"></a>
## <a name="factsetconfig"></a>FactSetConfig

控制是否显示`FactSet`s

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**title**|`object`| 否，默认值： `{"weight":"bolder","size":"default","color":"default","isSubtle":false,"wrap":true,"maxWidth":150}`|参数控制中文本的显示|1.0
|**value**|`object`| 否，默认值： `{"weight":"default","size":"default","color":"default","isSubtle":false,"wrap":true,"maxWidth":0}`|参数控制中文本的显示|1.0
|**spacing**|`integer`| 否，默认值： `10`|&nbsp;|1.0


<a name="schema-fontsizesconfig"></a>
## <a name="fontsizesconfig"></a>FontSizesConfig

不同的文本样式的控件的字体大小度量值

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**small**|`integer`| 否，默认值： `10`|很小的字体大小|1.0
|**默认**|`integer`| 否，默认值： `12`|默认字体大小|1.0
|**medium**|`integer`| 否，默认值： `14`|中等字体大小|1.0
|**large**|`integer`| 否，默认值： `17`|大字体大小|1.0
|**extraLarge**|`integer`| 否，默认值： `20`|特大规模字体大小|1.0


<a name="schema-fontweightsconfig"></a>
## <a name="fontweightsconfig"></a>FontWeightsConfig

控件的字体粗细指标

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**lighter**|`integer`| 否，默认值： `200`|&nbsp;|1.0
|**默认**|`integer`| 否，默认值： `400`|&nbsp;|1.0
|**bolder**|`integer`| 否，默认值： `800`|&nbsp;|1.0


<a name="schema-foregroundcolorsconfig"></a>
## <a name="foregroundcolorsconfig"></a>ForegroundColorsConfig

控制各种字体颜色

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**默认**|`object`| 否，默认值： `{"default":"#FF000000","subtle":"#B2000000"}`|&nbsp;|1.0
|**accent**|`object`| 否，默认值： `{"default":"#FF0000FF","subtle":"#B20000FF"}`|&nbsp;|1.0
|**dark**|`object`| 否，默认值： `{"default":"#FF101010","subtle":"#B2101010"}`|&nbsp;|1.0
|**light**|`object`| 否，默认值： `{"default":"#FFFFFFFF","subtle":"#B2FFFFFF"}`|&nbsp;|1.0
|**good**|`object`| 否，默认值： `{"default":"#FF008000","subtle":"#B2008000"}`|&nbsp;|1.0
|**warning**|`object`| 否，默认值： `{"default":"#FFFFD700","subtle":"#B2FFD700"}`|&nbsp;|1.0
|**attention**|`object`| 否，默认值： `{"default":"#FF8B0000","subtle":"#B28B0000"}`|&nbsp;|1.0


<a name="schema-imagesetconfig"></a>
## <a name="imagesetconfig"></a>ImageSetConfig

控件如何`ImageSet`显示

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**imageSize**|`string`| 否，默认值： `"auto"`|控件单独的图像大小调整|1.0
|**maxImageHeight**|`integer`| 否，默认值： `100`|将限制为此值的图像高度|1.0


<a name="schema-imagesizesconfig"></a>
## <a name="imagesizesconfig"></a>ImageSizesConfig

控件`Image`大小

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**small**|`integer`| 否，默认值： `80`|小图像大小值|1.0
|**medium**|`integer`| 否，默认值： `120`|中图像大小值|1.0
|**large**|`integer`| 否，默认值： `180`|大图像大小值|1.0


<a name="schema-mediaconfig"></a>
## <a name="mediaconfig"></a>MediaConfig

控制显示和行为的`Media`元素

#### <a name="introduced-in-version-11"></a>在版本 1.1 中引入

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**defaultPoster**|`string`| 否|未调用播放按钮时要显示图像的 URI|1.1
|**playButton**|`string`| 否|若要按播放按钮显示的图像|1.1
|**allowInlinePlayback**|`boolean`| 否，默认值： `true`|是否要显示媒体内联或外部调用|1.1


<a name="schema-separatorconfig"></a>
## <a name="separatorconfig"></a>SeparatorConfig

控制分隔符的显示方式

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**lineThickness**|`integer`| 否，默认值： `1`|分隔线的粗细|1.0
|**lineColor**|`string,null`| 否，默认值： `#B2000000`|要绘制分隔线时使用的颜色|1.0


<a name="schema-showcardconfig"></a>
## <a name="showcardconfig"></a>ShowCardConfig

控件的行为和样式 `Action.ShowCard`

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**actionMode**|`string`| 否，默认值： `"inline"`|控制卡的显示方式|1.0
|**style**|`object`| 否，默认值： `emphasis`|容器的控件样式设置|1.0
|**inlineTopMargin**|`integer`| 否，默认值： `16`|要显示在卡时使用的边距|1.0


<a name="schema-spacingsconfig"></a>
## <a name="spacingsconfig"></a>SpacingsConfig

控制元素的方式进行布局

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**small**|`integer`| 否，默认值： `3`|小间距值|1.0
|**默认**|`integer`| 否，默认值： `8`|默认间距值|1.0
|**medium**|`integer`| 否，默认值： `20`|中等间距值|1.0
|**large**|`integer`| 否，默认值： `30`|大型间距值|1.0
|**extraLarge**|`integer`| 否，默认值： `40`|特大规模间距值|1.0
|**padding**|`integer`| 否，默认值： `20`|空白值|1.0


<a name="schema-textblockconfig"></a>
## <a name="textblockconfig"></a>TextBlockConfig

参数控制中文本的显示

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|size|`string`| 否，默认值： `"default"`|卡未指定时要使用的字体大小|1.0
|**weight**|`string`| 否，默认值： `"normal"`|卡未指定时要使用的字体粗细|1.0
|**color**|`string`| 否，默认值： `"default"`|卡未指定时要使用的字体颜色|1.0
|**isSubtle**|`boolean`| 否，默认值： `false`|应为文本细微如果不指定卡片|1.0
|**wrap**|`boolean`| 否，默认值： `true`|如果未指定卡时，文本换行应|1.0
|**maxWidth**|`integer`| 否，默认值： `0`|如果未指定卡片，请使用最大宽度|1.0
