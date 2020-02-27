---
title: 实现呈现器
author: matthidinger
ms.author: mahiding
ms.date: 09/15/2017
ms.topic: article
ms.openlocfilehash: 607ce40e70e0e54e61a572853a521d2dd70a5c23
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454910"
---
# <a name="adaptive-card-renderer-specification"></a><span data-ttu-id="e6d3f-102">自适应卡片呈现器规范</span><span class="sxs-lookup"><span data-stu-id="e6d3f-102">Adaptive Card Renderer Specification</span></span>

<span data-ttu-id="e6d3f-103">以下规范介绍如何在任意 UI 平台上实现自适应卡片呈现器。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-103">The following specification describes how implement an Adaptive Card renderer on any UI platform.</span></span>

> [!IMPORTANT]
> 
> <span data-ttu-id="e6d3f-104">此内容尚未完成。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-104">This content is not finished yet.</span></span> <span data-ttu-id="e6d3f-105">请稍后再回来查看。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-105">Check back shortly.</span></span>

## <a name="sdk-versioning"></a><span data-ttu-id="e6d3f-106">SDK 版本控制</span><span class="sxs-lookup"><span data-stu-id="e6d3f-106">SDK Versioning</span></span>

1. <span data-ttu-id="e6d3f-107">SDK 主要版本和次要版本**应该**与 `schema` 版本匹配。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-107">The SDK major and minor version **SHOULD** match the `schema` version.</span></span> 
1. <span data-ttu-id="e6d3f-108">修补程序/内部版本**应该**用于没有架构更改的呈现器更新。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-108">Patch/build **SHOULD** be used for renderer updates that don't have schema changes.</span></span>

## <a name="parsing-json"></a><span data-ttu-id="e6d3f-109">分析 JSON</span><span class="sxs-lookup"><span data-stu-id="e6d3f-109">Parsing JSON</span></span>

### <a name="error-conditions"></a><span data-ttu-id="e6d3f-110">错误条件</span><span class="sxs-lookup"><span data-stu-id="e6d3f-110">Error conditions</span></span>
1. <span data-ttu-id="e6d3f-111">分析器**必须**确保它是有效的 JSON 内容</span><span class="sxs-lookup"><span data-stu-id="e6d3f-111">A parser **MUST** check that it's valid JSON content</span></span>
1. <span data-ttu-id="e6d3f-112">分析器**必须**按照架构要求（必需属性等）进行验证</span><span class="sxs-lookup"><span data-stu-id="e6d3f-112">A parser **MUST** validate against the schema (required properties, etc)</span></span>
1. <span data-ttu-id="e6d3f-113">**必须**向主机应用报告上述错误（异常或类似的内容）</span><span class="sxs-lookup"><span data-stu-id="e6d3f-113">The above errors **MUST** be reported to the host app (exception or equivalent)</span></span>

### <a name="unknown-types"></a><span data-ttu-id="e6d3f-114">未知类型</span><span class="sxs-lookup"><span data-stu-id="e6d3f-114">Unknown types</span></span>
1. <span data-ttu-id="e6d3f-115">如果遇到未知“类型”，**必须将其从结果中删除**</span><span class="sxs-lookup"><span data-stu-id="e6d3f-115">If unknown "types" are encountered they **MUST BE DROPPED** from the result</span></span>
1. <span data-ttu-id="e6d3f-116">对有效负载进行更改（如上所示）时，**应该**将其以警告形式报告给主机应用</span><span class="sxs-lookup"><span data-stu-id="e6d3f-116">Any alterations of the payload (like above) **SHOULD** be reported as warnings to the host app</span></span>

