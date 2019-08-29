---
title: 自适应卡模板语言
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: 993618ed94eaea1a004c7893a5a3927c0d818cd6
ms.sourcegitcommit: a16f53ba10a8607deacde5c8cc78927cac58657c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68878894"
---
# <a name="adaptive-cards-template-language"></a>自适应卡模板语言

模板化可将**数据**与自适应卡中的**布局**分离。 模板语言是用于创作模板的语法。 

> 有关[自适应卡模板的概述](index.md), 请阅读此概述

> [!IMPORTANT] 
> 
> 这些功能**处于预览阶段, 可能会有所更改**。 你的反馈不仅是欢迎的, 而且确保我们能够提供**所**需的功能至关重要。

创作模板时, 可以使用`AdaptiveCard`有效负载或在运行时使用[模板化 sdk](sdk.md)来指定数据。

## <a name="specify-data-within-the-card"></a>指定卡片内的数据

若要直接在卡有效负载中提供数据, 只`$data`需将属性`AdaptiveCard`添加到 (见下文)。

## <a name="binding-to-the-data"></a>绑定到数据

您可以绑定到卡`body`或`actions`卡中的数据。

* 绑定语法以开头`{` , 以`}`结尾。 例如,`{myProperty}`
* 用点表示法访问子对象
* 索引器语法, 用于按键或数组中的项检索属性
* 对于深层层次结构的宽容 null 处理
* *即将推出语法文档*

```json
{
    "type": "AdaptiveCard",
    "$data": {
        "employee": {
            "name": "Matt",
            "manager": { "name": "Thomas" },
            "peers": [{
                "name": "Andrew" 
            }, { 
                "name": "Lei"
            }, { 
                "name": "Mary Anne"
            }, { 
                "name": "Adam"
            }]
        }
    },
    "body": [
        {
            "type": "TextBlock",
            "text": "Hi {employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: {employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: {employee.peers[0].name}, {employee.peers[1].name}, {employee.peers[2].name}"
        }
    ]
}
```

## <a name="separating-the-template-from-the-data"></a>将模板与数据分离

另外, 您还可以创建一个重新使用的卡 "模板", 而不包含数据。 此模板可以存储为文件并添加到源代码管理中。

**EmployeeCardTemplate**

```json
{
    "type": "AdaptivCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Hi {employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: {employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: {employee.peers[0].name}, {employee.peers[1].name}, {employee.peers[2].name}"
        }
    ]
}
```

然后, 使用[模板化 sdk](sdk.md)加载它并在运行时提供数据。

**JavaScript 示例**

