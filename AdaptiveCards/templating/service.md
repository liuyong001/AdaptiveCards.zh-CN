---
title: 自适应卡片模板服务
author: matthidinger
ms.author: mahiding
ms.date: 08/01/2019
ms.topic: article
ms.openlocfilehash: db211fc3bac27dc980ae87983a918a35730f8e5e
ms.sourcegitcommit: e6418d692296e06be7412c95c689843f9db5240d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2020
ms.locfileid: "82136183"
---
# <a name="adaptive-cards-template-service"></a>自适应卡片模板服务

自适应卡片模板服务是一项概念证明服务，允许任何人查找、贡献以及共享一组已知的模板。

如果你要显示一些数据，但不想为其编写自定义的自适应卡片，则可使用此服务。

> 有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)

> [!IMPORTANT] 
> 
> 条款和协议  
> 
> 此 **Alpha 级别**服务“按原样”提供，包含所有错误，且不提供任何方式的支持。 从服务进行的任何数据收集都需遵循 [Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkID=824704)的要求。
> 
> 这些功能为**预览版，可能会更改**。 我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。

## <a name="how-does-the-service-help-me"></a>此服务如何帮助我？

假设我刚获得一份数据，该数据可能是财务数据、Microsoft Graph 数据、schema.org 数据或来自我的组织中的自定义数据。 

现在，我想要向用户显示该数据。 

传统上，这意味着在我向最终用户提供的所有前端堆栈中编写自定义 UI 代码。

但如果我的应用可以根据数据类型“学习”新的 UI 模板，会出现什么情况？ 任何人都可以在自己的项目中、组织内或整个 Internet 上参与、增强和共享公共 UI 模板。

## <a name="what-is-the-card-template-service"></a>什么是卡片模板服务？

卡片模板服务是一个简单的 REST 终结点，它有助于：

* 通过分析数据的结构来**查找**模板
* **获取**模板，以便直接将其绑定到客户端，无需将数据发送到服务器或离开设备 
* 当客户端数据绑定不合适或不可行时，**填充**服务器上的模板

其背后的事实是：

* 有一个 GitHub 支持的共享开源模板存储库。 （存储库目前为专用，但一旦我们准备就绪，就会将其公开） 
* 在存储库中，所有模板都是平面 JSON 文件，因此可以很自然地在开发人员工作流中进行编辑、贡献和共享。
* 此服务的代码将可用，因此你可以在自己感觉最合理的任何位置进行托管。 

## <a name="using-the-service"></a>使用服务

### <a name="get-all-templates"></a>获取所有模板 

此终结点返回一个包含所有已知模板的列表。

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

假设我刚访问 [Microsoft Graph](https://graph.microsoft.com) 终结点来获取有关我的组织数据。

> `HTTP GET https://graph.microsoft.com/v1.0/me/`

![Graph 浏览器屏幕截图](content/2019-08-01-12-08-13.png)

该 API 返回了 **JSON 数据**，但我如何使用自适应卡片向用户**显示它**？ 

首先，我想要查看是否存在此类数据的模板，因此使用 `POST body` 中的数据向 `/find` 终结点发出 HTTP 请求。

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

**响应：**

```json
[
  {
    "templateUrl": "graph.microsoft.com/Profile.json",
    "confidence": 1
  }
]
```

服务返回任何匹配模板的列表，以及一个 `confidence`，指示匹配程度。 现在，我可以使用该模板 URL 来**获取**模板，或在服务器端**填充**它。

### <a name="get-a-template"></a>获取模板

从此终结点检索的模板可以在运行时[使用模板化 SDK](sdk.md) 填充数据。

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]`

还可以让“示例数据”包含在模板中，这样就可以在设计器中更方便地进行编辑：

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]?sampleData=true`

#### <a name="example"></a>示例

让我们获取已从上面的 `/find` 返回的 Microsoft Graph 配置文件模板。

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

现在，请将此模板与[模板化 SDK](sdk.md) 配合使用，创建可以呈现的自适应卡片。

### <a name="populate-a-template-server-side"></a>在服务器端填充模板

某些情况下，在客户端填充模板可能没有意义。  对于这些用例，可以让服务返回一张完全填充的自适应卡片，该卡片可以传递给任何自适应卡片呈现器。

> `HTTP POST https://templates.adaptivecards.io/[TEMPLATE-PATH]`

#### <a name="example"></a>示例

让我们使用上面的数据填充已从 `/find` 返回的 Microsoft Graph 配置文件模板。

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

请注意响应如何将第一个 `TextBlock` 的文本替换为 `"Megan Bowen"` 而不是 `"{name}"`，如 `GET` 请求中所示。 现在可以将此 AdaptiveCard 传递给任何自适应卡片呈现器，无需进行客户端模板化。

## <a name="contributing-templates"></a>贡献模板

模板托管在 GitHub 上的 [adaptivecards-templates](https://github.com/microsoft/adaptivecards-templates) 存储库中。

我们希望使用 GitHub 作为模板的后备存储，这样就可以“推广”创作、增强和共享模板的过程。 任何人都可以提交包含一个全新模板的拉取请求，或者对现有模板进行增强操作，这一切都在便于开发人员使用的 GitHub 体验中提供。

## <a name="self-hosting-the-service"></a>自托管此服务

并非所有类型的数据都适用于 `https://templates.adaptivecards.io` 上托管的“中心”自适应卡片模板服务。 

我们希望确保任何人都可以在你的组织内托管模板服务，因此，源代码已在 GitHub 上提供，并且可以轻松部署到你自己的 Azure 函数。 

从此处开始➡ [adaptivecards-templates](https://github.com/microsoft/adaptivecards-templates)