### <a name="unknown-properties"></a><span data-ttu-id="e6d3f-117">未知属性</span><span class="sxs-lookup"><span data-stu-id="e6d3f-117">Unknown properties</span></span>
1. <span data-ttu-id="e6d3f-118">分析器**必须**包含元素的**其他**属性</span><span class="sxs-lookup"><span data-stu-id="e6d3f-118">A parser **MUST** include **additional** properties on elements</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="e6d3f-119">其他注意事项</span><span class="sxs-lookup"><span data-stu-id="e6d3f-119">Additional considerations</span></span>
1. <span data-ttu-id="e6d3f-120">`speak` 属性可能包含 SSML 标记，**必须**按指定要求返回到主机应用</span><span class="sxs-lookup"><span data-stu-id="e6d3f-120">The `speak` property may contain SSML markup and **MUST** be returned to the host app as-specified</span></span>

## <a name="parsing-host-config"></a><span data-ttu-id="e6d3f-121">分析主机配置</span><span class="sxs-lookup"><span data-stu-id="e6d3f-121">Parsing Host Config</span></span>
1. <span data-ttu-id="e6d3f-122">TODO</span><span class="sxs-lookup"><span data-stu-id="e6d3f-122">TODO</span></span>

## <a name="versioning"></a><span data-ttu-id="e6d3f-123">版本控制</span><span class="sxs-lookup"><span data-stu-id="e6d3f-123">Versioning</span></span>

1. <span data-ttu-id="e6d3f-124">呈现器**必须**实施特定版本的架构。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-124">A renderer **MUST** implement a particular version of the schema.</span></span> 
1. <span data-ttu-id="e6d3f-125">`AdaptiveCard` 构造函数**必须**根据当前架构版本为 `version` 属性提供默认值。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-125">The `AdaptiveCard` constructor **MUST** give the `version` property a default value based on the current schema version</span></span> 
1. <span data-ttu-id="e6d3f-126">如果呈现器在 `AdaptiveCard` 中遇到的 `version` 属性高于支持的版本，则**必须**改为返回 `fallbackText`。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-126">If a renderer encounters a `version` property in the `AdaptiveCard` that is higher than the supported version, it **MUST** return the `fallbackText` instead.</span></span>

## <a name="rendering"></a><span data-ttu-id="e6d3f-127">渲染</span><span class="sxs-lookup"><span data-stu-id="e6d3f-127">Rendering</span></span>

<span data-ttu-id="e6d3f-128">`AdaptiveCard` 包含 `body` 和 `actions`。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-128">An `AdaptiveCard` consists of a `body` and `actions`.</span></span> <span data-ttu-id="e6d3f-129">`body` 是可供呈现器按顺序枚举和呈现的 `CardElement` 的集合。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-129">The `body` is a collection of `CardElement`s that a renderer will enumerate and render in order.</span></span> 

1. <span data-ttu-id="e6d3f-130">每个元素**必须**按父元素的宽度进行拉伸（类似于 HTML 中的 `display: block`）。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-130">Each Element **MUST** stretch to the width of its parent (think `display: block` in HTML).</span></span>
1. <span data-ttu-id="e6d3f-131">呈现器**必须**忽略未知元素类型，继续呈现余下的有效负载。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-131">A renderer **MUST** ignore unknown element types, and continue rendering the rest of the payload.</span></span>

### <a name="spacing-and-separators"></a><span data-ttu-id="e6d3f-132">间距和分隔符</span><span class="sxs-lookup"><span data-stu-id="e6d3f-132">Spacing and Separators</span></span>