使用[adaptivecards 模板](https://npmjs.com/package/adaptivecards-templating)包。

```js
var template = new ACData.Template({ 
    // EmployeeCardTemplate goes here
});

// Specify data at runtime
var dataContext = new ACData.EvaluationContext();
dataContext.$root = {
    "employee": {
        "name": "Matt",
        "manager": { "name": "Thomas" },
        "peers": [{
            "name": "Andrew" 
        }, { 
            "name": "Lei"
        }, { 
            "name": "Mary Anne"
        }, { 
            "name": "Adam"
        }]
    }
};

var card = template.expand(dataContext);
// Now you have an AdaptiveCard ready to render!
```

## <a name="designer-support"></a>设计器支持

自适应卡设计器已更新为支持模板化。 

> 试用以下位置的 "vnext" 预览版: **[https://vnext.adaptivecards.io/designer](https://vnext.adaptivecards.io/designer)**

[![影像](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](http://vnext.adaptivecards.io/designer)

 
此 "vnext" URL 将产生 bug, 并将频繁部署。 **清除缓存**以确保具有最新版本, 如果发现 bug, 请告诉我们!

* **示例数据编辑器**-在此处指定示例数据, 以在 "预览模式" 中查看数据绑定卡。 此窗格中有一个小按钮, 用于填充现有示例数据中的数据结构。
* **数据结构**-这是示例数据的结构。 可以将字段拖到设计图面上以创建对它们的绑定 
* **预览模式**-按工具栏按钮, 在编辑体验和示例数据预览体验之间切换
* **打开示例**-单击此按钮以打开各种示例负载

## <a name="advanced-binding"></a>高级绑定

### <a name="binding-scopes"></a>绑定范围

有几个保留关键字可用于访问各种绑定范围。 

*注意:* 并非所有这些都是在预览版中实现的。

```json
{
    "{<property>}": "Implicitly binds to `$data.<property>`",
    "$data": "The current data object",
    "$root": "The root data object. Useful when iterating to escape to parent object",
    "$index": "The current index when iterating",
    "$host": "Access properties of the host *(not working yet)*"
}
```

### <a name="assigning-a-data-context-to-elements"></a>将数据上下文分配给元素

若要为任何元素分配 "数据上下文", 请`$data`将属性添加到元素。

```json
{
    "type": "Container",
    "$data": "{mySubObject}",
    "items": [
        {
            "type": "TextBlock",
            "text": "This TextBlock is now scoped directly to 'mySubObject': {mySubObjectProperty}"
        },
        {
            "type": "TextBlock",
            "text": "To break-out and access the root data, use: {$root}"
        }
    ]
}
```

## <a name="repeating-items-in-an-array"></a>数组中的重复项

此部分是 "暗幻"。 欢迎提供反馈。

* 如果对象`$data`的属性设置为**数组**, 则**将为数组中的每个项重复该对象本身。** 
* 由于它是重复的, `$data`因此在属性绑定中使用的范围限定为数组中的**单个项**。

例如, `TextBlock`下面将重复三次, 因为`$data`它是一个数组。 请注意`text`属性如何绑定到数组内`name`单个对象的属性。 

```json
{
    "type": "Container",
    "items": [
        {
            "type": "TextBlock",
            "$data": [
                { "name": "Matt" }, 
                { "name": "David" }, 
                { "name": "Thomas" }
            ],
            "text": "{name}"
        }
    ]
}
```

**导致:**

```json
{
    "type": "Container",
    "items": [ 
        {
            "type": "TextBlock",
            "text": "Matt"
        },
        {
            "type": "TextBlock",
            "text": "David"
        }
        {
            "type": "TextBlock",
            "text": "Thomas"
        }
    ]
}
```

## <a name="functions"></a>Functions

无需一些 helper 函数即可完成任何模板化语言。 我们将提供一组可在每个 SDK 上使用的标准函数。 

此处的语法仍在无线上, 因此请立即回来查看, 但以下是我们所计划的入门:

### <a name="string-functions"></a>字符串函数

* substr
* indexOf *(尚未工作)*
* toUpper *(尚未工作)*
* toLower *(尚未工作)*

### <a name="number-functions"></a>Number 函数

* 格式 (货币、小数点等) *(尚未工作)*

### <a name="date-functions"></a>日期函数

* 正在分析众所周知的日期字符串格式 *(尚未处理)*
* 格式众所周知的日期/时间表示形式 *(尚未处理)*

### <a name="conditional-functions"></a>条件函数

* if (*expression*, *trueValue*, *falseValue*)

**`if`实例**

```json
{
    "type": "TextBlock",
    "color": "if(priceChange >= 0, 'good', 'attention')"
}
```

### <a name="data-manipulation"></a>数据操作

* JSON。分析-分析 JSON 字符串的能力 

**`JSON.parse`实例**

这是一个 Azure DevOps 响应, 其中`message`的属性为 JSON 序列化字符串。 若要访问字符串中的值, 需要在模板中使用`JSON.parse`函数。

**数据** 

```json
{
    "id": "1291525457129548",
    "status": 4,
    "author": "Matt Hidinger",
    "message": "{\"type\":\"Deployment\",\"buildId\":\"9542982\",\"releaseId\":\"129\",\"buildNumber\":\"20180504.3\",\"releaseName\":\"Release-104\",\"repoProvider\":\"GitHub\"}",
    "start_time": "2018-05-04T18:05:33.3087147Z",
    "end_time": "2018-05-04T18:05:33.3087147Z"
}
```

**使用情况**

```json
{
    "type": "TextBlock",
    "text": "{JSON.parse(message).releaseName}"
}
```

**导致**

```json
{
    "type": "TextBlock",
    "text": "Release-104"
}
```

### <a name="custom-functions"></a>自定义函数

我们希望确保主机可以添加自定义功能, 这意味着, 如果不支持某个函数, 我们需要提供对回退支持的可靠支持。 我们仍在评估这一点。

## <a name="conditional-layout"></a>条件布局

若要在满足条件时删除整个元素, 请使用`$when`属性。 如果`$when`计算结果`false`为, 则不会向用户显示该元素。

```json
{
    "type": "AdaptiveCard",
    "$data": {
        "price": "35"
    },
    "body": [
        {
            "type": "TextBlock",
            "$when": "{price > 30}",
            "text": "This thing is pricy!",
            "color": "attention",
        },
         {
            "type": "TextBlock",
            "$when": "{price <= 30}",
            "text": "Dang, this thing is cheap!",
            "color": "good"
        }
    ]
}
```

### <a name="composing-templates"></a>撰写模板

当前不支持组合模板 "部件"。 但我们会探索选项, 希望不久就能分享。 这里欢迎你的想法!


## <a name="examples"></a>示例

到目前为止, 我们仅创建了有限数量的示例, 但请查看此处以开始使用。

* 通过单击 "**打开示例**" 在[设计器](http://vnext.adaptivecards.io/designer)中加载示例
* 或者只是直接[浏览它们的目录](https://github.com/Microsoft/AdaptiveCards/tree/js/template-engine/samples/v2.0/Scenarios)