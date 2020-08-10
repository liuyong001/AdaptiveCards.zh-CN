---
title: 自适应卡工具
author: matthidinger
ms.author: mahiding
ms.date: 03/14/2019
ms.topic: article
ms.openlocfilehash: 819788313d78b4057fb5d3dc4d5a9be658566642
ms.sourcegitcommit: 996fc604e59f72ba1dd96c29f4b517862a5264e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2020
ms.locfileid: "87566021"
---
# <a name="tools-and-samples"></a><span data-ttu-id="05d7d-102">工具和示例</span><span class="sxs-lookup"><span data-stu-id="05d7d-102">Tools and Samples</span></span>

## <a name="card-designer"></a><span data-ttu-id="05d7d-103">卡设计器</span><span class="sxs-lookup"><span data-stu-id="05d7d-103">Card Designer</span></span> 

<span data-ttu-id="05d7d-104">需要工具来设计卡片？</span><span class="sxs-lookup"><span data-stu-id="05d7d-104">Need for a tool to design your cards?</span></span> <span data-ttu-id="05d7d-105">不妨看看这个基于浏览器的自适应卡片设计器：[https://adaptivecards.io/designer](https://adaptivecards.io/designer)</span><span class="sxs-lookup"><span data-stu-id="05d7d-105">Look no further than the browser-based adaptive card designer at [https://adaptivecards.io/designer](https://adaptivecards.io/designer)</span></span>

<span data-ttu-id="05d7d-106">[![设计器屏幕截图](media/tools/designer.jpg)](https://adaptivecards.io/designer)</span><span class="sxs-lookup"><span data-stu-id="05d7d-106">[![designer screenshot](media/tools/designer.jpg)](https://adaptivecards.io/designer)</span></span>

### <a name="embed-the-designer-into-your-app"></a><span data-ttu-id="05d7d-107">将设计器嵌入应用</span><span class="sxs-lookup"><span data-stu-id="05d7d-107">Embed the designer into your app</span></span>

<span data-ttu-id="05d7d-108">但是，如果你可以使用我们的 JavaScript 库**将卡片设计器直接嵌入 Web 应用**中，为何还要让用户大费周折呢？</span><span class="sxs-lookup"><span data-stu-id="05d7d-108">But why send your users there when you can **embed the card designer directly into your web** app using our JavaScript library.</span></span> 

<span data-ttu-id="05d7d-109">若要开始，请查看 [adaptivecards-designer](https://npmjs.com/adaptivecards-designer) 包。</span><span class="sxs-lookup"><span data-stu-id="05d7d-109">Check out the [adaptivecards-designer](https://npmjs.com/adaptivecards-designer) package to get started.</span></span>

## <a name="schema-validation"></a><span data-ttu-id="05d7d-110">架构验证</span><span class="sxs-lookup"><span data-stu-id="05d7d-110">Schema validation</span></span>

<span data-ttu-id="05d7d-111">可以通过架构验证轻松地进行创作并启用工具功能。</span><span class="sxs-lookup"><span data-stu-id="05d7d-111">Schema validation is a powerful way of making authoring easier and enabling tooling.</span></span>

<span data-ttu-id="05d7d-112">我们提供了完整的 [JSON 架构文件](https://adaptivecards.io/schemas/1.2.0/adaptive-card.json)，用于编辑和验证 json 格式的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="05d7d-112">We have provided a complete [JSON Schema file](https://adaptivecards.io/schemas/1.2.0/adaptive-card.json) for editing and validating adaptive cards in json.</span></span> <span data-ttu-id="05d7d-113">请注意，架构 URL 进行了版本控制，较新版的自适应卡片会有相应的 URL。</span><span class="sxs-lookup"><span data-stu-id="05d7d-113">Note that the schema URL is versioned, newer versions of Adaptive Cards will have a corresponding URL.</span></span>

<span data-ttu-id="05d7d-114">在 Visual Studio 和 Visual Studio Code 中，添加一个 `$schema` 引用即可获取自动 Intellisense。</span><span class="sxs-lookup"><span data-stu-id="05d7d-114">In Visual Studio and Visual Studio Code you can get automatic Intellisense by including a `$schema` reference.</span></span>

![无效](media/tools/invalidjson1.png)

![自动完成](media/tools/autocomplete.png)

## <a name="example"></a><span data-ttu-id="05d7d-117">示例</span><span class="sxs-lookup"><span data-stu-id="05d7d-117">Example</span></span>

```json
{
    "$schema": "http://adaptivecards.io/schemas/1.2.0/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": []
}
```

## <a name="visual-studio-code-extensions"></a><span data-ttu-id="05d7d-118">Visual Studio Code 扩展</span><span class="sxs-lookup"><span data-stu-id="05d7d-118">Visual Studio Code Extensions</span></span>

### <a name="adaptive-cards-studio"></a><span data-ttu-id="05d7d-119">**自适应卡片设计器**</span><span class="sxs-lookup"><span data-stu-id="05d7d-119">**Adaptive Cards Studio**</span></span>

![市场](https://madewithcards.blob.core.windows.net/uploads/29bb3d02-2158-40b8-8420-4dd1f15da34c-acstudio.png)

<span data-ttu-id="05d7d-121">通过自适应卡片设计器，可以直接在 Visual Studio Code 中创建卡片。</span><span class="sxs-lookup"><span data-stu-id="05d7d-121">With AdaptiveCards Studio you can author cards directly in Visual Studio Code.</span></span> <span data-ttu-id="05d7d-122">该扩展会自动检测工作区中的所有自适应卡片，让你可以轻松编辑卡片模板和示例数据。</span><span class="sxs-lookup"><span data-stu-id="05d7d-122">The Extension automatically detects all Adaptive Cards in your working space and lets you easily edit the card template and sample data.</span></span>

[<span data-ttu-id="05d7d-123">在 Visual Studio Code 市场了解详细信息并进行安装</span><span class="sxs-lookup"><span data-stu-id="05d7d-123">Read more and install it from the Visual Studio Code Marketplace</span></span>](https://marketplace.visualstudio.com/items?itemName=madewithcardsio.adaptivecardsstudiobeta)


### <a name="adaptive-card-viewer"></a><span data-ttu-id="05d7d-124">**自适应卡片查看器**</span><span class="sxs-lookup"><span data-stu-id="05d7d-124">**Adaptive Card Viewer**</span></span>

<span data-ttu-id="05d7d-125">我们创建了一个 Visual Studio Code 扩展，让你可以在编辑器中实时查看正在编辑的卡片。</span><span class="sxs-lookup"><span data-stu-id="05d7d-125">We have created a Visual Studio code extension which allows you to visualize the card you are editing in real time inside the editor itself.</span></span> 

![扩展](media/tools/vscode-extension.png)

<span data-ttu-id="05d7d-127">若要进行安装，请打开“扩展市场”，然后搜索“自适应卡片查看器”。</span><span class="sxs-lookup"><span data-stu-id="05d7d-127">To install, open Extensions Marketplace and search for **Adaptive Card Viewer**.</span></span>

![市场](media/tools/vscode-extension-marketplace.png)

### <a name="usage"></a><span data-ttu-id="05d7d-129">用法</span><span class="sxs-lookup"><span data-stu-id="05d7d-129">Usage</span></span>

<span data-ttu-id="05d7d-130">编辑包含自适应卡片 `$schema` 属性的 .json 文件时，可以使用 `Ctrl+Shift+V A` 来查看。</span><span class="sxs-lookup"><span data-stu-id="05d7d-130">When you are editing a .json file with an Adaptive Card `$schema` property you can view by using `Ctrl+Shift+V A`.</span></span>
```json
{
    "$schema": "http://adaptivecards.io/schemas/1.2.0/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": []
}
```

### <a name="options"></a><span data-ttu-id="05d7d-131">选项</span><span class="sxs-lookup"><span data-stu-id="05d7d-131">Options</span></span>

<span data-ttu-id="05d7d-132">以下 Visual Studio Code 设置适用于自适应卡片查看器。</span><span class="sxs-lookup"><span data-stu-id="05d7d-132">The following Visual Studio Code setting is available for the AdaptiveCards Viewer.</span></span> <span data-ttu-id="05d7d-133">可以在“用户设置”或“工作区设置”中进行设置。</span><span class="sxs-lookup"><span data-stu-id="05d7d-133">This can be set in User Settings or Workspace Settings.</span></span>

```js
{
    // Open or not open the preview screen automatically
    "adaptivecardsviewer.enableautopreview": true,
}
```

## <a name="wpf-visualizer-sample"></a><span data-ttu-id="05d7d-134">WPF 可视化工具示例</span><span class="sxs-lookup"><span data-stu-id="05d7d-134">WPF Visualizer Sample</span></span>

<span data-ttu-id="05d7d-135">可以通过 [WPF 可视化工具示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer)在 Windows 计算机上使用 WPF/Xaml 实现卡片的可视化。</span><span class="sxs-lookup"><span data-stu-id="05d7d-135">The [WPF visualizer sample project](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer) lets you visualize cards using WPF/Xaml on a Windows machine.</span></span>  <span data-ttu-id="05d7d-136">已经内置了 `hostconfig` 编辑器，因此可以编辑和查看 host config 设置。</span><span class="sxs-lookup"><span data-stu-id="05d7d-136">A `hostconfig` editor is built in for editing and viewing host config settings.</span></span> <span data-ttu-id="05d7d-137">将这些设置另存为 JSON，即可在应用程序中将它们用于呈现。</span><span class="sxs-lookup"><span data-stu-id="05d7d-137">Save these settings as a JSON to use them in rendering in your application.</span></span>

![wpf 可视化工具](media/tools/wpfvisualizer.png)

## <a name="wpf-imagerender-sample"></a><span data-ttu-id="05d7d-139">WPF ImageRender 示例</span><span class="sxs-lookup"><span data-stu-id="05d7d-139">WPF ImageRender Sample</span></span>

<span data-ttu-id="05d7d-140">使用 [ImageRender 示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/AdaptiveCards.Sample.ImageRender)，可以通过 WPF 在命令行中将任何卡片转换成 PNG。</span><span class="sxs-lookup"><span data-stu-id="05d7d-140">The [ImageRender sample project](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/AdaptiveCards.Sample.ImageRender) turns any card into a PNG from the command line using WPF.</span></span> 
