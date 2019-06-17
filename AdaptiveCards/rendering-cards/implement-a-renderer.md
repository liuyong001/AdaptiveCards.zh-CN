---
title: 实现呈现器
author: matthidinger
ms.author: mahiding
ms.date: 09/15/2017
ms.topic: article
ms.openlocfilehash: b39493f82f3378e5a554abc6df890d6821869671
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67138020"
---
# <a name="adaptive-card-renderer-specification"></a><span data-ttu-id="ad58f-102">自适应卡呈现器规范</span><span class="sxs-lookup"><span data-stu-id="ad58f-102">Adaptive Card Renderer Specification</span></span>

<span data-ttu-id="ad58f-103">以下规范介绍如何实现在任何 UI 平台上的自适应卡呈现器。</span><span class="sxs-lookup"><span data-stu-id="ad58f-103">The following specification describes how implement an Adaptive Card renderer on any UI platform.</span></span>

> [!IMPORTANT]
> 
> <span data-ttu-id="ad58f-104">此内容尚未完成。</span><span class="sxs-lookup"><span data-stu-id="ad58f-104">This content is not finished yet.</span></span> <span data-ttu-id="ad58f-105">请稍后查看。</span><span class="sxs-lookup"><span data-stu-id="ad58f-105">Check back shortly.</span></span>

## <a name="sdk-versioning"></a><span data-ttu-id="ad58f-106">SDK 版本控制</span><span class="sxs-lookup"><span data-stu-id="ad58f-106">SDK Versioning</span></span>

1. <span data-ttu-id="ad58f-107">SDK 的主要和次要版本**应该**匹配`schema`版本。</span><span class="sxs-lookup"><span data-stu-id="ad58f-107">The SDK major and minor version **SHOULD** match the `schema` version.</span></span> 
1. <span data-ttu-id="ad58f-108">修补程序/build**应该**用于呈现器没有架构更改的更新。</span><span class="sxs-lookup"><span data-stu-id="ad58f-108">Patch/build **SHOULD** be used for renderer updates that don't have schema changes.</span></span>

## <a name="parsing-json"></a><span data-ttu-id="ad58f-109">分析 JSON</span><span class="sxs-lookup"><span data-stu-id="ad58f-109">Parsing JSON</span></span>

### <a name="error-conditions"></a><span data-ttu-id="ad58f-110">错误条件</span><span class="sxs-lookup"><span data-stu-id="ad58f-110">Error conditions</span></span>
1. <span data-ttu-id="ad58f-111">一个分析器**必须**检查它是否是有效的 JSON 内容</span><span class="sxs-lookup"><span data-stu-id="ad58f-111">A parser **MUST** check that it's valid JSON content</span></span>
1. <span data-ttu-id="ad58f-112">一个分析器**必须**根据架构 （必需的属性，等等） 进行验证</span><span class="sxs-lookup"><span data-stu-id="ad58f-112">A parser **MUST** validate against the schema (required properties, etc)</span></span>
1. <span data-ttu-id="ad58f-113">上述错误**必须**报告给主机应用程序 （异常或权限相同者）</span><span class="sxs-lookup"><span data-stu-id="ad58f-113">The above errors **MUST** be reported to the host app (exception or equivalent)</span></span>

### <a name="unknown-types"></a><span data-ttu-id="ad58f-114">未知的类型</span><span class="sxs-lookup"><span data-stu-id="ad58f-114">Unknown types</span></span>
1. <span data-ttu-id="ad58f-115">如果遇到未知"类型"他们**必须先删除**从结果</span><span class="sxs-lookup"><span data-stu-id="ad58f-115">If unknown "types" are encountered they **MUST BE DROPPED** from the result</span></span>
1. <span data-ttu-id="ad58f-116">有效负载 （例如，上面） 的任何变更**应该**被报告为警告记录到主机应用程序</span><span class="sxs-lookup"><span data-stu-id="ad58f-116">Any alterations of the payload (like above) **SHOULD** be reported as warnings to the host app</span></span>

