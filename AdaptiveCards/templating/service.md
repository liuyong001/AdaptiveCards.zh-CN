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
# <a name="adaptive-cards-template-service"></a><span data-ttu-id="d35fb-102">自适应卡片模板服务</span><span class="sxs-lookup"><span data-stu-id="d35fb-102">Adaptive Cards Template Service</span></span>

<span data-ttu-id="d35fb-103">自适应卡片模板服务是一项概念证明服务，允许任何人查找、贡献以及共享一组已知的模板。</span><span class="sxs-lookup"><span data-stu-id="d35fb-103">The Adaptive Cards Template Service is a proof-of-concept service that allows anyone to find, contribute to, and share a set of well-known templates.</span></span>

<span data-ttu-id="d35fb-104">如果你要显示一些数据，但不想为其编写自定义的自适应卡片，则可使用此服务。</span><span class="sxs-lookup"><span data-stu-id="d35fb-104">It's useful if you want to display some data but don't want to bother writing a custom adaptive card for it.</span></span>

> <span data-ttu-id="d35fb-105">有关此方面的内容，请参阅[自适应卡片模板化概述](index.md)</span><span class="sxs-lookup"><span data-stu-id="d35fb-105">Please read this for an [overview of Adaptive Card Templating](index.md)</span></span>

