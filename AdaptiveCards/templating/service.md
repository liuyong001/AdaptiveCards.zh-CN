---
title: 自适应卡模板服务
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: 81d1e598b6157b6ba1fedbf458a7c624705afcd5
ms.sourcegitcommit: a16f53ba10a8607deacde5c8cc78927cac58657c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68878884"
---
# <a name="adaptive-cards-template-service"></a>自适应卡模板服务

自适应卡模板服务是一种概念证明服务, 它允许任何人查找、参与和共享一组众所周知的模板。

如果希望显示某些数据, 但不希望为其编写自定义的自适应卡, 则此方法非常有用。

> 有关[自适应卡模板的概述](index.md), 请阅读此概述

> [!IMPORTANT] 
> 
> *条款和协议* 
> 
> 此**alpha 级别**服务 "按原样" 提供, 并具有所有错误, 不支持任何方式。 从服务收集的任何数据都服从[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkID=824704)。
> 
> 这些功能**处于预览阶段, 可能会有所更改**。 你的反馈不仅是欢迎的, 而且确保我们能够提供**所**需的功能至关重要。

## <a name="how-does-the-service-help-me"></a>服务如何帮助我？

假设我只获取了一段数据, 可能是它的财务数据、Microsoft Graph 数据、schema.org 数据或来自我的组织中的自定义数据。 

现在, 我想向用户显示数据。 

过去, 这意味着在我向最终用户提供的所有前端堆栈中编写自定义 UI 代码。

但如果我的应用程序可以基于数据类型 "了解" 新的 UI 模板, 该怎么办？ 任何人都可以在自己的项目中、组织内或整个 internet 上参与、增强和共享公共 UI 模板。

## <a name="what-is-the-card-template-service"></a>什么是卡模板服务？

卡模板服务是一个简单的 REST 终结点, 可帮助:

* 通过分析数据的结构**查找**模板
* **获取**模板以便可以直接将其绑定到客户端,*而无需将数据发送到服务器或离开设备*
* 当客户端数据绑定不合适或不可行时, 在服务器上**填充**模板

毕竟, 是:

* GitHub 支持的共享开源模板存储库。 *(存储库当前是专用的, 但会在我们连接到一些松动的末尾后立即公开)*
* 所有模板都是存储库中的平面 JSON 文件, 它们可对开发人员工作流的一个自然部分进行编辑、贡献和共享。
* 此服务的代码将可用, 因此你可以在任何位置进行托管。 

## <a name="using-the-service"></a>使用服务

### <a name="get-all-templates"></a>获取所有模板 

此终结点返回所有已知模板的列表。

> `HTTP GET https://templates.adaptivecards.io/list`

**响应摘录**

```json
{
  "graph.microsoft.com": {
    "templates": [
      {
        "file": "Files.json",
        "fullPath": "graph.microsoft.com/Files.json"
      },
      {
        "file": "Profile.json",
        "fullPath": "graph.microsoft.com/Profile.json"
      }
   ]
}
```

### <a name="find-a-template"></a>查找模板

此终结点尝试通过分析数据的结构来查找模板。

> `HTTP POST https://templates.adaptivecards.io/find`

#### <a name="example"></a>示例