1. <span data-ttu-id="e6d3f-133">每个元素的 `spacing` 属性影响**当前**元素和它**前面**的元素之间的空间量。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-133">The `spacing` property on every element influences the amount of space between the **CURRENT** element and the one **BEFORE** it.</span></span>
1. <span data-ttu-id="e6d3f-134">应用间距的**前提**是它前面确实有一个元素。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-134">Spacing **MUST ONLY** apply when there actually is an element preceding it.</span></span> <span data-ttu-id="e6d3f-135">（例如，间距不会应用到数组中的第一个项）</span><span class="sxs-lookup"><span data-stu-id="e6d3f-135">(E.g., won't apply to the first item in an array)</span></span>
1. <span data-ttu-id="e6d3f-136">呈现器**必须**从 `hostConfig` 间距查找要使用的空间量，以便将枚举值应用到当前元素。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-136">A renderer **MUST** look up the amount of space to use from the `hostConfig` spacing for the enum value applied to the current element.</span></span>
1. <span data-ttu-id="e6d3f-137">如果元素的 `separator` 值为 `true`，则**必须**在当前元素和它前面的元素之间绘制一条可见的线。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-137">If the element has a `separator` value of `true`, then a visible line **MUST** be drawn between the current element and the one before it.</span></span>
1. <span data-ttu-id="e6d3f-138">**必须**使用 `container.style.default.foregroundColor` 绘制此分隔线。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-138">The separator line **MUST** be drawn using the `container.style.default.foregroundColor`.</span></span>
1. <span data-ttu-id="e6d3f-139">绘制分隔符的**前提**是该项**不是**数组中的首项。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-139">A separator **MUST ONLY** be drawn if the item **IS NOT** the first in the array.</span></span>

### <a name="columns"></a><span data-ttu-id="e6d3f-140">列</span><span class="sxs-lookup"><span data-stu-id="e6d3f-140">Columns</span></span>

1. <span data-ttu-id="e6d3f-141">`Column` `width` **必须**通过“auto”、“stretch”或加权比率进行解释。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-141">`Column` `width` **MUST** be interpreted by "auto", "stretch" or a weighted ratio.</span></span>

### <a name="textblock"></a><span data-ttu-id="e6d3f-142">TextBlock</span><span class="sxs-lookup"><span data-stu-id="e6d3f-142">TextBlock</span></span>

1. <span data-ttu-id="e6d3f-143">TextBlock **必须**占用一行，除非 `wrap` 属性为 `true`。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-143">A TextBlock **MUST** take up a single line unless the `wrap` property is `true`.</span></span> 
1. <span data-ttu-id="e6d3f-144">文本块**应该**使用省略号 (...) 裁剪多余的文本</span><span class="sxs-lookup"><span data-stu-id="e6d3f-144">The text block **SHOULD** trim any excess text with an ellipsis (...)</span></span>

#### <a name="markdown"></a><span data-ttu-id="e6d3f-145">Markdown</span><span class="sxs-lookup"><span data-stu-id="e6d3f-145">Markdown</span></span>

1. <span data-ttu-id="e6d3f-146">自适应卡片允许 Markdown 的子集，**应该**在 `TextBlock` 中受到支持。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-146">Adaptive Cards allow for a subset of Markdown and **SHOULD** be supported in `TextBlock`.</span></span> 
1. <span data-ttu-id="e6d3f-147">请参阅完整的 [Markdown 要求](../authoring-cards/text-features.md)</span><span class="sxs-lookup"><span data-stu-id="e6d3f-147">See full [markdown requirements](../authoring-cards/text-features.md)</span></span>

#### <a name="formatting-functions"></a><span data-ttu-id="e6d3f-148">格式设置函数</span><span class="sxs-lookup"><span data-stu-id="e6d3f-148">Formatting functions</span></span>

1. <span data-ttu-id="e6d3f-149">`TextBlock` 允许 [DATE/TIME 格式设置函数](../authoring-cards/text-features.md)，这些函数**必须**在每个呈现器上都受到支持。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-149">`TextBlock` allows [DATE/TIME formatting functions](../authoring-cards/text-features.md) that **MUST** be supported on every renderer.</span></span>
1. <span data-ttu-id="e6d3f-150">**所有故障必须**在卡片中显示原始字符串。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-150">**ALL FAILURES MUST** display the raw string in the card.</span></span> <span data-ttu-id="e6d3f-151">未尝试友好消息。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-151">No friendly message attempted.</span></span> <span data-ttu-id="e6d3f-152">（目的是让开发人员立即意识到存在问题）</span><span class="sxs-lookup"><span data-stu-id="e6d3f-152">(The goal being to make the developer immediately aware there is a problem)</span></span>

1. <span data-ttu-id="e6d3f-153">TODO：包括 regex</span><span class="sxs-lookup"><span data-stu-id="e6d3f-153">TODO: Include regex</span></span>