### <a name="unknown-properties"></a><span data-ttu-id="ad58f-117">未知的属性</span><span class="sxs-lookup"><span data-stu-id="ad58f-117">Unknown properties</span></span>
1. <span data-ttu-id="ad58f-118">一个分析器**必须**包括**其他**元素上的属性</span><span class="sxs-lookup"><span data-stu-id="ad58f-118">A parser **MUST** include **additional** properties on elements</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="ad58f-119">其他注意事项</span><span class="sxs-lookup"><span data-stu-id="ad58f-119">Additional considerations</span></span>
1. <span data-ttu-id="ad58f-120">`speak`属性可能包含 SSML 标记和**必须**返回到指定为主机应用程序</span><span class="sxs-lookup"><span data-stu-id="ad58f-120">The `speak` property may contain SSML markup and **MUST** be returned to the host app as-specified</span></span>

## <a name="parsing-host-config"></a><span data-ttu-id="ad58f-121">分析主机配置</span><span class="sxs-lookup"><span data-stu-id="ad58f-121">Parsing Host Config</span></span>
1. <span data-ttu-id="ad58f-122">TODO</span><span class="sxs-lookup"><span data-stu-id="ad58f-122">TODO</span></span>

## <a name="versioning"></a><span data-ttu-id="ad58f-123">版本控制</span><span class="sxs-lookup"><span data-stu-id="ad58f-123">Versioning</span></span>

1. <span data-ttu-id="ad58f-124">呈现器**必须**实现了特定架构版本。</span><span class="sxs-lookup"><span data-stu-id="ad58f-124">A renderer **MUST** implement a particular version of the schema.</span></span> 
1. <span data-ttu-id="ad58f-125">`AdaptiveCard`构造函数**必须**提供`version`属性默认值基于当前的架构版本</span><span class="sxs-lookup"><span data-stu-id="ad58f-125">The `AdaptiveCard` constructor **MUST** give the `version` property a default value based on the current schema version</span></span> 
1. <span data-ttu-id="ad58f-126">如果呈现器遇到`version`中的属性`AdaptiveCard`高于受支持的版本，它**必须**返回`fallbackText`相反。</span><span class="sxs-lookup"><span data-stu-id="ad58f-126">If a renderer encounters a `version` property in the `AdaptiveCard` that is higher than the supported version, it **MUST** return the `fallbackText` instead.</span></span>

## <a name="rendering"></a><span data-ttu-id="ad58f-127">渲染</span><span class="sxs-lookup"><span data-stu-id="ad58f-127">Rendering</span></span>

<span data-ttu-id="ad58f-128">`AdaptiveCard`组成`body`和`actions`。</span><span class="sxs-lookup"><span data-stu-id="ad58f-128">An `AdaptiveCard` consists of a `body` and `actions`.</span></span> <span data-ttu-id="ad58f-129">`body`是一系列`CardElement`s，呈现器将枚举并按顺序呈现。</span><span class="sxs-lookup"><span data-stu-id="ad58f-129">The `body` is a collection of `CardElement`s that a renderer will enumerate and render in order.</span></span> 

1. <span data-ttu-id="ad58f-130">每个元素**必须**拉伸到其父项的宽度 (认为`display: block`以 html 格式)。</span><span class="sxs-lookup"><span data-stu-id="ad58f-130">Each Element **MUST** stretch to the width of its parent (think `display: block` in HTML).</span></span>
1. <span data-ttu-id="ad58f-131">呈现器**必须**忽略未知的元素类型，并继续呈现有效负载的其余部分。</span><span class="sxs-lookup"><span data-stu-id="ad58f-131">A renderer **MUST** ignore unknown element types, and continue rendering the rest of the payload.</span></span>

### <a name="spacing-and-separators"></a><span data-ttu-id="ad58f-132">间距和分隔符</span><span class="sxs-lookup"><span data-stu-id="ad58f-132">Spacing and Separators</span></span>

