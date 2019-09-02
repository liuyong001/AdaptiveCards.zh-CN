---
title: 实现呈现器
author: matthidinger
ms.author: mahiding
ms.date: 09/15/2017
ms.topic: article
ms.openlocfilehash: b39493f82f3378e5a554abc6df890d6821869671
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67138020"
---
# <a name="adaptive-card-renderer-specification"></a>自适应卡片呈现器规范

以下规范介绍如何在任意 UI 平台上实现自适应卡片呈现器。

> [!IMPORTANT]
> 
> 此内容尚未完成。 请稍后再回来查看。

## <a name="sdk-versioning"></a>SDK 版本控制

1. SDK 主要版本和次要版本**应该**与 `schema` 版本匹配。 
1. 修补程序/内部版本**应该**用于没有架构更改的呈现器更新。

## <a name="parsing-json"></a>分析 JSON

### <a name="error-conditions"></a>错误条件
1. 分析器**必须**确保它是有效的 JSON 内容
1. 分析器**必须**按照架构要求（必需属性等）进行验证
1. **必须**向主机应用报告上述错误（异常或类似的内容）

### <a name="unknown-types"></a>未知类型
1. 如果遇到未知“类型”，**必须将其从结果中删除**
1. 对有效负载进行更改（如上所示）时，**应该**将其以警告形式报告给主机应用

### <a name="unknown-properties"></a>未知属性
1. 分析器**必须**包含元素的**其他**属性

### <a name="additional-considerations"></a>其他注意事项
1. `speak` 属性可能包含 SSML 标记，**必须**按指定要求返回到主机应用

## <a name="parsing-host-config"></a>分析主机配置
1. TODO

## <a name="versioning"></a>版本控制

1. 呈现器**必须**实施特定版本的架构。 
1. `AdaptiveCard` 构造函数**必须**根据当前架构版本为 `version` 属性提供默认值。 
1. 如果呈现器在 `AdaptiveCard` 中遇到的 `version` 属性高于支持的版本，则**必须**改为返回 `fallbackText`。

## <a name="rendering"></a>渲染

`AdaptiveCard` 包含 `body` 和 `actions`。 `body` 是可供呈现器按顺序枚举和呈现的 `CardElement` 的集合。 

1. 每个元素**必须**按父元素的宽度进行拉伸（类似于 HTML 中的 `display: block`）。
1. 呈现器**必须**忽略未知元素类型，继续呈现余下的有效负载。

### <a name="spacing-and-separators"></a>间距和分隔符

1. 每个元素的 `spacing` 属性影响**当前**元素和它**前面**的元素之间的空间量。
1. 应用间距的**前提**是它前面确实有一个元素。 （例如，间距不会应用到数组中的第一个项）
1. 呈现器**必须**从 `hostConfig` 间距查找要使用的空间量，以便将枚举值应用到当前元素。
1. 如果元素的 `separator` 值为 `true`，则**必须**在当前元素和它前面的元素之间绘制一条可见的线。
1. **必须**使用 `container.style.default.foregroundColor` 绘制此分隔线。
1. 绘制分隔符的**前提**是该项**不是**数组中的首项。

### <a name="columns"></a>列

1. `Column` `width` **必须**通过“自动”、“拉伸”或加权比率进行解释。

### <a name="textblock"></a>TextBlock

1. TextBlock **必须**占用一行，除非 `wrap` 属性为 `true`。 
1. 文本块**应该**使用省略号 (...) 裁剪多余的文本

#### <a name="markdown"></a>Markdown

1. 自适应卡片允许 Markdown 的子集，**应该**在 `TextBlock` 中受到支持。 
1. 请参阅完整的 [Markdown 要求](../authoring-cards/text-features.md)

#### <a name="formatting-functions"></a>格式设置函数

1. `TextBlock` 允许 [DATE/TIME 格式设置函数](../authoring-cards/text-features.md)，这些函数**必须**在每个呈现器上都受到支持。
1. **所有故障必须**在卡片中显示原始字符串。 未尝试友好消息。 （目的是让开发人员立即意识到存在问题）

1. TODO：包括 regex

### <a name="images"></a>映像

1. 呈现器**应该**让主机应用知道在什么时候所有 HTTP 图像已完成下载且卡片已“完全呈现”
1. 呈现器**必须**在下载 HTTP 图像时检查主机配置的 `maxImageSize` 参数
1. 呈现器**必须**支持 `.png` 和 `.jpeg`
1. 呈现器**应该**支持 `.gif` 图像

### <a name="host-config"></a>主机配置

* TODO：默认值应该是什么？ 它们是否都应该共享它？ 我们是否应该在二进制文件中嵌入通用的 hostConfig.json 文件？
* TODO：我认为也需要对 HostConfig 进行版本控制，以便进行分析，对不对？

