---
title: 实现呈现器
author: matthidinger
ms.author: mahiding
ms.date: 09/15/2017
ms.topic: article
ms.openlocfilehash: 3c79d768d5c979626b66614a1856ad6c2e390805
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552549"
---
# <a name="adaptive-card-renderer-specification"></a>自适应卡呈现器规范

以下规范介绍如何实现在任何 UI 平台上的自适应卡呈现器。

> [!IMPORTANT]
> 
> 此内容尚未完成。 请稍后查看。

## <a name="sdk-versioning"></a>SDK 版本控制

1. SDK 的主要和次要版本**应该**匹配`schema`版本。 
1. 修补程序/build**应该**用于呈现器没有架构更改的更新。

## <a name="parsing-json"></a>分析 JSON

### <a name="error-conditions"></a>错误条件
1. 一个分析器**必须**检查它是否是有效的 JSON 内容
1. 一个分析器**必须**根据架构 （必需的属性，等等） 进行验证
1. 上述错误**必须**报告给主机应用程序 （异常或权限相同者）

### <a name="unknown-types"></a>未知的类型
1. 如果遇到未知"类型"他们**必须先删除**从结果
1. 有效负载 （例如，上面） 的任何变更**应该**被报告为警告记录到主机应用程序

### <a name="unknown-properties"></a>未知的属性
1. 一个分析器**必须**包括**其他**元素上的属性

### <a name="additional-considerations"></a>其他注意事项
1. `speak`属性可能包含 SSML 标记和**必须**返回到指定为主机应用程序

## <a name="parsing-host-config"></a>分析主机配置
1. TODO

## <a name="versioning"></a>版本控制

1. 呈现器**必须**实现了特定架构版本。 
1. `AdaptiveCard`构造函数**必须**提供`version`属性默认值基于当前的架构版本 
1. 如果呈现器遇到`version`中的属性`AdaptiveCard`高于受支持的版本，它**必须**返回`fallbackText`相反。

## <a name="rendering"></a>呈现

`AdaptiveCard`组成`body`和`actions`。 `body`是一系列`CardElement`s，呈现器将枚举并按顺序呈现。 

1. 每个元素**必须**拉伸到其父项的宽度 (认为`display: block`以 html 格式)。
1. 呈现器**必须**忽略未知的元素类型，并继续呈现有效负载的其余部分。

### <a name="spacing-and-separators"></a>间距和分隔符

1. `spacing`上的每个元素的属性会影响之间的空间量**当前**元素和一个**BEFORE**它。
1. 间距**必须仅**应用存在实际上是其前面的元素时。 （例如，不会应用于数组中的第一项）
1. 呈现器**必须**查找要使用的空间量`hostConfig`应用于当前元素的枚举值的间距。
1. 如果元素具有`separator`的值`true`，然后可见的行**必须**当前元素与前一个之间绘制。
1. 分隔线**必须**将使用绘制`container.style.default.foregroundColor`。
1. 分隔符**必须仅**如果绘制该项**IS NOT**数组中的第一个。

### <a name="columns"></a>列

1. `Column` `width` **必须**解释按"auto"、"stretch"或加权的比率。

### <a name="textblock"></a>TextBlock

1. TextBlock**必须**占用单个行，除非`wrap`属性是`true`。 
1. 文本块**应该**剪裁带省略号 （...） 的任何多余文本

#### <a name="markdown"></a>Markdown

1. 自适应卡允许对 Markdown 的子集并**应该**中支持`TextBlock`。 
1. 请参阅完整[markdown 要求](../authoring-cards/text-features.md)

#### <a name="formatting-functions"></a>格式设置函数

1. `TextBlock` 允许[日期/时间格式设置函数](../authoring-cards/text-features.md)的**必须**上每个呈现器支持。
1. **所有故障必须**卡中显示的原始字符串。 尝试无友好消息。 （要使开发人员立即知道存在的目标是问题）

1. TODO:包含正则表达式

### <a name="images"></a>映像

1. 呈现器**应该**允许主机应用程序知道所有 HTTP 映像都下载时和卡是"完全 rendererd"
1. 呈现器**必须**检查主机配置`maxImageSize`param 时下载 HTTP 图像
1. 呈现器**必须**支持`.png`和 `.jpeg`
1. 呈现器**应该**支持`.gif`映像

### <a name="host-config"></a>主机配置

* TODO:默认值应该是什么？ 它们都应共享它？ 我们应在二进制文件中嵌入常见的 hostConfig.json 文件？
* TODO:我认为 HostConfig 需要进行版本控制也用于分析？

