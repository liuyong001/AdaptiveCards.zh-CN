---
title: 入门
author: matthidinger
ms.author: mahiding
ms.date: 11/9/2017
ms.topic: article
ms.openlocfilehash: c9a0ad07ba5fefbcdc35239591c02fe0720b5b66
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454840"
---
# <a name="getting-started"></a>入门 

自适应卡片是进行了 JSON 序列化的卡片对象模型。

## <a name="adaptive-card-structure"></a>自适应卡片结构

卡片的基本结构如下：

* `AdaptiveCard` - 此根对象描述 AdaptiveCard 本身，包括其元素构成、其操作、其朗读方式，以及呈现它所需的架构版本。
* `body` - 卡片的主体由称为 `elements` 的构建基块组成。 元素有几乎无限的排列组合，因此可以创建许多类型的卡片。 
* `actions` - 许多卡片有一组可供用户在其上执行的操作。 此属性描述的那些操作通常在底部的“操作栏”中呈现。

### <a name="example-card"></a>示例卡片

此示例卡片包括单行文本和一张图像。

```json
{
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png"
        }
    ]
}
```

## <a name="type-property"></a>`Type` 属性

每个元素都有一个 `type` 属性，用于标识它是哪种类型的对象。 看看上面这张卡片，可以看到我们有两个元素：`TextBlock` 和 `Image`。

所有自适应卡片元素都会**垂直进行堆叠**，并**在受父项限制的情况下进行横向扩展**（这类似于 HTML 中的 `display: block`）。 不过，可以使用 `ColumnSet` 创建多个包含容器的并排列。

## <a name="adaptive-elements"></a>自适应元素

最基本的元素包括：

* **TextBlock** - 添加一个文本块，其包含的属性可以用来控制文本的外观
* **Image** - 添加一个图像，其包含的属性可以用来控制图像的外观

## <a name="container-elements"></a>容器元素

卡片也可以有容器，用于对一组子元素进行排列组合。

* **Container** - 定义一组元素
* **ColumnSet/Column** - 定义一组列，每个列都是一个容器
* **FactSet** - 事实容器
* **ImageSet** - 图像容器，方便 UI 针对一组图像显示相应的照片库体验。

## <a name="input-elements"></a>输入元素

可以通过输入元素要求本机 UI 构建简单的窗体：

* **Input.Text** - 从用户获取文本内容
* **Input.Date** - 从用户获取日期
* **Input.Time** - 从用户获取时间
* **Input.Number** - 从用户获取数字
* **Input.ChoiceSet** - 为用户提供一组选项供其选取
* **Input.Toggle** - 为用户提供一个在两个项之间进行切换的切换式选项供其选取

## <a name="actions"></a>“操作”

操作会将按钮添加到卡片上。 这些按钮可以执行多种操作，例如打开 URL 或提交某些数据。

* **Action.OpenUrl** - 按钮打开一个供查看的外部 URL
* **Action.ShowCard** - 请求一张显示给用户的子卡。
* **Action.Submit** - 要求将所有输入元素收集到一个对象中，然后通过主机应用程序定义的某个方法将该对象发送给你。

> **示例 Action.Submit**：使用 Skype 时，Action.Submit 会将 Bot Framework 机器人活动发送回机器人，其中的 **Value** 属性包含一个其上有所有输入数据的对象。

## <a name="learn-more"></a>了解详细信息

* [浏览示例卡片](http://adaptivecards.io/samples/)获取灵感
* 使用[架构资源管理器](http://adaptivecards.io/explorer)浏览可用元素
* 使用[交互式可视化工具](http://adaptivecards.io/visualizer/)构建一张卡片
* 如果你有任何反馈，请[联系我们](http://adaptivecards.io/connect)
