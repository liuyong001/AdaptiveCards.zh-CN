---
title: 本机样式设置 - Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: ebb033c68b9aedcaacb1989ffb1bec48707a9026
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67134241"
---
# <a name="native-styling---android"></a><span data-ttu-id="3db96-102">本机样式设置 - Android</span><span class="sxs-lookup"><span data-stu-id="3db96-102">Native styling - Android</span></span>

<span data-ttu-id="3db96-103">Android 呈现器不支持本机样式设置。v1.2 引入了对某些属性的样式设置的支持：</span><span class="sxs-lookup"><span data-stu-id="3db96-103">Native styling is not supported on the android renderer, v1.2 introduces the support for styling some properties:</span></span>

## <a name="action-sentiment"></a><span data-ttu-id="3db96-104">操作情绪</span><span class="sxs-lookup"><span data-stu-id="3db96-104">Action Sentiment</span></span>

<span data-ttu-id="3db96-105">操作情绪包括在 **v1.2** 中。虽然该版本不像其他版本那样支持许多样式，但可以对带有“破坏性”情绪或“正面”情绪的操作进行样式设置，只需实现一个有效的样式并将以下行添加到项目的 styles.xml 中即可</span><span class="sxs-lookup"><span data-stu-id="3db96-105">Action sentiment is included in **v1.2** and while not supporting as many styles as other versions, actions with *destructive* or *positive* sentiment can be styled by implementing a valid style and adding the following line into the styles.xml for your project</span></span>

```styles.xml
 <item name="adaptiveActionDestructive">@style/adaptiveActionDestructive</item>
 <item name="adaptiveActionPositive">@style/adaptiveActionPositive</item>
```

## <a name="inline-action"></a><span data-ttu-id="3db96-106">内联操作</span><span class="sxs-lookup"><span data-stu-id="3db96-106">Inline Action</span></span>

<span data-ttu-id="3db96-107">可以通过带内联操作的文本输入为要呈现的操作进行样式设置。</span><span class="sxs-lookup"><span data-stu-id="3db96-107">Text inputs with an inline action allows styling for the action being rendered.</span></span> <span data-ttu-id="3db96-108">这样可以将操作的样式设置为按钮 (adaptiveInlineAction) 或图像 (adaptiveInlineActionImage)</span><span class="sxs-lookup"><span data-stu-id="3db96-108">This allows styling the action as a button (adaptiveInlineAction) or as an image (adaptiveInlineActionImage)</span></span>

```styles.xml
 <item name="adaptiveInlineAction">@style/adaptiveInlineAction</item>
 <item name="adaptiveInlineActionImage">@style/adaptiveInlineActionImage</item>
```

> [!IMPORTANT]
> <span data-ttu-id="3db96-109">必须保留所有项目名称，如此处所示，因为呈现器会查找这些具体的名称</span><span class="sxs-lookup"><span data-stu-id="3db96-109">All item names must be kept as shown here as the renderer looks for those exact names</span></span>