[`HostConfig`](host-config.md) 是一个共享配置对象，用于指定自适应卡片呈现器生成 UI 的方式。  

这样，那些跨平台的属性就可以在不同平台和设备的呈现器中共享。 另外还可以创建工具，让你了解该卡片在给定环境下的外观。

1. 呈现器**必须**向主机应用公开 **Host Config** 参数
1. 所有元素都**必须**根据相应的 Host Config 设置进行样式设置

### <a name="native-platform-styling"></a>本机平台样式设置

1. 每个元素类型**应该**为生成的 UI 元素附加一个本机平台样式。 例如，在 HTML 中，我们为元素类型添加了一个 CSS 类，而在 XAML 中，我们会分配特定的样式。

## <a name="extensibility"></a>扩展性 

1. 呈现器**必须**允许主机应用重写默认的元素呈现器。 例如，将 `TextBlock` 呈现替换为自己的逻辑。
1. 呈现器**必须**允许主机应用注册自定义元素类型。 例如，添加对自定义 `Rating` 元素的支持
1. 呈现器**必须**允许主机应用删除对默认元素的支持。 例如，如果主机应用不希望支持 `Action.Submit`，则可将其删除。

## <a name="actions"></a>操作

1. 如果 HostConfig `supportsInteractivity` 为 `false`，则呈现器**不得**呈现任何操作。
1. `actions` 属性在某些类型的操作栏中**必须**呈现为按钮，这些按钮通常位于卡片底部。 
1. 当按钮受到点击时，**必须**允许主机应用处理该事件。 
1. 该事件**必须**将所有相关联的属性与操作一起传递。
1. 该事件**必须**传递已执行的 `AdaptiveCard`。

操作 | 行为
--- | ---
**Action.OpenUrl** | 打开要查看的外部 URL
**Action.ShowCard** | 请求一张显示给用户的子卡。
**Action.Submit** | 要求将所有输入元素收集到一个对象中，然后通过主机应用程序定义的某个方法将该对象发送给你。

### <a name="actionopenurl"></a>Action.OpenUrl
1. `Action.OpenUrl` **应该**使用本机平台机制打开一个 URL
1. 如果无法执行该操作，则**必须**引发一个事件，要求主机应用负责打开该 URL。 此事件**必须**允许主机应用重写默认行为。 例如，让它们在自己的应用中打开 URL。

### <a name="actionshowcard"></a>Action.ShowCard

1. `Action.ShowCard` **必须**获得某种方式的支持，具体取决于 hostConfig 设置。 有两种模式：内联和弹出窗口。 内联卡片**应该**自动切换卡片可见性。 在弹出窗口模式中，**应该**触发一个事件，要求主机应用以某种方式显示卡片。

### <a name="actionsubmit"></a>Action.Submit

提交操作的行为类似于 HTML 窗体提交，只是 HTML 通常触发一个 HTTP Post，而自适应卡片则让每个主机应用自行决定如何“提交”。 

1. 当此项**必须**引发一个事件时，用户需点击所调用的操作。  
1. `data` 属性**必须**包括在回调有效负载中。
1. 对于 `Action.Submit`，呈现器**必须**收集卡片上的所有输入并检索其值。 

### <a name="selectaction"></a>selectAction

1. 如果 HostConfig `supportedInteractivity` 为 `false`，则 `selectAction` **不得**呈现为触控目标。
1. `Image`、`ColumnSet` 和 `Column` 提供一个 `selectAction` 属性，当用户以某种方式（例如，点击该元素）调用该属性时，系统**应该**执行它。

## <a name="inputs"></a>输入

1. 如果 HostConfig `supportsInteractivity` 为 `false`，则呈现器**不得**呈现任何输入。
2. 输入的呈现**应该**尽可能采用高保真的形式。 例如，理想情况下，`Input.Date` 会为用户提供一个日期选取器，但如果不可能在 UI 堆栈上实现此功能，则呈现器**必须**退而求其次，呈现一个标准的文本框。
3. 可能情况下，呈现器**应该**显示 `placeholderText`
4. 呈现器**不**需对输入实施验证。 自适应卡片用户必须做好计划，在自己那一端验证任何接收的数据。
5. 输入值绑定**必须**进行正确的转义

6. 此对象**必须**返回到主机应用，如下所示：

   对于在自适应卡片中进行的输入验证，我们不做任何承诺，因此，接收方应该对响应进行适当的分析。 例如，Input.Number 可能返回“hello”，接收方需要做好相应的准备。


## <a name="events"></a>事件

1. 当某个元素的可见性变化时，呈现器**应该**触发一个事件，让主机应用将卡片滚动到相应位置。
