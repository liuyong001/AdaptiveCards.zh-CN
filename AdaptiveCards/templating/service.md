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
# <a name="adaptive-cards-template-service"></a><span data-ttu-id="c0b3a-102">自适应卡模板服务</span><span class="sxs-lookup"><span data-stu-id="c0b3a-102">Adaptive Cards Template Service</span></span>

<span data-ttu-id="c0b3a-103">自适应卡模板服务是一种概念证明服务, 它允许任何人查找、参与和共享一组众所周知的模板。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-103">The Adaptive Cards Template Service is a proof-of-concept service that allows anyone to find, contribute to, and share a set of well-known templates.</span></span>

<span data-ttu-id="c0b3a-104">如果希望显示某些数据, 但不希望为其编写自定义的自适应卡, 则此方法非常有用。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-104">It's useful if you want to display some data but don't want to bother writing a custom adaptive card for it.</span></span>

> <span data-ttu-id="c0b3a-105">有关[自适应卡模板的概述](index.md), 请阅读此概述</span><span class="sxs-lookup"><span data-stu-id="c0b3a-105">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="c0b3a-106">*条款和协议*</span><span class="sxs-lookup"><span data-stu-id="c0b3a-106">*Terms and agreement*</span></span> 
> 
> <span data-ttu-id="c0b3a-107">此**alpha 级别**服务 "按原样" 提供, 并具有所有错误, 不支持任何方式。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-107">This **alpha-level** service is provided "as-is", with all faults and is not supported in any way.</span></span> <span data-ttu-id="c0b3a-108">从服务收集的任何数据都服从[Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkID=824704)。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-108">Any data collection from the service is subject to the [Microsoft privacy statement](https://go.microsoft.com/fwlink/?LinkID=824704).</span></span>
> 
> <span data-ttu-id="c0b3a-109">这些功能**处于预览阶段, 可能会有所更改**。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-109">These features are **in preview and subject to change**.</span></span> <span data-ttu-id="c0b3a-110">你的反馈不仅是欢迎的, 而且确保我们能够提供**所**需的功能至关重要。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-110">Your feedback is not only welcome, but  critical to ensure we deliver the features **you** need.</span></span>

## <a name="how-does-the-service-help-me"></a><span data-ttu-id="c0b3a-111">服务如何帮助我？</span><span class="sxs-lookup"><span data-stu-id="c0b3a-111">How does the service help me?</span></span>

<span data-ttu-id="c0b3a-112">假设我只获取了一段数据, 可能是它的财务数据、Microsoft Graph 数据、schema.org 数据或来自我的组织中的自定义数据。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-112">Let's say I just got a piece of data, maybe it's financial data, Microsoft Graph data, schema.org data, or custom data from within my organization.</span></span> 

<span data-ttu-id="c0b3a-113">现在, 我想向用户显示数据。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-113">Now I want to display the data to a user.</span></span> 

<span data-ttu-id="c0b3a-114">过去, 这意味着在我向最终用户提供的所有前端堆栈中编写自定义 UI 代码。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-114">Traditionally that means writing custom UI code in all of the front-end stacks that I deliver to end-users.</span></span>

<span data-ttu-id="c0b3a-115">但如果我的应用程序可以基于数据类型 "了解" 新的 UI 模板, 该怎么办？</span><span class="sxs-lookup"><span data-stu-id="c0b3a-115">But what if there were a world where my app could "learn" new UI templates based on the type of data?</span></span> <span data-ttu-id="c0b3a-116">任何人都可以在自己的项目中、组织内或整个 internet 上参与、增强和共享公共 UI 模板。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-116">A world where anyone could contribute, enhance, and share common UI templates, within their own projects, within an organization, or for the entire internet.</span></span>

## <a name="what-is-the-card-template-service"></a><span data-ttu-id="c0b3a-117">什么是卡模板服务？</span><span class="sxs-lookup"><span data-stu-id="c0b3a-117">What is the card template service?</span></span>

<span data-ttu-id="c0b3a-118">卡模板服务是一个简单的 REST 终结点, 可帮助:</span><span class="sxs-lookup"><span data-stu-id="c0b3a-118">The card template service is a simple REST endpoint that helps:</span></span>

* <span data-ttu-id="c0b3a-119">通过分析数据的结构**查找**模板</span><span class="sxs-lookup"><span data-stu-id="c0b3a-119">**Find** a template by analyzing the structure of your data</span></span>
* <span data-ttu-id="c0b3a-120">**获取**模板以便可以直接将其绑定到客户端,*而无需将数据发送到服务器或离开设备*</span><span class="sxs-lookup"><span data-stu-id="c0b3a-120">**Get** a template so you can bind it directly on the client, *without sending your data to the server or ever leaving the device*</span></span>
* <span data-ttu-id="c0b3a-121">当客户端数据绑定不合适或不可行时, 在服务器上**填充**模板</span><span class="sxs-lookup"><span data-stu-id="c0b3a-121">**Populate** a template on the server, when client-side data binding isn't appropriate or possible</span></span>

<span data-ttu-id="c0b3a-122">毕竟, 是:</span><span class="sxs-lookup"><span data-stu-id="c0b3a-122">Behind it all, is:</span></span>

* <span data-ttu-id="c0b3a-123">GitHub 支持的共享开源模板存储库。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-123">A shared, open-source template repository backed by GitHub.</span></span> <span data-ttu-id="c0b3a-124">*(存储库当前是专用的, 但会在我们连接到一些松动的末尾后立即公开)*</span><span class="sxs-lookup"><span data-stu-id="c0b3a-124">*(The repo is currently private but will be made public as soon as we tie up some loose ends)*</span></span>
* <span data-ttu-id="c0b3a-125">所有模板都是存储库中的平面 JSON 文件, 它们可对开发人员工作流的一个自然部分进行编辑、贡献和共享。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-125">All the templates are flat JSON files in the repo, which makes editing, contributing, and sharing a natural part of a developer workflow.</span></span>
* <span data-ttu-id="c0b3a-126">此服务的代码将可用, 因此你可以在任何位置进行托管。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-126">The code for the service will be made available so you can host wherever makes the most sense to you.</span></span> 

## <a name="using-the-service"></a><span data-ttu-id="c0b3a-127">使用服务</span><span class="sxs-lookup"><span data-stu-id="c0b3a-127">Using the service</span></span>

### <a name="get-all-templates"></a><span data-ttu-id="c0b3a-128">获取所有模板</span><span class="sxs-lookup"><span data-stu-id="c0b3a-128">Get all templates</span></span> 

<span data-ttu-id="c0b3a-129">此终结点返回所有已知模板的列表。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-129">This endpoint returns a list of all known templates.</span></span>

> `HTTP GET https://templates.adaptivecards.io/list`

<span data-ttu-id="c0b3a-130">**响应摘录**</span><span class="sxs-lookup"><span data-stu-id="c0b3a-130">**Response excerpt**</span></span>

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

### <a name="find-a-template"></a><span data-ttu-id="c0b3a-131">查找模板</span><span class="sxs-lookup"><span data-stu-id="c0b3a-131">Find a template</span></span>

<span data-ttu-id="c0b3a-132">此终结点尝试通过分析数据的结构来查找模板。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-132">This endpoint tries to find a template by analyzing the structure of your data.</span></span>

> `HTTP POST https://templates.adaptivecards.io/find`

#### <a name="example"></a><span data-ttu-id="c0b3a-133">示例</span><span class="sxs-lookup"><span data-stu-id="c0b3a-133">Example</span></span>

<span data-ttu-id="c0b3a-134">假设我只是点击了一个[Microsoft Graph](https://graph.microsoft.com)的终结点来获取组织数据。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-134">Let's say I just hit a [Microsoft Graph](https://graph.microsoft.com) endpoint to get organizational data about me.</span></span>

> `HTTP GET https://graph.microsoft.com/v1.0/me/`

![图形资源管理器屏幕快照](content/2019-08-01-12-08-13.png)

<span data-ttu-id="c0b3a-136">该 API 返回了**JSON 数据**, 但如何使用自适应卡向用户**显示它**？</span><span class="sxs-lookup"><span data-stu-id="c0b3a-136">That API returned **JSON data**, but how do I **display it** to users using Adaptive Cards?</span></span> 

<span data-ttu-id="c0b3a-137">首先, 我想要查看是否存在此类数据的模板, 因此我使用`/find` `POST body`中的数据对终结点发出 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-137">First I want to see if a template exists for this type of data, so I make an HTTP request to the `/find` endpoint with my data in the `POST body`.</span></span>

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

<span data-ttu-id="c0b3a-138">**回复**</span><span class="sxs-lookup"><span data-stu-id="c0b3a-138">**Response:**</span></span>

```json
[
  {
    "templateUrl": "graph.microsoft.com/Profile.json",
    "confidence": 1
  }
]
```

<span data-ttu-id="c0b3a-139">服务将返回任何匹配模板的列表, 同时还会返回`confidence`一个, 指示匹配项的接近程度。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-139">The service returns a list of any matching templates, along with a `confidence` indicating how close the match is.</span></span> <span data-ttu-id="c0b3a-140">现在, 我可以使用该模板 URL 来**获取**模板, 或将其**填充**到服务器端。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-140">Now I can use that template URL to **get** the template, or **populate** it server-side.</span></span>

### <a name="get-a-template"></a><span data-ttu-id="c0b3a-141">获取模板</span><span class="sxs-lookup"><span data-stu-id="c0b3a-141">Get a template</span></span>

<span data-ttu-id="c0b3a-142">[使用 Templatng sdk](sdk.md), 可在运行时使用数据填充从此终结点检索的模板。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-142">A template retrieved from this endpoint can be populated with data at runtime [using the templatng SDKs](sdk.md).</span></span>

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]`

<span data-ttu-id="c0b3a-143">你还可以将 "示例数据" 包含在模板中, 以便在设计器中进行编辑更友好:</span><span class="sxs-lookup"><span data-stu-id="c0b3a-143">You can also include "sample data" with the template, which makes editing in the designer more friendly:</span></span>

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]?sampleData=true`

#### <a name="example"></a><span data-ttu-id="c0b3a-144">示例</span><span class="sxs-lookup"><span data-stu-id="c0b3a-144">Example</span></span>

<span data-ttu-id="c0b3a-145">接下来, 我们将获取从`/find`上面返回的 Microsoft Graph 配置文件模板。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-145">Let's get the Microsoft Graph profile template that was returned from `/find` above.</span></span>

`HTTP GET https://templates.adaptivecards.io/graph.microsoft.com/Profile.json`

<span data-ttu-id="c0b3a-146">**响应摘录**</span><span class="sxs-lookup"><span data-stu-id="c0b3a-146">**Response excerpt**</span></span>

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

<span data-ttu-id="c0b3a-147">现在, 将此模板与模板[化 sdk](sdk.md)结合使用, 以创建现成的自适应卡。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-147">Now use this template with the [templating SDKs](sdk.md) to create a ready-to-render Adaptive Card.</span></span>

### <a name="populate-a-template-server-side"></a><span data-ttu-id="c0b3a-148">填充模板服务器端</span><span class="sxs-lookup"><span data-stu-id="c0b3a-148">Populate a template server-side</span></span>

<span data-ttu-id="c0b3a-149">在某些情况下, 在客户端上填充模板可能没有意义。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-149">In some cases it may not make sense to populate a template on the client.</span></span>  <span data-ttu-id="c0b3a-150">对于这些用例, 可以让服务返回完全填充的自适应卡, 并准备好将其传递到任何自适应卡呈现器。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-150">For these use cases, you can have the service return a fully-populated Adaptive Card, ready to be passed to any Adaptive Card Renderer.</span></span>

> `HTTP POST https://templates.adaptivecards.io/[TEMPLATE-PATH]`

#### <a name="example"></a><span data-ttu-id="c0b3a-151">示例</span><span class="sxs-lookup"><span data-stu-id="c0b3a-151">Example</span></span>

<span data-ttu-id="c0b3a-152">接下来, `/find`使用上面的数据来填充返回的 Microsoft Graph 配置文件模板。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-152">Let's populate the Microsoft Graph profile template that was returned from `/find` using the data above.</span></span>

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

<span data-ttu-id="c0b3a-153">**响应摘录**</span><span class="sxs-lookup"><span data-stu-id="c0b3a-153">**Response excerpt**</span></span>

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

<span data-ttu-id="c0b3a-154">请注意`"{name}"`, 响应如何在`GET`请求中将第`TextBlock`一个`"Megan Bowen"`替换为 (而不是) 的文本。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-154">Notice how the response replaced the text of the first `TextBlock` with `"Megan Bowen"` instead of `"{name}"`, as in the `GET` request.</span></span> <span data-ttu-id="c0b3a-155">现在可以将此 AdaptiveCard 传递到任何自适应卡呈现器, 而无需通过客户端模板化。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-155">This AdaptiveCard can now be passed to any Adaptive Card renderer without going through client-side templating.</span></span>

## <a name="contributing-templates"></a><span data-ttu-id="c0b3a-156">参与模板</span><span class="sxs-lookup"><span data-stu-id="c0b3a-156">Contributing templates</span></span>

<span data-ttu-id="c0b3a-157">此模板服务由 GitHub 存储库 (当前为**专用**) 来支持, 但我们会在我们占用一些松动的结束后打开源。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-157">The template service is backed by a GitHub repo (which is currently **private**), but we will open source once we tie up some loose ends.</span></span>

<span data-ttu-id="c0b3a-158">我们希望使用 GitHub 作为模板的后备存储, 我们可以 "变得大众化" 创作、增强和共享模板的过程。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-158">Our hope is that by using GitHub as a backing store for the templates, we can "democratize" the process of authoring, enhancing, and sharing templates.</span></span> <span data-ttu-id="c0b3a-159">任何人都可以提交包含一个全新模板的拉取请求, 或对现有模板进行增强 .。。GitHub 的开发人员友好体验中都有。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-159">Anyone can submit a Pull Request that includes an entirely new template, or make enhancements to existing ones... all within the developer-friendly experience of GitHub.</span></span>

## <a name="self-hosting-the-service"></a><span data-ttu-id="c0b3a-160">自承载服务</span><span class="sxs-lookup"><span data-stu-id="c0b3a-160">Self-hosting the service</span></span>

<span data-ttu-id="c0b3a-161">并非所有类型的数据都适用于中承载`https://templates.adaptivecards.io`的 "中心" 自适应卡模板服务。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-161">Not all types of data are appropriate for the "central" Adaptive Cards template service hosted at `https://templates.adaptivecards.io`.</span></span> 

<span data-ttu-id="c0b3a-162">我们想要确保任何人都可以在你的组织内托管模板服务, 因此, 将提供源代码, 并使部署到 Azure 或你自己的后端变得非常简单。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-162">We want to make sure anyone can host the template service within your organization, so the source code will be made available and we'll make it very simple to deploy to Azure or your own back-end.</span></span>

<span data-ttu-id="c0b3a-163">稍后将对此进行详细介绍。</span><span class="sxs-lookup"><span data-stu-id="c0b3a-163">More on this at a later date.</span></span>