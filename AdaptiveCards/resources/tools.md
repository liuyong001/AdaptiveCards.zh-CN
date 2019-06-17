---
title: 自适应卡工具
author: matthidinger
ms.author: mahiding
ms.date: 03/14/2019
ms.topic: article
ms.openlocfilehash: ad520693224509deaf0ea1c2cd6a837089dbf2d5
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67137980"
---
# <a name="tools-and-samples"></a><span data-ttu-id="d4b6e-102">工具和示例</span><span class="sxs-lookup"><span data-stu-id="d4b6e-102">Tools and Samples</span></span>

## <a name="card-designer"></a><span data-ttu-id="d4b6e-103">卡设计器</span><span class="sxs-lookup"><span data-stu-id="d4b6e-103">Card Designer</span></span> 

<span data-ttu-id="d4b6e-104">需要工具来设计您的卡？</span><span class="sxs-lookup"><span data-stu-id="d4b6e-104">Need for a tool to design your cards?</span></span> <span data-ttu-id="d4b6e-105">请关注处的基于浏览器的自适应卡设计器 [https://adaptivecards.io/designer](https://adaptivecards.io/designer)</span><span class="sxs-lookup"><span data-stu-id="d4b6e-105">Look no further than the browser-based adaptive card designer at [https://adaptivecards.io/designer](https://adaptivecards.io/designer)</span></span>

<span data-ttu-id="d4b6e-106">[![设计器的屏幕截图](media/tools/designer.jpg)](https://adaptivecards.io/designer)</span><span class="sxs-lookup"><span data-stu-id="d4b6e-106">[![designer screenshot](media/tools/designer.jpg)](https://adaptivecards.io/designer)</span></span>

### <a name="embed-the-designer-into-your-app"></a><span data-ttu-id="d4b6e-107">将在设计器嵌入到您的应用程序</span><span class="sxs-lookup"><span data-stu-id="d4b6e-107">Embed the designer into your app</span></span>

<span data-ttu-id="d4b6e-108">但为什么时你可以那里发送你的用户**卡设计器将直接嵌入到你的 web**使用我们的 JavaScript 库应用程序。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-108">But why send your users there when you can **embed the card designer directly into your web** app using our JavaScript library.</span></span> 

<span data-ttu-id="d4b6e-109">请查看[adaptivecards 设计器](https://npmjs.com/adaptivecards-designer)入门程序包。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-109">Check out the [adaptivecards-designer](https://npmjs.com/adaptivecards-designer) package to get started.</span></span>

## <a name="schema-validation"></a><span data-ttu-id="d4b6e-110">架构验证</span><span class="sxs-lookup"><span data-stu-id="d4b6e-110">Schema validation</span></span>

<span data-ttu-id="d4b6e-111">架构验证是更轻松地创作和启用工具的一种强大方法。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-111">Schema validation is a powerful way of making authoring easier and enabling tooling.</span></span>

<span data-ttu-id="d4b6e-112">我们提供了一个完整[JSON 架构文件](http://adaptivecards.io/schemas/1.2.0/adaptive-card.json)用于编辑和验证 json 中的自适应卡。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-112">We have provided a complete [JSON Schema file](http://adaptivecards.io/schemas/1.2.0/adaptive-card.json) for editing and validating adaptive cards in json.</span></span> <span data-ttu-id="d4b6e-113">请注意，架构 URL 进行版本控制，较新版本的自适应卡将具有相应的 URL。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-113">Note that the schema URL is versioned, newer versions of Adaptive Cards will have a corresponding URL.</span></span>

<span data-ttu-id="d4b6e-114">在 Visual Studio 和 Visual Studio Code 中你可以通过获取自动 Intellisense`$schema`引用。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-114">In Visual Studio and Visual Studio Code you can get automatic Intellisense by including a `$schema` reference.</span></span>

![错误](media/tools/invalidjson1.png)

![记忆式键入功能](media/tools/autocomplete.png)

## <a name="example"></a><span data-ttu-id="d4b6e-117">示例</span><span class="sxs-lookup"><span data-stu-id="d4b6e-117">Example</span></span>

```json
{
    "$schema": "http://adaptivecards.io/schemas/1.2.0/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": []
}
```

## <a name="visual-studio-code-extension"></a><span data-ttu-id="d4b6e-118">Visual Studio Code 扩展</span><span class="sxs-lookup"><span data-stu-id="d4b6e-118">Visual Studio Code Extension</span></span>

<span data-ttu-id="d4b6e-119">我们创建了 Visual Studio code 扩展可用于可视化编辑本身在编辑器内实时的卡。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-119">We have created a Visual Studio code extension which allows you to visualize the card you are editing in real time inside the editor itself.</span></span> 

![扩展](media/tools/vscode-extension.png)

<span data-ttu-id="d4b6e-121">若要安装，打开扩展应用商店并搜索**自适应卡查看器**。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-121">To install, open Extensions Marketplace and search for **Adaptive Card Viewer**.</span></span>

![Marketplace](media/tools/vscode-extension-marketplace.png)

### <a name="usage"></a><span data-ttu-id="d4b6e-123">用法</span><span class="sxs-lookup"><span data-stu-id="d4b6e-123">Usage</span></span>

<span data-ttu-id="d4b6e-124">当正在.json 文件编辑自适应卡`$schema`属性可以通过查看`Ctrl+Shift+V A`。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-124">When you are editing a .json file with an Adaptive Card `$schema` property you can view by using `Ctrl+Shift+V A`.</span></span>
```json
{
    "$schema": "http://adaptivecards.io/schemas/1.2.0/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": []
}
```

### <a name="options"></a><span data-ttu-id="d4b6e-125">选项</span><span class="sxs-lookup"><span data-stu-id="d4b6e-125">Options</span></span>

<span data-ttu-id="d4b6e-126">以下 Visual Studio Code 设置是适用于 AdaptiveCards 查看器。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-126">The following Visual Studio Code setting is available for the AdaptiveCards Viewer.</span></span> <span data-ttu-id="d4b6e-127">这可以在用户设置或工作区设置中设置。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-127">This can be set in User Settings or Workspace Settings.</span></span>

```js
{
    // Open or not open the preview screen automatically
    "adaptivecardsviewer.enableautopreview": true,
}
```

## <a name="wpf-visualizer-sample"></a><span data-ttu-id="d4b6e-128">WPF 可视化工具示例</span><span class="sxs-lookup"><span data-stu-id="d4b6e-128">WPF Visualizer Sample</span></span>

<span data-ttu-id="d4b6e-129">[WPF 可视化工具示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer)允许您直观地显示在 Windows 计算机上使用 WPF/Xaml 的卡。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-129">The [WPF visualizer sample project](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/WPFVisualizer) lets you visualize cards using WPF/Xaml on a Windows machine.</span></span>  <span data-ttu-id="d4b6e-130">一个`hostconfig`编辑器生成用于编辑和查看主机的配置设置。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-130">A `hostconfig` editor is built in for editing and viewing host config settings.</span></span> <span data-ttu-id="d4b6e-131">将这些设置保存为 JSON 中呈现应用程序中使用它们。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-131">Save these settings as a JSON to use them in rendering in your application.</span></span>

![wpf 可视化工具](media/tools/wpfvisualizer.png)

## <a name="wpf-imagerender-sample"></a><span data-ttu-id="d4b6e-133">WPF ImageRender 示例</span><span class="sxs-lookup"><span data-stu-id="d4b6e-133">WPF ImageRender Sample</span></span>

<span data-ttu-id="d4b6e-134">[ImageRender 示例项目](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/AdaptiveCards.Sample.ImageRender)将任何卡转变为从命令行使用 WPF PNG。</span><span class="sxs-lookup"><span data-stu-id="d4b6e-134">The [ImageRender sample project](https://github.com/Microsoft/AdaptiveCards/tree/master/source/dotnet/Samples/AdaptiveCards.Sample.ImageRender) turns any card into a PNG from the command line using WPF.</span></span> 
