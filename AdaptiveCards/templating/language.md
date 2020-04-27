---
title: 自适应卡片模板语言
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: ffd2ec065550f483bf602483eebf622565f7f47a
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82136173"
---
# <a name="adaptive-cards-template-language"></a>自适应卡片模板语言

模板化可以将自适应卡片中的**数据**与**布局**分开。 模板语言是用于创作模板的语法。 

> 有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)

> [!IMPORTANT] 
> 
> 这些功能为**预览版，可能会更改**。 我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。

创作模板时，可以使用 `AdaptiveCard` 有效负载以内联方式指定数据，也可以在运行时使用[模板化 SDK](sdk.md) 来这样做。

## <a name="specify-data-within-the-card"></a>指定卡片中的数据

若要直接在卡片有效负载中提供数据，只需将 `$data` 属性添加到 `AdaptiveCard` 即可（见下）。

## <a name="binding-to-the-data"></a>绑定到数据

可以绑定到卡片的 `body` 或 `actions` 中的数据。

* 绑定语法以 `{` 开头，以 `}` 结尾。 例如 `{myProperty}`
* 用于访问子对象的点表示法
* 索引器语法，用于按键或数组中的项检索属性
* 针对深层次结构的常规 null 处理
* 即将发布的转义符语法文档 

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

另外，还可以创建一个可反复使用的不含数据的卡片“模板”（可能性更高）。 此模板可以存储为文件并添加到源代码管理中。

**EmployeeCardTemplate.json**

```json
{
    "type": "AdaptiveCard",
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

然后，将其加载并使用 [模板化 SDK](sdk.md) 在运行时提供数据。

**JavaScript 示例**

使用 [adaptivecards-templating](https://npmjs.com/package/adaptivecards-templating) 包。

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

自适应卡片设计器已更新为支持模板化。 

> 试用网址： **[https://adaptivecards.io/designer](https://adaptivecards.io/designer)**

[![图像](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](https://adaptivecards.io/designer)

* **示例数据编辑器** - 在此处指定示例数据，以便在“预览模式”下查看数据绑定卡片。 此窗格中有一个小按钮，用于填充现有示例数据中的“数据结构”。
* **数据结构** - 这是示例数据的结构。 可以将字段拖到设计图面上，以便创建一个绑定，将内容绑定到这些字段 
* **预览模式** - 按工具栏按钮即可在编辑体验和示例数据预览体验之间切换
* **打开示例** - 单击此按钮即可打开各种示例有效负载

## <a name="advanced-binding"></a>高级绑定

### <a name="binding-scopes"></a>绑定范围

可以通过几个保留关键字来访问各种绑定范围。 

 注意：在预览版中，并非所有这些都得到了实现。

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

若要为任意元素分配“数据上下文”，请将 `$data` 属性添加到该元素。

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

此部分有点“晦涩”。 欢迎反馈。

* 如果将某个自适应卡片元素的 `$data` 属性绑定到**数组**，则**会针对数组中的每个项重复元素本身。** 
* 在属性值中使用的任何绑定表达式 (`{myProperty}`) 的作用域都将是数组中的**单个项**。
* 如果绑定到字符串数组，请使用 `{$data}` 访问单个字符串元素。 例如 `"text": "{$data}"`

举例来说，下面的 `TextBlock` 会重复 3 次，因为其 `$data` 是数组。 请注意 `text` 属性如何绑定到数组内单个对象的 `name` 属性。 

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

**结果：**

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

## <a name="functions"></a>函数

如果没有帮助程序函数，则任何模板化语言都不是完整的。 我们会提供一组可在每个 SDK 上使用的标准函数。 

此处的语法仍未确定，因此请稍后回来查看。不过，下面是我们所计划内容的开头：

### <a name="string-functions"></a>字符串函数

* substr
* indexOf（尚不能使用） 
* toUpper（尚不能使用） 
* toLower（尚不能使用） 

### <a name="number-functions"></a>数值函数

* 格式化（货币、小数等）（尚不能使用） 

### <a name="date-functions"></a>日期函数

* 分析众所周知的日期字符串格式（尚不能使用） 
* 针对众所周知的日期/时间表示方式进行格式设置（尚不能使用） 

### <a name="conditional-functions"></a>条件函数

* if(*表达式*, *trueValue*, *falseValue*)

**`if` 示例**

```json
{
    "type": "TextBlock",
    "color": "{if(priceChange >= 0, 'good', 'attention')}"
}
```

### <a name="data-manipulation"></a>数据操作

* JSON.parse - 分析 JSON 字符串的功能 

**`JSON.parse` 示例**

这是 Azure DevOps 响应，其中的 `message` 属性是一个 JSON 序列化字符串。 若要访问字符串中的值，需要在模板中使用 `JSON.parse` 函数。

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

**用法**

```json
{
    "type": "TextBlock",
    "text": "{JSON.parse(message).releaseName}"
}
```

**结果**

```json
{
    "type": "TextBlock",
    "text": "Release-104"
}
```

### <a name="custom-functions"></a>自定义函数

我们希望确保主机可以添加自定义函数。这意味着，如果某个函数不受支持，我们需要提供对回退支持的可靠支持。 我们仍在对此进行评估。

## <a name="conditional-layout"></a>条件布局

若要在满足条件时删除整个元素，请使用 `$when` 属性。 如果 `$when` 的计算结果为 `false`，则此元素不会显示给用户。

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

### <a name="composing-templates"></a>组合模板

目前不支持将模板“部件”组合到一起。 但是，我们会探索相关选项，希望不久就能为大家提供更多此方面的内容。 欢迎你在此提供自己的想法！


## <a name="examples"></a>示例

请浏览更新的[“示例”页](https://adaptivecards.io/samples)，其中包含各种新的模板化卡片。
