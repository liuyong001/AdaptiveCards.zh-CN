---
title: 卡架构
author: paulcam206
ms.author: paulcam
ms.date: 09/18/2018
ms.topic: reference
ms.openlocfilehash: 76a21affcd26798acb52e2bcf1168121838ed00a
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553719"
---
# <a name="card-schema"></a>卡架构

卡
   * [`AdaptiveCard`](#schema-adaptivecard) 自适应卡中的根元素。

卡元素
   * [`TextBlock`](#schema-textblock) -显示文本，允许控制字体大小、 宽度和颜色。
   * [`Image`](#schema-image) -显示图像。
   * [`Media`](#schema-media) -显示音频或视频内容的媒体播放器。
   * [`MediaSource`](#schema-mediasource) -定义为媒体元素的源

容器
   * [`Container`](#schema-container) -容器组合在一起的项。
   * [`ColumnSet`](#schema-columnset) -列集将一个区域划分为列，这允许要位于通过并行元素。
   * [`Column`](#schema-column) -定义属于列集的容器。
   * [`FactSet`](#schema-factset) -在 FactSet 元素以表格形式显示一组的事实 （即名称/值对）。
   * [`Fact`](#schema-fact) -以键/值对的形式介绍 FactSet 中的事实。
   * [`ImageSet`](#schema-imageset) -ImageSet 显示映像类似于库的集合。

操作
   * [`Action.OpenUrl`](#schema-action.openurl) -调用时，显示给定的 url 通过外部 web 浏览器或显示就地使用嵌入式的 web 浏览器中启动。
   * [`Action.Submit`](#schema-action.submit) -收集输入的字段、 合并与可选的数据字段，并将事件发送到客户端。 负责客户端确定如何处理这些数据。 例如：使用 BotFramework 智能机器人，客户端会将通过消息传送中的活动发送到智能机器人应用程序。
   * [`Action.ShowCard`](#schema-action.showcard) -定义 AdaptiveCard 以单击按钮或链接时不显示给用户。

输入
   * [`Input.Text`](#schema-input.text) -允许用户输入文本。
   * [`Input.Number`](#schema-input.number) -允许用户输入一个数字。
   * [`Input.Date`](#schema-input.date) -允许用户选择的日期。
   * [`Input.Time`](#schema-input.time) -允许用户选择的时间。
   * [`Input.Toggle`](#schema-input.toggle) -可使用户在两个选项之间进行选择。
   * [`Input.ChoiceSet`](#schema-input.choiceset) -允许用户输入一个选择。
   * [`Input.Choice`](#schema-input.choice) -介绍在 ChoiceSet 中使用的选择。

# <a name="cards"></a>卡

<a name="schema-adaptivecard"></a>
## <a name="adaptivecard"></a>AdaptiveCard

自适应卡中的根元素。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"AdaptiveCard"`|是|必须为`"AdaptiveCard"`。|1.0
|**actions**|`Action[]`| 否|要在卡的操作栏中显示的操作。|1.0
|**body**|`array[]`| 否|要在主卡区域中显示的卡元素。|1.0
|**selectAction**|`object`| 否|点击或选择卡时，将调用一个操作。 `Action.ShowCard` 不支持。|1.0
|**version**|`string`|是|此卡所需的架构版本。 如果客户端**较低**比此版本中，`fallbackText`将呈现。|1.0
|**fallbackText**|`string`| 否|显示当客户端不支持指定的版本的文本 （可能包含的 markdown）。|1.0
|**backgroundImage**|`string`| 否|若要使用为卡的背景图像。|1.0
|**speak**|`string`| 否|指定此整个卡应朗读的内容。 这是简单的文本或 SSML 片段。|1.0
|**lang**|`string`| 否|在卡中使用的两字母 ISO 639 1 语言。 用于本地化的任何日期/时间函数。|1.0


# <a name="card-elements"></a>卡元素

<a name="schema-textblock"></a>
## <a name="textblock"></a>TextBlock

显示文本，允许控制字体大小、 宽度和颜色。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**color**|`string`| 否|控制的颜色`TextBlock`元素。|1.0
|**horizontalAlignment**|`string`| 否，默认值： `"left"`|控制如何元素水平放置在其容器内。|1.0
|**isSubtle**|`boolean`| 否，默认值： `false`|如果`true`，显示稍有减弱不太突出显示的文本。|1.0
|**maxLines**|`number`| 否|指定要显示行的最的大数。|1.0
|size|`string`| 否|控制文本的大小。|1.0
|**text**|`string`|是|若要显示的文本。|1.0
|**type**|`"TextBlock"`|是|必须为`"TextBlock"`。|1.0
|**weight**|`string`| 否|控制的权重`TextBlock`元素。|1.0
|**wrap**|`boolean`| 否，默认值： `false`|如果`true`，允许文本换行。 否则，文本被截断。|1.0
|**id**|`string`| 否|与元素关联的唯一标识符。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-image"></a>
## <a name="image"></a>图像

显示图像。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**altText**|`string`| 否|描述图像的替换文字。|1.0
|**horizontalAlignment**|`string`| 否，默认值： `"left"`|控制如何元素水平放置在其容器内。|1.0
|**selectAction**|`object`| 否|将一个操作时调用`Image`点击或选择。 `Action.ShowCard` 不支持。|1.0
|size|`string`| 否，默认值： `"auto"`|控制图像的近似大小。 每个主机，物理尺寸将会有所不同。 指定`"auto"`真实映像维度或`"stretch"`以强制其填充容器。|1.0
|**style**|`string`| 否|控制如何将此`Image`显示。|1.0
|**type**|`"Image"`|是|必须为`"Image"`。|1.0
|**url**|`string`|是|图像的 URL。|1.0
|**id**|`string`| 否|与元素关联的唯一标识符。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-media"></a>
## <a name="media"></a>Media

显示音频或视频内容的媒体播放器。

#### <a name="introduced-in-version-11"></a>在版本 1.1 中引入

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"Media"`|是|必须为`"Media"`。|1.1
|**sources**|`object` `[]`| 否|若要尝试播放的媒体源的数组。|1.1
|**poster**|`string`| 否|若要在播放之前显示的图像的 URL。|1.1
|**altText**|`string`| 否|描述的音频或视频的备用文本。|1.1
|**id**|`string`| 否|与元素关联的唯一标识符。|1.1
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.1
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.1


<a name="schema-mediasource"></a>
## <a name="mediasource"></a>MediaSource

定义为媒体元素的源

#### <a name="introduced-in-version-11"></a>在版本 1.1 中引入

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**mimeType**|`string`|是|Mime 类型关联的媒体 (例如`"video/mp4"`)。|1.1
|**url**|`string`|是|媒体 URL。|1.1


# <a name="containers"></a>容器

<a name="schema-container"></a>
## <a name="container"></a>容器

容器组合在一起的项。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"Container"`|是|必须为`"Container"`。|1.0
|**items**|`array[]`|是|要在呈现的卡元素`Container`。|1.0
|**selectAction**|`object`| 否|将一个操作时调用`Container`点击或选择。 `Action.ShowCard` 不支持。|1.0
|**style**|`string`| 否|样式提示`Container`。|1.0
|**verticalContentAlignment**|`string`| 否，默认值： `"top"`|定义内容的对齐方式垂直在容器中。|1.1
|**id**|`string`| 否|与元素关联的唯一标识符。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-columnset"></a>
## <a name="columnset"></a>ColumnSet

列集将一个区域划分为列，这允许要位于通过并行元素。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**columns**|`Column[]`| 否|数组`Columns`划分到区域。|1.0
|**selectAction**|`object`| 否|将一个操作时调用`ColumnSet`点击或选择。 `Action.ShowCard` 不支持。|1.0
|**type**|`"ColumnSet"`|是|必须为`"ColumnSet"`。|1.0
|**id**|`string`| 否|与元素关联的唯一标识符。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-column"></a>
## <a name="column"></a>列

定义属于列集的容器。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**items**|`array[]`|是|要在中包含的卡元素`Column`。|1.0
|**selectAction**|`object`| 否|将一个操作时调用`Column`点击或选择。 `Action.ShowCard` 不支持。|1.0
|**style**|`string`| 否|样式提示`Column`。|1.0
|**width**|`string,number`| 否|`"auto"``"stretch"`，或一个表示列组中的列的相对宽度的数字。|1.0
|**type**|`"Column"`| 否|必须为`"Column"`。|1.0
|**id**|`string`| 否|与元素关联的唯一标识符。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-factset"></a>
## <a name="factset"></a>FactSet

FactSet 元素以表格形式显示一组的事实 （即名称/值对）。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**facts**|`Fact[]`|是|数组`Fact`s。|1.0
|**type**|`"FactSet"`|是|必须为`"FactSet"`。|1.0
|**id**|`string`| 否|与元素关联的唯一标识符。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-fact"></a>
## <a name="fact"></a>这一事实

描述为键/值对中的 FactSet 的事实。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"Fact"`| 否|&nbsp;|1.0
|**title**|`string`|是|这一事实的标题。|1.0
|**value**|`string`|是|事实的值。|1.0


<a name="schema-imageset"></a>
## <a name="imageset"></a>ImageSet

ImageSet 显示映像类似于库的集合。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**images**|`Image[]`|是|数组`Image`要显示的元素。|1.0
|**imageSize**|`string`| 否，默认值： `"auto"`|控制图像的近似大小。 每个主机，物理尺寸将会有所不同。 指定`"auto"`真实映像维度或`"stretch"`以强制其填充容器。|1.0
|**type**|`"ImageSet"`|是|必须为`"ImageSet"`。|1.0
|**id**|`string`| 否|与元素关联的唯一标识符。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


# <a name="actions"></a>操作

<a name="schema-action.openurl"></a>
## <a name="actionopenurl"></a>Action.OpenUrl

调用时，显示给定的 url 通过外部 web 浏览器或显示就地使用嵌入式的 web 浏览器中启动。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"Action.OpenUrl"`|是|必须为`"Action.OpenUrl"`。|1.0
|**title**|`string`|是|按钮或链接，表示此操作的标签。|1.0
|**iconUrl**|`string`| 否|要执行的操作与标题一起显示的可选图标|1.1
|**url**|`string`|是|要打开的 URL。|1.0


<a name="schema-action.submit"></a>
## <a name="actionsubmit"></a>Action.Submit

收集输入的字段、 合并与可选的数据字段，并将事件发送到客户端。 负责客户端确定如何处理这些数据。 例如：使用 BotFramework 智能机器人，客户端会将通过消息传送中的活动发送到智能机器人应用程序。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"Action.Submit"`|是|必须为`"Action.Submit"`。|1.0
|**title**|`string`|是|按钮或链接，表示此操作的标签。|1.0
|**iconUrl**|`string`| 否|要执行的操作与标题一起显示的可选图标|1.1
|**data**|`string,object`| 否|输入的字段将合并在一起的初始数据。 这些是实质上是隐藏属性。|1.0


<a name="schema-action.showcard"></a>
## <a name="actionshowcard"></a>Action.ShowCard

定义 AdaptiveCard 以单击按钮或链接时不显示给用户。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"Action.ShowCard"`|是|必须为`"Action.ShowCard"`。|1.0
|**title**|`string`|是|按钮或链接，表示此操作的标签。|1.0
|**iconUrl**|`string`| 否|要执行的操作与标题一起显示的可选图标|1.1
|**card**|`object`|是|自适应卡中的根元素。|1.0


# <a name="inputs"></a>输入

<a name="schema-input.text"></a>
## <a name="inputtext"></a>Input.Text

允许用户输入文本。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**id**|`string`|是|值的唯一标识符。 用于标识收集的输入执行提交操作。|1.0
|**isMultiline**|`boolean`| 否，默认值： `false`|如果`true`，允许多个输入行。|1.0
|**maxLength**|`number`| 否|若要收集的最大长度字符的提示 （可能会忽略某些客户端）。|1.0
|**placeholder**|`string`| 否|输入所需的说明。 当已不输入任何文本时显示。|1.0
|**style**|`string`| 否，默认值： `"text"`|样式提示`Input.Text`。|1.0
|**type**|`"Input.Text"`|是|必须为`"Input.Text"`。|1.0
|**value**|`string`| 否|此字段的初始值。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-input.number"></a>
## <a name="inputnumber"></a>Input.Number

允许用户输入一个数字。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**id**|`string`|是|值的唯一标识符。 用于标识收集的输入执行提交操作。|1.0
|**max**|`number`| 否|最大值 （可能会忽略某些客户端） 的提示。|1.0
|**min**|`number`| 否|最小值 （可能会忽略某些客户端） 的提示。|1.0
|**placeholder**|`string`| 否|输入所需的说明。 显示时不进行任何选择。|1.0
|**type**|`"Input.Number"`|是|必须为`"Input.Number"`。|1.0
|**value**|`number`| 否|此字段的的初始值。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-input.date"></a>
## <a name="inputdate"></a>Input.Date

允许用户选择的日期。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**id**|`string`|是|值的唯一标识符。 用于标识收集的输入执行提交操作。|1.0
|**max**|`string`| 否|表示 ISO 8601 格式 （可能会忽略某些客户端） 的最大值的提示。|1.0
|**min**|`string`| 否|以 ISO-8601 格式 （可能会忽略某些客户端） 表示的最小值的提示。|1.0
|**placeholder**|`string`| 否|输入所需的说明。 显示时不进行任何选择。|1.0
|**type**|`"Input.Date"`|是|必须为`"Input.Date"`。|1.0
|**value**|`string`| 否|以 ISO-8601 格式表示此字段的初始值。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-input.time"></a>
## <a name="inputtime"></a>Input.Time

允许用户选择的时间。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**id**|`string`|是|值的唯一标识符。 用于标识收集的输入执行提交操作。|1.0
|**max**|`string`| 否|最大值 （可能会忽略某些客户端） 的提示。|1.0
|**min**|`string`| 否|最小值 （可能会忽略某些客户端） 的提示。|1.0
|**placeholder**|`string`| 否|输入所需的说明。 显示选择了没有时间时。|1.0
|**type**|`"Input.Time"`|是|必须为`"Input.Time"`。|1.0
|**value**|`string`| 否|以 ISO-8601 格式表示此字段的初始值。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-input.toggle"></a>
## <a name="inputtoggle"></a>Input.Toggle

可使用户在两个选项之间进行选择。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**id**|`string`|是|值的唯一标识符。 用于标识收集的输入执行提交操作。|1.0
|**title**|`string`|是|切换标题|1.0
|**type**|`"Input.Toggle"`|是|Input.Toggle|1.0
|**value**|`string`| 否，默认值： `"false"`|当前所选的值。 如果选定了项，将使用"valueOn"，否则为"valueOff"|1.0
|**valueOff**|`string`| 否，默认值： `"false"`|开关处于关闭状态时的值|1.0
|**valueOn**|`string`| 否，默认值： `"true"`|切换为开时，值|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-input.choiceset"></a>
## <a name="inputchoiceset"></a>Input.ChoiceSet

允许用户输入一个选择。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**选择**|`Input.Choice[]`|是|`Choice` 选项。|1.0
|**id**|`string`|是|值的唯一标识符。 用于标识收集的输入执行提交操作。|1.0
|**isMultiSelect**|`boolean`| 否，默认值： `false`|允许多个要选择的选项。|1.0
|**style**|`string`| 否，默认值： `"compact"`|样式提示`Input.ChoiceSet`。|1.0
|**type**|`"Input.ChoiceSet"`|是|必须为`"Input.ChoiceInput"`。|1.0
|**value**|`string`| 否|最初的选择 （或组选择），应处于选中状态。 以进行多重选择，指定值的逗号分隔的字符串。|1.0
|**spacing**|`string`| 否|控制此元素与前面的元素之间的间距的大小。|1.0
|**separator**|`boolean`| 否，默认值： `false`|当`true`，绘制一条分隔线顶部的元素。|1.0


<a name="schema-input.choice"></a>
## <a name="inputchoice"></a>Input.Choice

介绍在 ChoiceSet 中使用的选择。

|属性|在任务栏的搜索框中键入|必需|描述|Version|
|--------|----|--------|-----------|-------|
|**type**|`"Input.Choice"`| 否|&nbsp;|1.0
|**title**|`string`|是|若要显示的文本。|1.0
|**value**|`string`|是|选择原始值。 **注意：** 不要使用`,`在值中，由于`ChoiceSet`与`isMultiSelect`设置为`true`返回的所选值的以逗号分隔的字符串。|1.0
