---
title: Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: b5f1279317e6b34d2e3bccee2625d972ac185e04
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67134278"
---
# <a name="getting-started---android"></a><span data-ttu-id="2c7d9-102">入门 - Android</span><span class="sxs-lookup"><span data-stu-id="2c7d9-102">Getting started - Android</span></span>

<span data-ttu-id="2c7d9-103">这是以 Android 原生控件为目标的呈现器。</span><span class="sxs-lookup"><span data-stu-id="2c7d9-103">This is a renderer which targets Android native controls.</span></span>

## <a name="install-maven-package"></a><span data-ttu-id="2c7d9-104">安装 Maven 包</span><span class="sxs-lookup"><span data-stu-id="2c7d9-104">Install Maven package</span></span>

<span data-ttu-id="2c7d9-105">[![Maven Central](https://img.shields.io/maven-central/v/io.adaptivecards/adaptivecards-android.svg)](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22adaptivecards-android%22)</span><span class="sxs-lookup"><span data-stu-id="2c7d9-105">[![Maven Central](https://img.shields.io/maven-central/v/io.adaptivecards/adaptivecards-android.svg)](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22adaptivecards-android%22)</span></span>

<span data-ttu-id="2c7d9-106">可以在</span><span class="sxs-lookup"><span data-stu-id="2c7d9-106">You can find the published packages</span></span> ![此处](https://search.maven.org/search?q=g:io.adaptivecards)

<span data-ttu-id="2c7d9-108">若要将库包括到项目中，必须将以下行包括到项目 gradle.build 的 dependencies 节中</span><span class="sxs-lookup"><span data-stu-id="2c7d9-108">To include library to your project you must include this line into your project gradle.build under the dependencies section</span></span>

```build.gradle
 implementation 'io.adaptivecards:adaptivecards-android:1.1.0'
```
<span data-ttu-id="2c7d9-109">需要更改版本号，具体取决于需包括到项目中的版本</span><span class="sxs-lookup"><span data-stu-id="2c7d9-109">You need to change the version number depending on the version you want to include into your project</span></span>

## <a name="add-import"></a><span data-ttu-id="2c7d9-110">添加 import</span><span class="sxs-lookup"><span data-stu-id="2c7d9-110">Add import</span></span>

<span data-ttu-id="2c7d9-111">若要包括对象模型，请添加以下 import</span><span class="sxs-lookup"><span data-stu-id="2c7d9-111">To include the object model, add this import</span></span>

```
 import io.adaptivecards.objectmodel.*;
```

<span data-ttu-id="2c7d9-112">若要包括呈现器，请添加以下 import</span><span class="sxs-lookup"><span data-stu-id="2c7d9-112">To include the renderer, add this import</span></span>

```
 import io.adaptivecards.renderer.*;
```

## <a name="next-steps"></a><span data-ttu-id="2c7d9-113">后续步骤</span><span class="sxs-lookup"><span data-stu-id="2c7d9-113">Next steps</span></span>

<span data-ttu-id="2c7d9-114">请参阅[呈现卡片](render-a-card.md)，了解后续步骤！</span><span class="sxs-lookup"><span data-stu-id="2c7d9-114">See [Render a card](render-a-card.md) for the next steps!</span></span>
