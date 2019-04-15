---
title: 入门
author: matthidinger
ms.author: mahiding
ms.date: 11/9/2017
ms.topic: article
ms.openlocfilehash: 9d363da0c10b242e23d2594984292fcc1f31382f
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552679"
---
# <a name="getting-started"></a>入门 

自适应卡是一个 JSON 序列化卡对象模型。

## <a name="adaptive-card-structure"></a>自适应卡结构

卡片的基本结构是按如下所示：

* `AdaptiveCard` -根对象描述 AdaptiveCard 本身，包括其元素构成、 其操作、 如何应朗读它，以及呈现它所需的架构版本。
* `body` 的卡片正文组成的构建基块称为`elements`。 元素可以包含几乎无限的布局，以创建多个类型的卡中。 
* `actions` -许多数据卡也有一组用户可能在其执行的操作。 此属性描述了这些操作，这通常在底部"操作栏"中的呈现。

### <a name="example-card"></a>示例卡

此示例卡，其中包括单个跟图像的文本行。

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

每个元素都`type`标识何种类型的对象的属性。 查看上面的卡，可以看到我们有两个元素`TextBlock`和一个`Image`。

自适应卡的所有元素**垂直堆叠**并**扩展到其父级的宽度**(认为`display: block`以 html 格式)。 但是，可以使用`ColumnSet`若要创建的容器-同时列。

## <a name="adaptive-elements"></a>自适应元素

最基本的元素是：

* **TextBlock** -添加具有属性来控制文本如下所示的文本块
* **映像**-将使用属性来控制图像如下所示的图像添加

## <a name="container-elements"></a>容器元素

卡还可以排列子元素的集合的容器。

* **容器**-定义元素的集合
* **列集/列**-定义集合的列，每个列是一个容器
* **FactSet**的事实数据的容器
* **ImageSet** -容器的映像以便该 UI 可以显示相应照片库体验的映像集合。

## <a name="input-elements"></a>输入的元素

输入的元素允许您提出的本机 UI，以生成简单的窗体：

* **Input.Text** -从用户获取文本内容
* **Input.Date** -从用户获取日期
* **Input.Time** -从用户获取一次
* **Input.Number** -从用户获取一个数字
* **Input.ChoiceSet** -为用户提供的一组选项，并让他们选择
* **Input.Toggle** -为用户提供两个项之间的单个选择，并让他们选择

## <a name="actions"></a>操作

操作添加到卡片的按钮。 这些可执行各种操作，如打开 URL 或提交一些数据。

* **Action.OpenUrl** -此按钮将打开外部 URL 以进行查看
* **Action.ShowCard** -请求子卡以向用户显示。
* **Action.Submit** -输入元素的所有要求，以便收集到的对象，然后将它发送给你通过主机应用程序定义的一些方法。

> **示例 Action.Submit**:使用 Skype，Action.Submit 将发送 Bot Framework 机器人活动回复到智能机器人**值**包含对它的输入数据的所有对象的属性。

## <a name="learn-more"></a>了解详细信息

* [浏览示例卡](http://adaptivecards.io/samples/)激发灵感
* 使用[架构资源管理器](http://adaptivecards.io/explorer)浏览可用元素
* 生成卡使用[交互式可视化工具](http://adaptivecards.io/visualizer/)
* [与我们联系](http://adaptivecards.io/connect)与你有任何反馈