[`HostConfig`](host-config.md) 是一个共享的配置对象，指定如何为自适应的卡片呈现器生成 UI。  

这样，是平台不可知的在不同平台和设备上的呈现器之间共享的属性。 它还允许工具创建这您的卡外观和感觉会为给定的环境。

1. 呈现器**必须**公开**主机配置**托管应用程序的参数
1. 所有元素**必须**根据其各自的主机配置设置来设置样式

### <a name="native-platform-styling"></a>本机平台样式设置

1. 每个元素类型**应该**附加本机平台样式与生成的 UI 元素。 例如，在 HTML 中我们添加了一个 CSS 类的元素类型，并在 XAML 中我们将分配特定样式。

## <a name="extensibility"></a>扩展性 

1. 呈现器**必须**允许重写默认元素呈现器的主机应用程序。 例如，替换`TextBlock`呈现具有其自己的逻辑。
1. 呈现器**必须**允许注册自定义元素类型的主机应用程序。 例如，添加对自定义支持`Rating`元素
1. 呈现器**必须**允许删除默认元素对的支持的主机应用程序。 例如，删除`Action.Submit`如果他们不想让它支持。

## <a name="actions"></a>操作

1. 如果 HostConfig`supportsInteractivity`是`false`，将呈现器**不得**呈现的任何操作。
1. `actions`属性**必须**呈现为某种类型的操作栏中，通常是在卡的底部中的按钮。 
1. 点击按钮时它**必须**允许主机应用程序以处理事件。 
1. 事件**必须**与操作的所有关联属性一起传递
1. 事件**必须**传递`AdaptiveCard`执行所用

操作 | 行为
--- | ---
**Action.OpenUrl** | 打开外部 URL 以进行查看
**Action.ShowCard** | 请求子卡以向用户显示。
**Action.Submit** | 要求所有的输入元素收集到的对象，然后将它发送给你通过主机应用程序定义的一些方法。

### <a name="actionopenurl"></a>Action.OpenUrl
1. `Action.OpenUrl` **应**打开使用本机平台机制的 URL
1. 如果无法做到这一点它**必须**事件引发到主机应用程序以处理打开 URL。 此事件**必须**允许主机应用程序以重写默认行为。 例如，让他们打开自己的应用中的 URL。

### <a name="actionshowcard"></a>Action.ShowCard

1. `Action.ShowCard` **必须**以某种方式，根据 hostConfig 设置支持。 有两种模式： 以内联方式和弹出窗口。 内联卡**应该**自动切换卡可见性。 在弹出窗口模式下，事件**应该**触发到主机应用程序，以某种方式显示的卡片。

### <a name="actionsubmit"></a>Action.Submit

提交操作的行为类似于 HTML 窗体提交，则这些不同之处在于 HTML 通常触发 HTTP post，自适应卡最多保留它意味着每个主机应用程序，以确定什么"提交"。 

1. 当这**必须**引发事件的用户点击操作 invokved。  
1. `data`属性**必须**包含回调有效负载中。
1. 有关`Action.Submit`，将呈现器**必须**收集在卡上的所有输入，并检索其值。 

### <a name="selectaction"></a>selectAction

1. 如果主机配置`supportedInteractivity`是`false`则`selectAction`**不得**触摸目标的方式进行呈现。
1. `Image``ColumnSet`，并`Column`提供`selectAction`属性，其中**应该**用户调用，例如，通过点击该元素时要执行。

## <a name="inputs"></a>输入

1. 如果 HostConfig`supportsInteractivity`是`false`呈现器**不得**呈现任何输入。
2. 输入**应该**可能用最高的保真度呈现。 例如，`Input.Date`理想情况下将日期选取器提供给用户，但如果这不是您的 UI 堆栈，则呈现器可能**必须**故障回复到呈现标准文本框。
3. 呈现器**应该**显示`placeholderText`在可能的情况
4. 呈现器**不**必须实现的输入验证。 自适应卡的用户必须规划以验证其端上的所有接收的数据。
5. 输入值绑定**必须**正确转义

6. 该对象**必须**返回到主机应用程序，如下所示：

   我们没有使接收方以正确分析的响应取决于自适应卡中进行输入验证任何承诺。 例如，Input.Number 可能返回"你好"，并且他们需要作好准备。


## <a name="events"></a>事件

1. 呈现器**应该**激发事件时已更改元素的可见性，允许主机应用程序向卡滚动到位。