1. <span data-ttu-id="ad58f-133">`spacing`上的每个元素的属性会影响之间的空间量**当前**元素和一个**BEFORE**它。</span><span class="sxs-lookup"><span data-stu-id="ad58f-133">The `spacing` property on every element influences the amount of space between the **CURRENT** element and the one **BEFORE** it.</span></span>
1. <span data-ttu-id="ad58f-134">间距**必须仅**应用存在实际上是其前面的元素时。</span><span class="sxs-lookup"><span data-stu-id="ad58f-134">Spacing **MUST ONLY** apply when there actually is an element preceding it.</span></span> <span data-ttu-id="ad58f-135">（例如，不会应用于数组中的第一项）</span><span class="sxs-lookup"><span data-stu-id="ad58f-135">(E.g., won't apply to the first item in an array)</span></span>
1. <span data-ttu-id="ad58f-136">呈现器**必须**查找要使用的空间量`hostConfig`应用于当前元素的枚举值的间距。</span><span class="sxs-lookup"><span data-stu-id="ad58f-136">A renderer **MUST** look up the amount of space to use from the `hostConfig` spacing for the enum value applied to the current element.</span></span>
1. <span data-ttu-id="ad58f-137">如果元素具有`separator`的值`true`，然后可见的行**必须**当前元素与前一个之间绘制。</span><span class="sxs-lookup"><span data-stu-id="ad58f-137">If the element has a `separator` value of `true`, then a visible line **MUST** be drawn between the current element and the one before it.</span></span>
1. <span data-ttu-id="ad58f-138">分隔线**必须**将使用绘制`container.style.default.foregroundColor`。</span><span class="sxs-lookup"><span data-stu-id="ad58f-138">The separator line **MUST** be drawn using the `container.style.default.foregroundColor`.</span></span>
1. <span data-ttu-id="ad58f-139">分隔符**必须仅**如果绘制该项**IS NOT**数组中的第一个。</span><span class="sxs-lookup"><span data-stu-id="ad58f-139">A separator **MUST ONLY** be drawn if the item **IS NOT** the first in the array.</span></span>

### <a name="columns"></a><span data-ttu-id="ad58f-140">列</span><span class="sxs-lookup"><span data-stu-id="ad58f-140">Columns</span></span>

1. <span data-ttu-id="ad58f-141">`Column` `width` **必须**解释按"auto"、"stretch"或加权的比率。</span><span class="sxs-lookup"><span data-stu-id="ad58f-141">`Column` `width` **MUST** be interpreted by "auto", "stretch" or a weighted ratio.</span></span>

### <a name="textblock"></a><span data-ttu-id="ad58f-142">TextBlock</span><span class="sxs-lookup"><span data-stu-id="ad58f-142">TextBlock</span></span>

1. <span data-ttu-id="ad58f-143">TextBlock**必须**占用单个行，除非`wrap`属性是`true`。</span><span class="sxs-lookup"><span data-stu-id="ad58f-143">A TextBlock **MUST** take up a single line unless the `wrap` property is `true`.</span></span> 
1. <span data-ttu-id="ad58f-144">文本块**应该**剪裁带省略号 （...） 的任何多余文本</span><span class="sxs-lookup"><span data-stu-id="ad58f-144">The text block **SHOULD** trim any excess text with an ellipsis (...)</span></span>

#### <a name="markdown"></a><span data-ttu-id="ad58f-145">Markdown</span><span class="sxs-lookup"><span data-stu-id="ad58f-145">Markdown</span></span>

1. <span data-ttu-id="ad58f-146">自适应卡允许对 Markdown 的子集并**应该**中支持`TextBlock`。</span><span class="sxs-lookup"><span data-stu-id="ad58f-146">Adaptive Cards allow for a subset of Markdown and **SHOULD** be supported in `TextBlock`.</span></span> 
1. <span data-ttu-id="ad58f-147">请参阅完整[markdown 要求](../authoring-cards/text-features.md)</span><span class="sxs-lookup"><span data-stu-id="ad58f-147">See full [markdown requirements](../authoring-cards/text-features.md)</span></span>

#### <a name="formatting-functions"></a><span data-ttu-id="ad58f-148">格式设置函数</span><span class="sxs-lookup"><span data-stu-id="ad58f-148">Formatting functions</span></span>

1. <span data-ttu-id="ad58f-149">`TextBlock` 允许[日期/时间格式设置函数](../authoring-cards/text-features.md)的**必须**上每个呈现器支持。</span><span class="sxs-lookup"><span data-stu-id="ad58f-149">`TextBlock` allows [DATE/TIME formatting functions](../authoring-cards/text-features.md) that **MUST** be supported on every renderer.</span></span>
1. <span data-ttu-id="ad58f-150">**所有故障必须**卡中显示的原始字符串。</span><span class="sxs-lookup"><span data-stu-id="ad58f-150">**ALL FAILURES MUST** display the raw string in the card.</span></span> <span data-ttu-id="ad58f-151">尝试无友好消息。</span><span class="sxs-lookup"><span data-stu-id="ad58f-151">No friendly message attempted.</span></span> <span data-ttu-id="ad58f-152">（要使开发人员立即知道存在的目标是问题）</span><span class="sxs-lookup"><span data-stu-id="ad58f-152">(The goal being to make the developer immediately aware there is a problem)</span></span>

1. <span data-ttu-id="ad58f-153">TODO:包含正则表达式</span><span class="sxs-lookup"><span data-stu-id="ad58f-153">TODO: Include regex</span></span>

### <a name="images"></a><span data-ttu-id="ad58f-154">映像</span><span class="sxs-lookup"><span data-stu-id="ad58f-154">Images</span></span>

1. <span data-ttu-id="ad58f-155">呈现器**应该**允许主机应用程序知道所有 HTTP 映像都下载时和卡"完全呈现"</span><span class="sxs-lookup"><span data-stu-id="ad58f-155">A renderer **SHOULD** allow host apps to know when all HTTP images have been downloaded and the card is "fully rendered"</span></span>
1. <span data-ttu-id="ad58f-156">呈现器**必须**检查主机配置`maxImageSize`param 时下载 HTTP 图像</span><span class="sxs-lookup"><span data-stu-id="ad58f-156">A renderer **MUST** inspect the Host Config `maxImageSize` param when downloading HTTP images</span></span>
1. <span data-ttu-id="ad58f-157">呈现器**必须**支持`.png`和 `.jpeg`</span><span class="sxs-lookup"><span data-stu-id="ad58f-157">A renderer **MUST** support `.png` and `.jpeg`</span></span>
1. <span data-ttu-id="ad58f-158">呈现器**应该**支持`.gif`映像</span><span class="sxs-lookup"><span data-stu-id="ad58f-158">A renderer **SHOULD** support `.gif` images</span></span>

### <a name="host-config"></a><span data-ttu-id="ad58f-159">主机配置</span><span class="sxs-lookup"><span data-stu-id="ad58f-159">Host Config</span></span>

* <span data-ttu-id="ad58f-160">TODO:默认值应该是什么？</span><span class="sxs-lookup"><span data-stu-id="ad58f-160">TODO: What should the defaults be?</span></span> <span data-ttu-id="ad58f-161">它们都应共享它？</span><span class="sxs-lookup"><span data-stu-id="ad58f-161">Should they all share it?</span></span> <span data-ttu-id="ad58f-162">我们应在二进制文件中嵌入常见的 hostConfig.json 文件？</span><span class="sxs-lookup"><span data-stu-id="ad58f-162">Should we embed a common hostConfig.json file in the binaries?</span></span>
* <span data-ttu-id="ad58f-163">TODO:我认为 HostConfig 需要进行版本控制也用于分析？</span><span class="sxs-lookup"><span data-stu-id="ad58f-163">TODO: I think HostConfig needs to be versioned as well for parsing?</span></span>

<span data-ttu-id="ad58f-164">[`HostConfig`](host-config.md) 是一个共享的配置对象，指定如何为自适应的卡片呈现器生成 UI。</span><span class="sxs-lookup"><span data-stu-id="ad58f-164">[`HostConfig`](host-config.md) is a shared configuration object that specifies how an Adaptive Card Renderer generates UI.</span></span>  

<span data-ttu-id="ad58f-165">这样，是平台不可知的在不同平台和设备上的呈现器之间共享的属性。</span><span class="sxs-lookup"><span data-stu-id="ad58f-165">This allows properties which are platform agnostic to be shared among renderers on different platforms and devices.</span></span> <span data-ttu-id="ad58f-166">它还允许工具创建这您的卡外观和感觉会为给定的环境。</span><span class="sxs-lookup"><span data-stu-id="ad58f-166">It also allows tooling to be created which gives you an idea of the look and feel that card would have for a given environment.</span></span>

1. <span data-ttu-id="ad58f-167">呈现器**必须**公开**主机配置**托管应用程序的参数</span><span class="sxs-lookup"><span data-stu-id="ad58f-167">Renderers **MUST** expose a **Host Config** parameter to host apps</span></span>
1. <span data-ttu-id="ad58f-168">所有元素**必须**根据其各自的主机配置设置来设置样式</span><span class="sxs-lookup"><span data-stu-id="ad58f-168">All elements **MUST** be styled according to their respective Host Config settings</span></span>

### <a name="native-platform-styling"></a><span data-ttu-id="ad58f-169">本机平台样式设置</span><span class="sxs-lookup"><span data-stu-id="ad58f-169">Native platform styling</span></span>

1. <span data-ttu-id="ad58f-170">每个元素类型**应该**附加本机平台样式与生成的 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="ad58f-170">Each element type **SHOULD** attach a native platform style with the generated UI element.</span></span> <span data-ttu-id="ad58f-171">例如，在 HTML 中我们添加了一个 CSS 类的元素类型，并在 XAML 中我们将分配特定样式。</span><span class="sxs-lookup"><span data-stu-id="ad58f-171">E.g., in HTML we added a CSS class to the element types, and in XAML we assign a specific Style.</span></span>

## <a name="extensibility"></a><span data-ttu-id="ad58f-172">扩展性</span><span class="sxs-lookup"><span data-stu-id="ad58f-172">Extensibility</span></span> 

1. <span data-ttu-id="ad58f-173">呈现器**必须**允许重写默认元素呈现器的主机应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad58f-173">A renderer **MUST** allow host apps to override default element renderers.</span></span> <span data-ttu-id="ad58f-174">例如，替换`TextBlock`呈现具有其自己的逻辑。</span><span class="sxs-lookup"><span data-stu-id="ad58f-174">E.g., replace `TextBlock` rendering with their own logic.</span></span>
1. <span data-ttu-id="ad58f-175">呈现器**必须**允许注册自定义元素类型的主机应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad58f-175">A renderer **MUST** allow host apps to register custom element types.</span></span> <span data-ttu-id="ad58f-176">例如，添加对自定义支持`Rating`元素</span><span class="sxs-lookup"><span data-stu-id="ad58f-176">E.g., add support for a custom `Rating` element</span></span>
1. <span data-ttu-id="ad58f-177">呈现器**必须**允许删除默认元素对的支持的主机应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad58f-177">A renderer **MUST** allow host apps to remove support for a default element.</span></span> <span data-ttu-id="ad58f-178">例如，删除`Action.Submit`如果他们不想让它支持。</span><span class="sxs-lookup"><span data-stu-id="ad58f-178">E.g., remove `Action.Submit` if they don't want it supported.</span></span>

## <a name="actions"></a><span data-ttu-id="ad58f-179">操作</span><span class="sxs-lookup"><span data-stu-id="ad58f-179">Actions</span></span>

1. <span data-ttu-id="ad58f-180">如果 HostConfig`supportsInteractivity`是`false`，将呈现器**不得**呈现的任何操作。</span><span class="sxs-lookup"><span data-stu-id="ad58f-180">If HostConfig `supportsInteractivity` is `false`, a renderer **MUST NOT** render any actions.</span></span>
1. <span data-ttu-id="ad58f-181">`actions`属性**必须**呈现为某种类型的操作栏中，通常是在卡的底部中的按钮。</span><span class="sxs-lookup"><span data-stu-id="ad58f-181">The `actions` property **MUST** be rendered as buttons in some kind of action bar, usually at the bottom of the card.</span></span> 
1. <span data-ttu-id="ad58f-182">点击按钮时它**必须**允许主机应用程序以处理事件。</span><span class="sxs-lookup"><span data-stu-id="ad58f-182">When a button is tapped it **MUST** allow the host app to handle the event.</span></span> 
1. <span data-ttu-id="ad58f-183">事件**必须**与操作的所有关联属性一起传递</span><span class="sxs-lookup"><span data-stu-id="ad58f-183">The event **MUST** pass along all associated properties with the action</span></span>
1. <span data-ttu-id="ad58f-184">事件**必须**传递`AdaptiveCard`执行所用</span><span class="sxs-lookup"><span data-stu-id="ad58f-184">The event **MUST** pass along the `AdaptiveCard` which was executed</span></span>

<span data-ttu-id="ad58f-185">操作</span><span class="sxs-lookup"><span data-stu-id="ad58f-185">Action</span></span> | <span data-ttu-id="ad58f-186">行为</span><span class="sxs-lookup"><span data-stu-id="ad58f-186">Behavior</span></span>
--- | ---
<span data-ttu-id="ad58f-187">**Action.OpenUrl**</span><span class="sxs-lookup"><span data-stu-id="ad58f-187">**Action.OpenUrl**</span></span> | <span data-ttu-id="ad58f-188">打开外部 URL 以进行查看</span><span class="sxs-lookup"><span data-stu-id="ad58f-188">Open an external URL for viewing</span></span>
<span data-ttu-id="ad58f-189">**Action.ShowCard**</span><span class="sxs-lookup"><span data-stu-id="ad58f-189">**Action.ShowCard**</span></span> | <span data-ttu-id="ad58f-190">请求子卡以向用户显示。</span><span class="sxs-lookup"><span data-stu-id="ad58f-190">Requests a sub-card to be shown to the user.</span></span>
<span data-ttu-id="ad58f-191">**Action.Submit**</span><span class="sxs-lookup"><span data-stu-id="ad58f-191">**Action.Submit**</span></span> | <span data-ttu-id="ad58f-192">要求所有的输入元素收集到的对象，然后将它发送给你通过主机应用程序定义的一些方法。</span><span class="sxs-lookup"><span data-stu-id="ad58f-192">Ask for all of the input elements to be gathered up into an object which is then sent to you through some method defined by the host application.</span></span>

### <a name="actionopenurl"></a><span data-ttu-id="ad58f-193">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="ad58f-193">Action.OpenUrl</span></span>
1. <span data-ttu-id="ad58f-194">`Action.OpenUrl` **应**打开使用本机平台机制的 URL</span><span class="sxs-lookup"><span data-stu-id="ad58f-194">`Action.OpenUrl` **SHOULD** open a URL using the native platform mechanism</span></span>
1. <span data-ttu-id="ad58f-195">如果无法做到这一点它**必须**事件引发到主机应用程序以处理打开 URL。</span><span class="sxs-lookup"><span data-stu-id="ad58f-195">If this is not possible it **MUST** raise an event to the host app to handle opening the URL.</span></span> <span data-ttu-id="ad58f-196">此事件**必须**允许主机应用程序以重写默认行为。</span><span class="sxs-lookup"><span data-stu-id="ad58f-196">This event **MUST** allow the host app to override the default behavior.</span></span> <span data-ttu-id="ad58f-197">例如，让他们打开自己的应用中的 URL。</span><span class="sxs-lookup"><span data-stu-id="ad58f-197">E.g., let them open the URL within their own app.</span></span>

### <a name="actionshowcard"></a><span data-ttu-id="ad58f-198">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="ad58f-198">Action.ShowCard</span></span>

1. <span data-ttu-id="ad58f-199">`Action.ShowCard` **必须**以某种方式，根据 hostConfig 设置支持。</span><span class="sxs-lookup"><span data-stu-id="ad58f-199">`Action.ShowCard` **MUST** be supported in some way, based on the hostConfig setting.</span></span> <span data-ttu-id="ad58f-200">有两种模式： 以内联方式和弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="ad58f-200">There are two modes: inline, and popup.</span></span> <span data-ttu-id="ad58f-201">内联卡**应该**自动切换卡可见性。</span><span class="sxs-lookup"><span data-stu-id="ad58f-201">Inline cards **SHOULD** toggle the card visibility automatically.</span></span> <span data-ttu-id="ad58f-202">在弹出窗口模式下，事件**应该**触发到主机应用程序，以某种方式显示的卡片。</span><span class="sxs-lookup"><span data-stu-id="ad58f-202">In popup mode, an event **SHOULD** be fired to the host app to show the card in some way.</span></span>

### <a name="actionsubmit"></a><span data-ttu-id="ad58f-203">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="ad58f-203">Action.Submit</span></span>

<span data-ttu-id="ad58f-204">提交操作的行为类似于 HTML 窗体提交，则这些不同之处在于 HTML 通常触发 HTTP post，自适应卡最多保留它意味着每个主机应用程序，以确定什么"提交"。</span><span class="sxs-lookup"><span data-stu-id="ad58f-204">The Submit Action behaves like an HTML form submit, except that where HTML typically triggers an HTTP post, Adaptive Cards leaves it up to each host app to determine what "submit" means to them.</span></span> 

1. <span data-ttu-id="ad58f-205">当这**必须**引发的事件在用户点击调用的操作。</span><span class="sxs-lookup"><span data-stu-id="ad58f-205">When this **MUST** raise an event the user taps the action invoked.</span></span>  
1. <span data-ttu-id="ad58f-206">`data`属性**必须**包含回调有效负载中。</span><span class="sxs-lookup"><span data-stu-id="ad58f-206">The `data` property **MUST** be included in the callback payload.</span></span>
1. <span data-ttu-id="ad58f-207">有关`Action.Submit`，将呈现器**必须**收集在卡上的所有输入，并检索其值。</span><span class="sxs-lookup"><span data-stu-id="ad58f-207">For `Action.Submit`, a renderer **MUST** gather all inputs on the card and retrieve their values.</span></span> 

### <a name="selectaction"></a><span data-ttu-id="ad58f-208">selectAction</span><span class="sxs-lookup"><span data-stu-id="ad58f-208">selectAction</span></span>

1. <span data-ttu-id="ad58f-209">如果主机配置`supportedInteractivity`是`false`则`selectAction`**不得**触摸目标的方式进行呈现。</span><span class="sxs-lookup"><span data-stu-id="ad58f-209">If Host Config `supportedInteractivity` is `false` then a `selectAction` **MUST NOT** render as a touch target.</span></span>
1. <span data-ttu-id="ad58f-210">`Image``ColumnSet`，并`Column`提供`selectAction`属性，其中**应该**用户调用，例如，通过点击该元素时要执行。</span><span class="sxs-lookup"><span data-stu-id="ad58f-210">`Image`, `ColumnSet`, and `Column` offer a `selectAction` property, which **SHOULD** be executed when the user invokes it, e.g., by tapping the element.</span></span>

## <a name="inputs"></a><span data-ttu-id="ad58f-211">输入</span><span class="sxs-lookup"><span data-stu-id="ad58f-211">Inputs</span></span>

1. <span data-ttu-id="ad58f-212">如果 HostConfig`supportsInteractivity`是`false`呈现器**不得**呈现任何输入。</span><span class="sxs-lookup"><span data-stu-id="ad58f-212">If HostConfig `supportsInteractivity` is `false` a renderer **MUST NOT** render any inputs.</span></span>
2. <span data-ttu-id="ad58f-213">输入**应该**可能用最高的保真度呈现。</span><span class="sxs-lookup"><span data-stu-id="ad58f-213">Inputs **SHOULD** render with the highest fidelity possible.</span></span> <span data-ttu-id="ad58f-214">例如，`Input.Date`理想情况下将日期选取器提供给用户，但如果这不是您的 UI 堆栈，则呈现器可能**必须**故障回复到呈现标准文本框。</span><span class="sxs-lookup"><span data-stu-id="ad58f-214">For example, an `Input.Date` would ideally offer a date picker to a user, but if this isn't possible on your UI stack, then the renderer **MUST** fall back to rendering a standard text box.</span></span>
3. <span data-ttu-id="ad58f-215">呈现器**应该**显示`placeholderText`在可能的情况</span><span class="sxs-lookup"><span data-stu-id="ad58f-215">A renderer **SHOULD** display the `placeholderText` if possible</span></span>
4. <span data-ttu-id="ad58f-216">呈现器**不**必须实现的输入验证。</span><span class="sxs-lookup"><span data-stu-id="ad58f-216">A renderer **DOES NOT** have to implement validation of the input.</span></span> <span data-ttu-id="ad58f-217">自适应卡的用户必须规划以验证他们一端任何接收的数据。</span><span class="sxs-lookup"><span data-stu-id="ad58f-217">Users of Adaptive Cards must plan to validate any received data on their end.</span></span>
5. <span data-ttu-id="ad58f-218">输入值绑定**必须**正确转义</span><span class="sxs-lookup"><span data-stu-id="ad58f-218">Input value binding **MUST** be properly escaped</span></span>

6. <span data-ttu-id="ad58f-219">该对象**必须**返回到主机应用程序，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ad58f-219">The object **MUST** be returned to the host app as follows:</span></span>

   <span data-ttu-id="ad58f-220">我们没有使接收方以正确分析的响应取决于自适应卡中进行输入验证任何承诺。</span><span class="sxs-lookup"><span data-stu-id="ad58f-220">We do not make any promises of input validation in adaptive cards, so it's up to the receiving party to properly parse the response.</span></span> <span data-ttu-id="ad58f-221">例如，Input.Number 可能返回"你好"，并且他们需要作好准备。</span><span class="sxs-lookup"><span data-stu-id="ad58f-221">E.g., a Input.Number could return "hello" and they need to be prepared for that.</span></span>


## <a name="events"></a><span data-ttu-id="ad58f-222">Events</span><span class="sxs-lookup"><span data-stu-id="ad58f-222">Events</span></span>

1. <span data-ttu-id="ad58f-223">呈现器**应该**激发事件时已更改元素的可见性，允许主机应用程序向卡滚动到位。</span><span class="sxs-lookup"><span data-stu-id="ad58f-223">A renderer **SHOULD** fire an event when an element's visibility has changed, allowing the host app to scroll the card into position.</span></span>
