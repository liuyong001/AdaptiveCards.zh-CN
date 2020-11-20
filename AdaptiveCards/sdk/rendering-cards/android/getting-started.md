---
title: Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: 864bb96c5875365845f7b9a7955b8a5380f034d9
ms.sourcegitcommit: 65b792d73c264c943036343e05b75f2b0488e6e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2020
ms.locfileid: "95001784"
---
# <a name="getting-started---android"></a><span data-ttu-id="29cb0-102">入门 - Android</span><span class="sxs-lookup"><span data-stu-id="29cb0-102">Getting started - Android</span></span>

<span data-ttu-id="29cb0-103">这是以 Android 原生控件为目标的呈现器。</span><span class="sxs-lookup"><span data-stu-id="29cb0-103">This is a renderer which targets Android native controls.</span></span>

## <a name="install-maven-package"></a><span data-ttu-id="29cb0-104">安装 Maven 包</span><span class="sxs-lookup"><span data-stu-id="29cb0-104">Install Maven package</span></span>

<span data-ttu-id="29cb0-105">[![Maven 中部](https://img.shields.io/maven-central/v/io.adaptivecards/adaptivecards-android.svg)](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22adaptivecards-android%22)</span><span class="sxs-lookup"><span data-stu-id="29cb0-105">[![Maven Central](https://img.shields.io/maven-central/v/io.adaptivecards/adaptivecards-android.svg)](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22adaptivecards-android%22)</span></span>

<span data-ttu-id="29cb0-106">可在[此处](https://search.maven.org/artifact/io.adaptivecards/adaptivecards-android)找到已发布的包</span><span class="sxs-lookup"><span data-stu-id="29cb0-106">You can find the published packages [here](https://search.maven.org/artifact/io.adaptivecards/adaptivecards-android)</span></span>

<span data-ttu-id="29cb0-107">若要将库包括到项目中，必须将以下行包括到项目 gradle.build 的 dependencies 节中</span><span class="sxs-lookup"><span data-stu-id="29cb0-107">To include library to your project you must include this line into your project gradle.build under the dependencies section</span></span>

```build.gradle
 implementation 'io.adaptivecards:adaptivecards-android:1.1.0'
```
<span data-ttu-id="29cb0-108">需要更改版本号，具体取决于需包括到项目中的版本</span><span class="sxs-lookup"><span data-stu-id="29cb0-108">You need to change the version number depending on the version you want to include into your project</span></span>

## <a name="add-import"></a><span data-ttu-id="29cb0-109">添加导入</span><span class="sxs-lookup"><span data-stu-id="29cb0-109">Add import</span></span>

<span data-ttu-id="29cb0-110">若要包括对象模型，请添加以下 import</span><span class="sxs-lookup"><span data-stu-id="29cb0-110">To include the object model, add this import</span></span>

```
 import io.adaptivecards.objectmodel.*;
```

<span data-ttu-id="29cb0-111">若要包括呈现器，请添加以下 import</span><span class="sxs-lookup"><span data-stu-id="29cb0-111">To include the renderer, add this import</span></span>

```
 import io.adaptivecards.renderer.*;
```

## <a name="next-steps"></a><span data-ttu-id="29cb0-112">后续步骤</span><span class="sxs-lookup"><span data-stu-id="29cb0-112">Next steps</span></span>

<span data-ttu-id="29cb0-113">请参阅[呈现卡片](render-a-card.md)，了解后续步骤！</span><span class="sxs-lookup"><span data-stu-id="29cb0-113">See [Render a card](render-a-card.md) for the next steps!</span></span>
