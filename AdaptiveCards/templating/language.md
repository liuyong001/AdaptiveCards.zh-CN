---
title: 自适应卡片模板语言
author: matthidinger
ms.author: mahiding
ms.date: 05/18/2020
ms.topic: article
ms.openlocfilehash: c03ed2c18039d199f37b9cbd52814f4561dad199
ms.sourcegitcommit: 65b792d73c264c943036343e05b75f2b0488e6e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "95001854"
---
# <a name="adaptive-cards-template-language"></a>自适应卡片模板语言

模板化可以将自适应卡片中的 **数据** 与 **布局** 分开。 模板语言是用于创作模板的语法。 

> 有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)

> [!IMPORTANT] 
> 
> **2020 年 5 月候选发布版本** 中的 **中断性变更**
>
> 我们正在努力工作，力求尽早发布模板，我们已经在做最后的冲刺了！ 发布之前，我们需要进行一些小的中断性变更。

## <a name="breaking-changes-as-of-may-2020"></a>2020 年 5 月起的中断性变更

1. 绑定语法已从 `{...}` 更改为 `${...}`
    * 例如：`"text": "Hello {name}"` 变为 `"text": "Hello ${name}"`
    
## <a name="binding-to-data"></a>绑定到数据

编写模板非常简单，只需要将卡片的“非静态”内容替换为“绑定表达式”即可。

### <a name="static-card-payload"></a>静态卡片有效负载

```json
{
   "type": "TextBlock",
   "text": "Matt"
}
```

### <a name="template-payload"></a>模板有效负载

```json
{
   "type": "TextBlock",
   "text": "${firstName}"
}
```

* 任何存在静态内容的地方几乎都可以放置绑定表达式
* 绑定语法以 `${` 开头，以 `}` 结尾。 例如 `${myProperty}`
* 使用点表示法访问对象层次结构的子对象。 例如 `${myParent.myChild}`
* 采用正常的 null 处理方式，可确保在访问对象图中的 null 属性时不会收到异常
* 使用索引器语法，按键或数组中的项检索属性。 例如 `${myArray[0]}`

## <a name="providing-the-data"></a>提供数据

有了模板后，需要提供数据，以得到完整的模板。 有两个选项可用来执行此操作：

1. **选项 A：在模板有效负载内执行内联**。 可以在 `AdaptiveCard` 模板负载中以内联方式提供数据。 为此，只需将 `$data` 特性添加到根 `AdaptiveCard` 对象即可。
2. **选项 B：作为单独的数据对象提供**。 如果选择此选项，则在运行时向[模板化 SDK](sdk.md) 提供两个单独的对象：`template` 和 `data`。 这是更常见的方法，因为通常的情况是创建一个模板，然后在以后提供动态数据。

### <a name="option-a-inline-data"></a>选项 A：内联数据

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
            "text": "Hi ${employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: ${employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: ${employee.peers[0].name}, ${employee.peers[1].name}, ${employee.peers[2].name}"
        }
    ]
}
```

### <a name="option-b-separating-the-template-from-the-data"></a>选项 B：将模板与数据分离

另外，还可以创建一个可反复使用的不含数据的卡片“模板”（可能性更高）。 此模板可以存储为文件并添加到源代码管理中。

**EmployeeCardTemplate.json**

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Hi ${employee.name}! Here's a bit about your org..."
        },
        {
            "type": "TextBlock",
            "text": "Your manager is: ${employee.manager.name}"
        },
        {
            "type": "TextBlock",
            "text": "3 of your peers are: ${employee.peers[0].name}, ${employee.peers[1].name}, ${employee.peers[2].name}"
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
var card = template.expand({
    $root: {
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
    }
});

// Now you have an AdaptiveCard ready to render!
```

## <a name="designer-support"></a>设计器支持

自适应卡片设计器已更新为支持模板化。 

> 试用网址： **[https://adaptivecards.io/designer](https://adaptivecards.io/designer)**

[![图像](https://user-images.githubusercontent.com/1432195/53214462-88d46980-3601-11e9-908d-253a1bb940a8.png)](https://adaptivecards.io/designer)

* **示例数据编辑器** - 在此处指定示例数据，以便在“预览模式”下查看数据绑定卡片。 此窗格中有一个小按钮，用于填充现有示例数据中的“数据结构”。
* **预览模式** - 按工具栏按钮即可在编辑体验和示例数据预览体验之间切换
* **打开示例** - 单击此按钮即可打开各种示例有效负载

## <a name="advanced-binding"></a>高级绑定

### <a name="binding-scopes"></a>绑定范围

可以通过几个保留关键字来访问各种绑定范围。 

```json
{
    "${<property>}": "Implicitly binds to `$data.<property>`",
    "$data": "The current data object",
    "$root": "The root data object. Useful when iterating to escape to parent object",
    "$index": "The current index when iterating"
}
```

### <a name="assigning-a-data-context-to-elements"></a>将数据上下文分配给元素

若要为任意元素分配“数据上下文”，请将 `$data` 属性添加到该元素。

```json
{
    "type": "Container",
    "$data": "${mySubObject}",
    "items": [
        {
            "type": "TextBlock",
            "text": "This TextBlock is now scoped directly to 'mySubObject': ${mySubObjectProperty}"
        },
        {
            "type": "TextBlock",
            "text": "To break-out and access the root data, use: ${$root}"
        }
    ]
}
```

## <a name="repeating-items-in-an-array"></a>数组中的重复项

* 如果将某个自适应卡片元素的 `$data` 属性绑定到 **数组**，则 **会针对数组中的每个项重复元素本身。** 
* 在属性值中使用的任何绑定表达式 (`${myProperty}`) 的作用域都将是数组中的 **单个项**。
* 如果绑定到字符串数组，请使用 `${$data}` 访问单个字符串元素。 例如 `"text": "${$data}"`

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
            "text": "${name}"
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

## <a name="built-in-functions"></a>内置函数

如果没有一整套丰富的帮助程序函数，则任何模板化语言都不是完整的。 自适应卡模板化建立在[自适应表达式语言](https://aka.ms/adaptive-expressions) (AEL) 的基础之上，后者是声明可在许多不同平台上进行计算的表达式的开放性标准。 而且它是“逻辑应用”的一个适当超集，因此可以使用与 Power Automate 等类似的语法。

**这只是一小部分内置函数的示例。**

查看[自适应表达式语言预生成函数](https://docs.microsoft.com/azure/bot-service/bot-builder-concept-adaptive-expressions?view=azure-bot-service-4.0)的完整列表。

### <a name="conditional-evaluation"></a>条件计算

* if(*表达式*, *trueValue*, *falseValue*)

**`if` 示例**

```json
{
    "type": "TextBlock",
    "color": "${if(priceChange >= 0, 'good', 'attention')}"
}
```

### <a name="parsing-json"></a>分析 JSON

* json(*jsonString*) - 分析 JSON 字符串

**`json` 示例**

这是 Azure DevOps 响应，其中的 `message` 属性是一个 JSON 序列化字符串。 若要访问字符串中的值，需要在模板中使用 `json` 函数。

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
    "text": "${json(message).releaseName}"
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

[模板化 SDK](sdk.md) 中通过 API 支持自定义函数。 

## <a name="conditional-layout-with-when"></a>使用 `$when` 的条件布局

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
            "$when": "${price > 30}",
            "text": "This thing is pricy!",
            "color": "attention",
        },
         {
            "type": "TextBlock",
            "$when": "${price <= 30}",
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