### <a name="images"></a><span data-ttu-id="e6d3f-154">映像</span><span class="sxs-lookup"><span data-stu-id="e6d3f-154">Images</span></span>

1. <span data-ttu-id="e6d3f-155">呈现器**应该**让主机应用知道在什么时候所有 HTTP 图像已完成下载且卡片已“完全呈现”</span><span class="sxs-lookup"><span data-stu-id="e6d3f-155">A renderer **SHOULD** allow host apps to know when all HTTP images have been downloaded and the card is "fully rendered"</span></span>
1. <span data-ttu-id="e6d3f-156">呈现器**必须**在下载 HTTP 图像时检查主机配置的 `maxImageSize` 参数</span><span class="sxs-lookup"><span data-stu-id="e6d3f-156">A renderer **MUST** inspect the Host Config `maxImageSize` param when downloading HTTP images</span></span>
1. <span data-ttu-id="e6d3f-157">呈现器**必须**支持 `.png` 和 `.jpeg`</span><span class="sxs-lookup"><span data-stu-id="e6d3f-157">A renderer **MUST** support `.png` and `.jpeg`</span></span>
1. <span data-ttu-id="e6d3f-158">呈现器**应该**支持 `.gif` 图像</span><span class="sxs-lookup"><span data-stu-id="e6d3f-158">A renderer **SHOULD** support `.gif` images</span></span>

### <a name="host-config"></a><span data-ttu-id="e6d3f-159">主机配置</span><span class="sxs-lookup"><span data-stu-id="e6d3f-159">Host Config</span></span>

* <span data-ttu-id="e6d3f-160">TODO：默认值应该是什么？</span><span class="sxs-lookup"><span data-stu-id="e6d3f-160">TODO: What should the defaults be?</span></span> <span data-ttu-id="e6d3f-161">它们是否都应该共享它？</span><span class="sxs-lookup"><span data-stu-id="e6d3f-161">Should they all share it?</span></span> <span data-ttu-id="e6d3f-162">我们是否应该在二进制文件中嵌入通用的 hostConfig.json 文件？</span><span class="sxs-lookup"><span data-stu-id="e6d3f-162">Should we embed a common hostConfig.json file in the binaries?</span></span>
* <span data-ttu-id="e6d3f-163">TODO：我认为也需要对 HostConfig 进行版本控制，以便进行分析，对不对？</span><span class="sxs-lookup"><span data-stu-id="e6d3f-163">TODO: I think HostConfig needs to be versioned as well for parsing?</span></span>

<span data-ttu-id="e6d3f-164">[`HostConfig`](host-config.md) 是一个共享配置对象，用于指定自适应卡片呈现器生成 UI 的方式。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-164">[`HostConfig`](host-config.md) is a shared configuration object that specifies how an Adaptive Card Renderer generates UI.</span></span>  

<span data-ttu-id="e6d3f-165">这样，那些跨平台的属性就可以在不同平台和设备的呈现器中共享。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-165">This allows properties which are platform agnostic to be shared among renderers on different platforms and devices.</span></span> <span data-ttu-id="e6d3f-166">另外还可以创建工具，让你了解该卡片在给定环境下的外观。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-166">It also allows tooling to be created which gives you an idea of the look and feel that card would have for a given environment.</span></span>

1. <span data-ttu-id="e6d3f-167">呈现器**必须**向主机应用公开 **Host Config** 参数</span><span class="sxs-lookup"><span data-stu-id="e6d3f-167">Renderers **MUST** expose a **Host Config** parameter to host apps</span></span>
1. <span data-ttu-id="e6d3f-168">所有元素都**必须**根据相应的 Host Config 设置进行样式设置</span><span class="sxs-lookup"><span data-stu-id="e6d3f-168">All elements **MUST** be styled according to their respective Host Config settings</span></span>

### <a name="native-platform-styling"></a><span data-ttu-id="e6d3f-169">本机平台样式设置</span><span class="sxs-lookup"><span data-stu-id="e6d3f-169">Native platform styling</span></span>

