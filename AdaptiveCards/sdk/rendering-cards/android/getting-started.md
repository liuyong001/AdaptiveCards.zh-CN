---
title: Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: d15e0963427babe045a4db6f93800e09e0d95da9
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145497"
---
# <a name="getting-started---android"></a>入门 - Android

这是以 Android 原生控件为目标的呈现器。

## <a name="install-maven-package"></a>安装 Maven 包

[![Maven Central](https://img.shields.io/maven-central/v/io.adaptivecards/adaptivecards-android.svg)](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22adaptivecards-android%22)

可以在 ![此处](https://search.maven.org/search?q=g:io.adaptivecards)

若要将库包括到项目中，必须将以下行包括到项目 gradle.build 的 dependencies 节中

```build.gradle
 implementation 'io.adaptivecards:adaptivecards-android:1.1.0'
```
需要更改版本号，具体取决于需包括到项目中的版本

## <a name="add-import"></a>添加 import

若要包括对象模型，请添加以下 import

```
 import io.adaptivecards.objectmodel.*;
```

若要包括呈现器，请添加以下 import

```
 import io.adaptivecards.renderer.*;
```

## <a name="next-steps"></a>后续步骤

请参阅[呈现卡片](render-a-card.md)，了解后续步骤！