假设我只是点击了一个[Microsoft Graph](https://graph.microsoft.com)的终结点来获取组织数据。

> `HTTP GET https://graph.microsoft.com/v1.0/me/`

![图形资源管理器屏幕快照](content/2019-08-01-12-08-13.png)

该 API 返回了**JSON 数据**, 但如何使用自适应卡向用户**显示它**？ 

首先, 我想要查看是否存在此类数据的模板, 因此我使用`/find` `POST body`中的数据对终结点发出 HTTP 请求。

```
HTTP POST https://templates.adaptivecards.io/find

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users/$entity",
    "businessPhones": [
        "+1 412 555 0109"
    ],
    "displayName": "Megan Bowen",
    "givenName": "Megan",
    "jobTitle": "Auditor",
    "mail": "MeganB@M365x214355.onmicrosoft.com",
    "mobilePhone": null,
    "officeLocation": "12/1110",
    "preferredLanguage": "en-US",
    "surname": "Bowen",
    "userPrincipalName": "MeganB@M365x214355.onmicrosoft.com",
    "id": "48d31887-5fad-4d73-a9f5-3c356e68a038"
}
```

**回复**

```json
[
  {
    "templateUrl": "graph.microsoft.com/Profile.json",
    "confidence": 1
  }
]
```

服务将返回任何匹配模板的列表, 同时还会返回`confidence`一个, 指示匹配项的接近程度。 现在, 我可以使用该模板 URL 来**获取**模板, 或将其**填充**到服务器端。

### <a name="get-a-template"></a>获取模板

[使用 Templatng sdk](sdk.md), 可在运行时使用数据填充从此终结点检索的模板。

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]`

你还可以将 "示例数据" 包含在模板中, 以便在设计器中进行编辑更友好:

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]?sampleData=true`

#### <a name="example"></a>示例

接下来, 我们将获取从`/find`上面返回的 Microsoft Graph 配置文件模板。

`HTTP GET https://templates.adaptivecards.io/graph.microsoft.com/Profile.json`

**响应摘录**

```json
{
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "size": "Medium",
      "weight": "Bolder",
      "text": "{name}"
    },
    {
        // ...snip
    }
  ]
}
```

现在, 将此模板与模板[化 sdk](sdk.md)结合使用, 以创建现成的自适应卡。

### <a name="populate-a-template-server-side"></a>填充模板服务器端

在某些情况下, 在客户端上填充模板可能没有意义。  对于这些用例, 可以让服务返回完全填充的自适应卡, 并准备好将其传递到任何自适应卡呈现器。

> `HTTP POST https://templates.adaptivecards.io/[TEMPLATE-PATH]`

#### <a name="example"></a>示例

接下来, `/find`使用上面的数据来填充返回的 Microsoft Graph 配置文件模板。

```
HTTP POST https://templates.adaptivecards.io/graph.microsoft.com/Profile.json

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users/$entity",
    "businessPhones": [
        "+1 412 555 0109"
    ],
    "displayName": "Megan Bowen",
    "givenName": "Megan",
    "jobTitle": "Auditor",
    "mail": "MeganB@M365x214355.onmicrosoft.com",
    "mobilePhone": null,
    "officeLocation": "12/1110",
    "preferredLanguage": "en-US",
    "surname": "Bowen",
    "userPrincipalName": "MeganB@M365x214355.onmicrosoft.com",
    "id": "48d31887-5fad-4d73-a9f5-3c356e68a038"
}
```

**响应摘录**

```json
{
  "type": "AdaptiveCard",
  "version": "1.0",
  "body": [
    {
      "type": "TextBlock",
      "size": "Medium",
      "weight": "Bolder",
      "text": "Megan Bowen"
    },
    {
        // ...snip
    }
  ]
}
```

请注意`"{name}"`, 响应如何在`GET`请求中将第`TextBlock`一个`"Megan Bowen"`替换为 (而不是) 的文本。 现在可以将此 AdaptiveCard 传递到任何自适应卡呈现器, 而无需通过客户端模板化。

## <a name="contributing-templates"></a>参与模板

此模板服务由 GitHub 存储库 (当前为**专用**) 来支持, 但我们会在我们占用一些松动的结束后打开源。

我们希望使用 GitHub 作为模板的后备存储, 我们可以 "变得大众化" 创作、增强和共享模板的过程。 任何人都可以提交包含一个全新模板的拉取请求, 或对现有模板进行增强... GitHub 的开发人员友好体验中都有。

## <a name="self-hosting-the-service"></a>自承载服务

并非所有类型的数据都适用于中承载`https://templates.adaptivecards.io`的 "中心" 自适应卡模板服务。 

我们想要确保任何人都可以在你的组织内托管模板服务, 因此, 将提供源代码, 并使部署到 Azure 或你自己的后端变得非常简单。

稍后将对此进行详细介绍。