1. <span data-ttu-id="e6d3f-170">每个元素类型**应该**为生成的 UI 元素附加一个本机平台样式。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-170">Each element type **SHOULD** attach a native platform style with the generated UI element.</span></span> <span data-ttu-id="e6d3f-171">例如，在 HTML 中，我们为元素类型添加了一个 CSS 类，而在 XAML 中，我们会分配特定的样式。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-171">E.g., in HTML we added a CSS class to the element types, and in XAML we assign a specific Style.</span></span>

## <a name="extensibility"></a><span data-ttu-id="e6d3f-172">扩展性</span><span class="sxs-lookup"><span data-stu-id="e6d3f-172">Extensibility</span></span> 

1. <span data-ttu-id="e6d3f-173">呈现器**必须**允许主机应用重写默认的元素呈现器。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-173">A renderer **MUST** allow host apps to override default element renderers.</span></span> <span data-ttu-id="e6d3f-174">例如，将 `TextBlock` 呈现替换为自己的逻辑。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-174">E.g., replace `TextBlock` rendering with their own logic.</span></span>
1. <span data-ttu-id="e6d3f-175">呈现器**必须**允许主机应用注册自定义元素类型。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-175">A renderer **MUST** allow host apps to register custom element types.</span></span> <span data-ttu-id="e6d3f-176">例如，添加对自定义 `Rating` 元素的支持</span><span class="sxs-lookup"><span data-stu-id="e6d3f-176">E.g., add support for a custom `Rating` element</span></span>
1. <span data-ttu-id="e6d3f-177">呈现器**必须**允许主机应用删除对默认元素的支持。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-177">A renderer **MUST** allow host apps to remove support for a default element.</span></span> <span data-ttu-id="e6d3f-178">例如，如果主机应用不希望支持 `Action.Submit`，则可将其删除。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-178">E.g., remove `Action.Submit` if they don't want it supported.</span></span>

## <a name="actions"></a><span data-ttu-id="e6d3f-179">“操作”</span><span class="sxs-lookup"><span data-stu-id="e6d3f-179">Actions</span></span>

1. <span data-ttu-id="e6d3f-180">如果 HostConfig `supportsInteractivity` 为 `false`，则呈现器**不得**呈现任何操作。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-180">If HostConfig `supportsInteractivity` is `false`, a renderer **MUST NOT** render any actions.</span></span>
1. <span data-ttu-id="e6d3f-181">`actions` 属性在某些类型的操作栏中**必须**呈现为按钮，这些按钮通常位于卡片底部。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-181">The `actions` property **MUST** be rendered as buttons in some kind of action bar, usually at the bottom of the card.</span></span> 
1. <span data-ttu-id="e6d3f-182">当按钮受到点击时，**必须**允许主机应用处理该事件。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-182">When a button is tapped it **MUST** allow the host app to handle the event.</span></span> 
1. <span data-ttu-id="e6d3f-183">该事件**必须**将所有相关联的属性与操作一起传递。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-183">The event **MUST** pass along all associated properties with the action</span></span>
1. <span data-ttu-id="e6d3f-184">该事件**必须**传递已执行的 `AdaptiveCard`。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-184">The event **MUST** pass along the `AdaptiveCard` which was executed</span></span>