> [!IMPORTANT] 
> 
> <span data-ttu-id="d35fb-106">条款和协议 </span><span class="sxs-lookup"><span data-stu-id="d35fb-106">*Terms and agreement*</span></span> 
> 
> <span data-ttu-id="d35fb-107">此 **Alpha 级别**服务“按原样”提供，包含所有错误，且不提供任何方式的支持。</span><span class="sxs-lookup"><span data-stu-id="d35fb-107">This **alpha-level** service is provided "as-is", with all faults and is not supported in any way.</span></span> <span data-ttu-id="d35fb-108">从服务进行的任何数据收集都需遵循 [Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkID=824704)的要求。</span><span class="sxs-lookup"><span data-stu-id="d35fb-108">Any data collection from the service is subject to the [Microsoft privacy statement](https://go.microsoft.com/fwlink/?LinkID=824704).</span></span>
> 
> <span data-ttu-id="d35fb-109">这些功能为**预览版，可能会更改**。</span><span class="sxs-lookup"><span data-stu-id="d35fb-109">These features are **in preview and subject to change**.</span></span> <span data-ttu-id="d35fb-110">我们欢迎你的反馈，它很重要，可以确保我们提供**你**需要的功能。</span><span class="sxs-lookup"><span data-stu-id="d35fb-110">Your feedback is not only welcome, but  critical to ensure we deliver the features **you** need.</span></span>

## <a name="how-does-the-service-help-me"></a><span data-ttu-id="d35fb-111">此服务如何帮助我？</span><span class="sxs-lookup"><span data-stu-id="d35fb-111">How does the service help me?</span></span>

<span data-ttu-id="d35fb-112">假设我刚获得一份数据，该数据可能是财务数据、Microsoft Graph 数据、schema.org 数据或来自我的组织中的自定义数据。</span><span class="sxs-lookup"><span data-stu-id="d35fb-112">Let's say I just got a piece of data, maybe it's financial data, Microsoft Graph data, schema.org data, or custom data from within my organization.</span></span> 

<span data-ttu-id="d35fb-113">现在，我想要向用户显示该数据。</span><span class="sxs-lookup"><span data-stu-id="d35fb-113">Now I want to display the data to a user.</span></span> 

<span data-ttu-id="d35fb-114">传统上，这意味着在我向最终用户提供的所有前端堆栈中编写自定义 UI 代码。</span><span class="sxs-lookup"><span data-stu-id="d35fb-114">Traditionally that means writing custom UI code in all of the front-end stacks that I deliver to end-users.</span></span>

<span data-ttu-id="d35fb-115">但如果我的应用可以根据数据类型“学习”新的 UI 模板，会出现什么情况？</span><span class="sxs-lookup"><span data-stu-id="d35fb-115">But what if there were a world where my app could "learn" new UI templates based on the type of data?</span></span> <span data-ttu-id="d35fb-116">任何人都可以在自己的项目中、组织内或整个 Internet 上参与、增强和共享公共 UI 模板。</span><span class="sxs-lookup"><span data-stu-id="d35fb-116">A world where anyone could contribute, enhance, and share common UI templates, within their own projects, within an organization, or for the entire internet.</span></span>

## <a name="what-is-the-card-template-service"></a><span data-ttu-id="d35fb-117">什么是卡片模板服务？</span><span class="sxs-lookup"><span data-stu-id="d35fb-117">What is the card template service?</span></span>

<span data-ttu-id="d35fb-118">卡片模板服务是一个简单的 REST 终结点，它有助于：</span><span class="sxs-lookup"><span data-stu-id="d35fb-118">The card template service is a simple REST endpoint that helps:</span></span>

* <span data-ttu-id="d35fb-119">通过分析数据的结构来**查找**模板</span><span class="sxs-lookup"><span data-stu-id="d35fb-119">**Find** a template by analyzing the structure of your data</span></span>
* <span data-ttu-id="d35fb-120">**获取**模板，以便直接将其绑定到客户端，无需将数据发送到服务器或离开设备 </span><span class="sxs-lookup"><span data-stu-id="d35fb-120">**Get** a template so you can bind it directly on the client, *without sending your data to the server or ever leaving the device*</span></span>
* <span data-ttu-id="d35fb-121">当客户端数据绑定不合适或不可行时，**填充**服务器上的模板</span><span class="sxs-lookup"><span data-stu-id="d35fb-121">**Populate** a template on the server, when client-side data binding isn't appropriate or possible</span></span>

<span data-ttu-id="d35fb-122">其背后的事实是：</span><span class="sxs-lookup"><span data-stu-id="d35fb-122">Behind it all, is:</span></span>

* <span data-ttu-id="d35fb-123">有一个 GitHub 支持的共享开源模板存储库。</span><span class="sxs-lookup"><span data-stu-id="d35fb-123">A shared, open-source template repository backed by GitHub.</span></span> <span data-ttu-id="d35fb-124">（存储库目前为专用，但一旦我们准备就绪，就会将其公开） </span><span class="sxs-lookup"><span data-stu-id="d35fb-124">*(The repo is currently private but will be made public as soon as we tie up some loose ends)*</span></span>
* <span data-ttu-id="d35fb-125">在存储库中，所有模板都是平面 JSON 文件，因此可以很自然地在开发人员工作流中进行编辑、贡献和共享。</span><span class="sxs-lookup"><span data-stu-id="d35fb-125">All the templates are flat JSON files in the repo, which makes editing, contributing, and sharing a natural part of a developer workflow.</span></span>
* <span data-ttu-id="d35fb-126">此服务的代码将可用，因此你可以在自己感觉最合理的任何位置进行托管。</span><span class="sxs-lookup"><span data-stu-id="d35fb-126">The code for the service will be made available so you can host wherever makes the most sense to you.</span></span> 

## <a name="using-the-service"></a><span data-ttu-id="d35fb-127">使用服务</span><span class="sxs-lookup"><span data-stu-id="d35fb-127">Using the service</span></span>

### <a name="get-all-templates"></a><span data-ttu-id="d35fb-128">获取所有模板</span><span class="sxs-lookup"><span data-stu-id="d35fb-128">Get all templates</span></span> 

<span data-ttu-id="d35fb-129">此终结点返回一个包含所有已知模板的列表。</span><span class="sxs-lookup"><span data-stu-id="d35fb-129">This endpoint returns a list of all known templates.</span></span>

> `HTTP GET https://templates.adaptivecards.io/list`

<span data-ttu-id="d35fb-130">**响应摘录**</span><span class="sxs-lookup"><span data-stu-id="d35fb-130">**Response excerpt**</span></span>

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

### <a name="find-a-template"></a><span data-ttu-id="d35fb-131">查找模板</span><span class="sxs-lookup"><span data-stu-id="d35fb-131">Find a template</span></span>

<span data-ttu-id="d35fb-132">此终结点尝试通过分析数据的结构来查找模板。</span><span class="sxs-lookup"><span data-stu-id="d35fb-132">This endpoint tries to find a template by analyzing the structure of your data.</span></span>

> `HTTP POST https://templates.adaptivecards.io/find`

#### <a name="example"></a><span data-ttu-id="d35fb-133">示例</span><span class="sxs-lookup"><span data-stu-id="d35fb-133">Example</span></span>

<span data-ttu-id="d35fb-134">假设我刚访问 [Microsoft Graph](https://graph.microsoft.com) 终结点来获取有关我的组织数据。</span><span class="sxs-lookup"><span data-stu-id="d35fb-134">Let's say I access a [Microsoft Graph](https://graph.microsoft.com) endpoint to get organizational data about me.</span></span>

> `HTTP GET https://graph.microsoft.com/v1.0/me/`

![Graph 浏览器屏幕截图](content/2019-08-01-12-08-13.png)

<span data-ttu-id="d35fb-136">该 API 返回了 **JSON 数据**，但我如何使用自适应卡片向用户**显示它**？</span><span class="sxs-lookup"><span data-stu-id="d35fb-136">That API returned **JSON data**, but how do I **display it** to users using Adaptive Cards?</span></span> 

<span data-ttu-id="d35fb-137">首先，我想要查看是否存在此类数据的模板，因此使用 `POST body` 中的数据向 `/find` 终结点发出 HTTP 请求。</span><span class="sxs-lookup"><span data-stu-id="d35fb-137">First I want to see if a template exists for this type of data, so I make an HTTP request to the `/find` endpoint with my data in the `POST body`.</span></span>

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

<span data-ttu-id="d35fb-138">**响应：**</span><span class="sxs-lookup"><span data-stu-id="d35fb-138">**Response:**</span></span>

```json
[
  {
    "templateUrl": "graph.microsoft.com/Profile.json",
    "confidence": 1
  }
]
```

<span data-ttu-id="d35fb-139">服务返回任何匹配模板的列表，以及一个 `confidence`，指示匹配程度。</span><span class="sxs-lookup"><span data-stu-id="d35fb-139">The service returns a list of any matching templates, along with a `confidence` indicating how close the match is.</span></span> <span data-ttu-id="d35fb-140">现在，我可以使用该模板 URL 来**获取**模板，或在服务器端**填充**它。</span><span class="sxs-lookup"><span data-stu-id="d35fb-140">Now I can use that template URL to **get** the template, or **populate** it server-side.</span></span>

### <a name="get-a-template"></a><span data-ttu-id="d35fb-141">获取模板</span><span class="sxs-lookup"><span data-stu-id="d35fb-141">Get a template</span></span>

<span data-ttu-id="d35fb-142">从此终结点检索的模板可以在运行时[使用模板化 SDK](sdk.md) 填充数据。</span><span class="sxs-lookup"><span data-stu-id="d35fb-142">A template retrieved from this endpoint can be populated with data at runtime [using the templatng SDKs](sdk.md).</span></span>

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]`

<span data-ttu-id="d35fb-143">还可以让“示例数据”包含在模板中，这样就可以在设计器中更方便地进行编辑：</span><span class="sxs-lookup"><span data-stu-id="d35fb-143">You can also include "sample data" with the template, which makes editing in the designer more friendly:</span></span>

> `HTTP GET https://templates.adaptivecards.io/[TEMPLATE-PATH]?sampleData=true`

#### <a name="example"></a><span data-ttu-id="d35fb-144">示例</span><span class="sxs-lookup"><span data-stu-id="d35fb-144">Example</span></span>

<span data-ttu-id="d35fb-145">让我们获取已从上面的 `/find` 返回的 Microsoft Graph 配置文件模板。</span><span class="sxs-lookup"><span data-stu-id="d35fb-145">Let's get the Microsoft Graph profile template that was returned from `/find` above.</span></span>

`HTTP GET https://templates.adaptivecards.io/graph.microsoft.com/Profile.json`

<span data-ttu-id="d35fb-146">**响应摘录**</span><span class="sxs-lookup"><span data-stu-id="d35fb-146">**Response excerpt**</span></span>

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

<span data-ttu-id="d35fb-147">现在，请将此模板与[模板化 SDK](sdk.md) 配合使用，创建可以呈现的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="d35fb-147">Now use this template with the [templating SDKs](sdk.md) to create a ready-to-render Adaptive Card.</span></span>

### <a name="populate-a-template-server-side"></a><span data-ttu-id="d35fb-148">在服务器端填充模板</span><span class="sxs-lookup"><span data-stu-id="d35fb-148">Populate a template server-side</span></span>

<span data-ttu-id="d35fb-149">某些情况下，在客户端填充模板可能没有意义。</span><span class="sxs-lookup"><span data-stu-id="d35fb-149">In some cases it may not make sense to populate a template on the client.</span></span>  <span data-ttu-id="d35fb-150">对于这些用例，可以让服务返回一张完全填充的自适应卡片，该卡片可以传递给任何自适应卡片呈现器。</span><span class="sxs-lookup"><span data-stu-id="d35fb-150">For these use cases, you can have the service return a fully-populated Adaptive Card, ready to be passed to any Adaptive Card Renderer.</span></span>

> `HTTP POST https://templates.adaptivecards.io/[TEMPLATE-PATH]`

#### <a name="example"></a><span data-ttu-id="d35fb-151">示例</span><span class="sxs-lookup"><span data-stu-id="d35fb-151">Example</span></span>

<span data-ttu-id="d35fb-152">让我们使用上面的数据填充已从 `/find` 返回的 Microsoft Graph 配置文件模板。</span><span class="sxs-lookup"><span data-stu-id="d35fb-152">Let's populate the Microsoft Graph profile template that was returned from `/find` using the data above.</span></span>

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

<span data-ttu-id="d35fb-153">**响应摘录**</span><span class="sxs-lookup"><span data-stu-id="d35fb-153">**Response excerpt**</span></span>

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

<span data-ttu-id="d35fb-154">请注意响应如何将第一个 `TextBlock` 的文本替换为 `"Megan Bowen"` 而不是 `"{name}"`，如 `GET` 请求中所示。</span><span class="sxs-lookup"><span data-stu-id="d35fb-154">Notice how the response replaced the text of the first `TextBlock` with `"Megan Bowen"` instead of `"{name}"`, as in the `GET` request.</span></span> <span data-ttu-id="d35fb-155">现在可以将此 AdaptiveCard 传递给任何自适应卡片呈现器，无需进行客户端模板化。</span><span class="sxs-lookup"><span data-stu-id="d35fb-155">This AdaptiveCard can now be passed to any Adaptive Card renderer without going through client-side templating.</span></span>

## <a name="contributing-templates"></a><span data-ttu-id="d35fb-156">贡献模板</span><span class="sxs-lookup"><span data-stu-id="d35fb-156">Contributing templates</span></span>

<span data-ttu-id="d35fb-157">模板托管在 GitHub 上的 [adaptivecards-templates](https://github.com/microsoft/adaptivecards-templates) 存储库中。</span><span class="sxs-lookup"><span data-stu-id="d35fb-157">The templates are hosted on GitHub in the [adaptivecards-templates](https://github.com/microsoft/adaptivecards-templates) repo.</span></span>

<span data-ttu-id="d35fb-158">我们希望使用 GitHub 作为模板的后备存储，这样就可以“推广”创作、增强和共享模板的过程。</span><span class="sxs-lookup"><span data-stu-id="d35fb-158">Our hope is that by using GitHub as a backing store for the templates, we can "democratize" the process of authoring, enhancing, and sharing templates.</span></span> <span data-ttu-id="d35fb-159">任何人都可以提交包含一个全新模板的拉取请求，或者对现有模板进行增强操作，这一切都在便于开发人员使用的 GitHub 体验中提供。</span><span class="sxs-lookup"><span data-stu-id="d35fb-159">Anyone can submit a Pull Request that includes an entirely new template, or make enhancements to existing ones... all within the developer-friendly experience of GitHub.</span></span>

## <a name="self-hosting-the-service"></a><span data-ttu-id="d35fb-160">自托管此服务</span><span class="sxs-lookup"><span data-stu-id="d35fb-160">Self-hosting the service</span></span>

<span data-ttu-id="d35fb-161">并非所有类型的数据都适用于 `https://templates.adaptivecards.io` 上托管的“中心”自适应卡片模板服务。</span><span class="sxs-lookup"><span data-stu-id="d35fb-161">Not all types of data are appropriate for the "central" Adaptive Cards template service hosted at `https://templates.adaptivecards.io`.</span></span> 

<span data-ttu-id="d35fb-162">我们希望确保任何人都可以在你的组织内托管模板服务，因此，源代码已在 GitHub 上提供，并且可以轻松部署到你自己的 Azure 函数。</span><span class="sxs-lookup"><span data-stu-id="d35fb-162">We want to make sure anyone can host the template service within your organization, so the source code is available on GitHub and can be easily deployed to your own Azure Function.</span></span> 

<span data-ttu-id="d35fb-163">从此处开始➡ [adaptivecards-templates](https://github.com/microsoft/adaptivecards-templates)</span><span class="sxs-lookup"><span data-stu-id="d35fb-163">Get started here ➡ [adaptivecards-templates](https://github.com/microsoft/adaptivecards-templates)</span></span>