<span data-ttu-id="e6d3f-185">操作</span><span class="sxs-lookup"><span data-stu-id="e6d3f-185">Action</span></span> | <span data-ttu-id="e6d3f-186">行为</span><span class="sxs-lookup"><span data-stu-id="e6d3f-186">Behavior</span></span>
--- | ---
<span data-ttu-id="e6d3f-187">**Action.OpenUrl**</span><span class="sxs-lookup"><span data-stu-id="e6d3f-187">**Action.OpenUrl**</span></span> | <span data-ttu-id="e6d3f-188">打开要查看的外部 URL</span><span class="sxs-lookup"><span data-stu-id="e6d3f-188">Open an external URL for viewing</span></span>
<span data-ttu-id="e6d3f-189">**Action.ShowCard**</span><span class="sxs-lookup"><span data-stu-id="e6d3f-189">**Action.ShowCard**</span></span> | <span data-ttu-id="e6d3f-190">请求一张显示给用户的子卡。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-190">Requests a sub-card to be shown to the user.</span></span>
<span data-ttu-id="e6d3f-191">**Action.Submit**</span><span class="sxs-lookup"><span data-stu-id="e6d3f-191">**Action.Submit**</span></span> | <span data-ttu-id="e6d3f-192">要求将所有输入元素收集到一个对象中，然后通过主机应用程序定义的某个方法将该对象发送给你。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-192">Ask for all of the input elements to be gathered up into an object which is then sent to you through some method defined by the host application.</span></span>

### <a name="actionopenurl"></a><span data-ttu-id="e6d3f-193">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="e6d3f-193">Action.OpenUrl</span></span>
1. <span data-ttu-id="e6d3f-194">`Action.OpenUrl` **应该**使用本机平台机制打开一个 URL</span><span class="sxs-lookup"><span data-stu-id="e6d3f-194">`Action.OpenUrl` **SHOULD** open a URL using the native platform mechanism</span></span>
1. <span data-ttu-id="e6d3f-195">如果无法执行该操作，则**必须**引发一个事件，要求主机应用负责打开该 URL。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-195">If this is not possible it **MUST** raise an event to the host app to handle opening the URL.</span></span> <span data-ttu-id="e6d3f-196">此事件**必须**允许主机应用重写默认行为。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-196">This event **MUST** allow the host app to override the default behavior.</span></span> <span data-ttu-id="e6d3f-197">例如，让它们在自己的应用中打开 URL。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-197">E.g., let them open the URL within their own app.</span></span>

### <a name="actionshowcard"></a><span data-ttu-id="e6d3f-198">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="e6d3f-198">Action.ShowCard</span></span>

1. <span data-ttu-id="e6d3f-199">`Action.ShowCard` **必须**获得某种方式的支持，具体取决于 hostConfig 设置。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-199">`Action.ShowCard` **MUST** be supported in some way, based on the hostConfig setting.</span></span> <span data-ttu-id="e6d3f-200">有两种模式：内联和弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-200">There are two modes: inline, and popup.</span></span> <span data-ttu-id="e6d3f-201">内联卡片**应该**自动切换卡片可见性。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-201">Inline cards **SHOULD** toggle the card visibility automatically.</span></span> <span data-ttu-id="e6d3f-202">在弹出窗口模式中，**应该**触发一个事件，要求主机应用以某种方式显示卡片。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-202">In popup mode, an event **SHOULD** be fired to the host app to show the card in some way.</span></span>

### <a name="actionsubmit"></a><span data-ttu-id="e6d3f-203">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="e6d3f-203">Action.Submit</span></span>

<span data-ttu-id="e6d3f-204">提交操作的行为类似于 HTML 窗体提交，只是 HTML 通常触发一个 HTTP Post，而自适应卡片则让每个主机应用自行决定如何“提交”。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-204">The Submit Action behaves like an HTML form submit, except that where HTML typically triggers an HTTP post, Adaptive Cards leaves it up to each host app to determine what "submit" means to them.</span></span> 

1. <span data-ttu-id="e6d3f-205">当此项**必须**引发一个事件时，用户需点击所调用的操作。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-205">When this **MUST** raise an event the user taps the action invoked.</span></span>  
1. <span data-ttu-id="e6d3f-206">`data` 属性**必须**包括在回调有效负载中。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-206">The `data` property **MUST** be included in the callback payload.</span></span>
1. <span data-ttu-id="e6d3f-207">对于 `Action.Submit`，呈现器**必须**收集卡片上的所有输入并检索其值。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-207">For `Action.Submit`, a renderer **MUST** gather all inputs on the card and retrieve their values.</span></span> 

### <a name="selectaction"></a><span data-ttu-id="e6d3f-208">selectAction</span><span class="sxs-lookup"><span data-stu-id="e6d3f-208">selectAction</span></span>

1. <span data-ttu-id="e6d3f-209">如果 HostConfig `supportedInteractivity` 为 `false`，则 `selectAction` **不得**呈现为触控目标。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-209">If Host Config `supportedInteractivity` is `false` then a `selectAction` **MUST NOT** render as a touch target.</span></span>
1. <span data-ttu-id="e6d3f-210">`Image`、`ColumnSet` 和 `Column` 提供一个 `selectAction` 属性，当用户以某种方式（例如，点击该元素）调用该属性时，系统**应该**执行它。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-210">`Image`, `ColumnSet`, and `Column` offer a `selectAction` property, which **SHOULD** be executed when the user invokes it, e.g., by tapping the element.</span></span>

## <a name="inputs"></a><span data-ttu-id="e6d3f-211">输入</span><span class="sxs-lookup"><span data-stu-id="e6d3f-211">Inputs</span></span>

1. <span data-ttu-id="e6d3f-212">如果 HostConfig `supportsInteractivity` 为 `false`，则呈现器**不得**呈现任何输入。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-212">If HostConfig `supportsInteractivity` is `false` a renderer **MUST NOT** render any inputs.</span></span>
2. <span data-ttu-id="e6d3f-213">输入的呈现**应该**尽可能采用高保真的形式。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-213">Inputs **SHOULD** render with the highest fidelity possible.</span></span> <span data-ttu-id="e6d3f-214">例如，理想情况下，`Input.Date` 会为用户提供一个日期选取器，但如果不可能在 UI 堆栈上实现此功能，则呈现器**必须**退而求其次，呈现一个标准的文本框。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-214">For example, an `Input.Date` would ideally offer a date picker to a user, but if this isn't possible on your UI stack, then the renderer **MUST** fall back to rendering a standard text box.</span></span>
3. <span data-ttu-id="e6d3f-215">可能情况下，呈现器**应该**显示 `placeholderText`</span><span class="sxs-lookup"><span data-stu-id="e6d3f-215">A renderer **SHOULD** display the `placeholderText` if possible</span></span>
4. <span data-ttu-id="e6d3f-216">呈现器**不**需对输入实施验证。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-216">A renderer **DOES NOT** have to implement validation of the input.</span></span> <span data-ttu-id="e6d3f-217">自适应卡片用户必须做好计划，在自己那一端验证任何接收的数据。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-217">Users of Adaptive Cards must plan to validate any received data on their end.</span></span>
5. <span data-ttu-id="e6d3f-218">输入值绑定**必须**进行正确的转义</span><span class="sxs-lookup"><span data-stu-id="e6d3f-218">Input value binding **MUST** be properly escaped</span></span>

6. <span data-ttu-id="e6d3f-219">此对象**必须**返回到主机应用，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e6d3f-219">The object **MUST** be returned to the host app as follows:</span></span>

   <span data-ttu-id="e6d3f-220">对于在自适应卡片中进行的输入验证，我们不做任何承诺，因此，接收方应该对响应进行适当的分析。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-220">We do not make any promises of input validation in adaptive cards, so it's up to the receiving party to properly parse the response.</span></span> <span data-ttu-id="e6d3f-221">例如，Input.Number 可能返回“hello”，接收方需要做好相应的准备。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-221">E.g., a Input.Number could return "hello" and they need to be prepared for that.</span></span>


## <a name="events"></a><span data-ttu-id="e6d3f-222">事件</span><span class="sxs-lookup"><span data-stu-id="e6d3f-222">Events</span></span>

1. <span data-ttu-id="e6d3f-223">当某个元素的可见性变化时，呈现器**应该**触发一个事件，让主机应用将卡片滚动到相应位置。</span><span class="sxs-lookup"><span data-stu-id="e6d3f-223">A renderer **SHOULD** fire an event when an element's visibility has changed, allowing the host app to scroll the card into position.</span></span>
