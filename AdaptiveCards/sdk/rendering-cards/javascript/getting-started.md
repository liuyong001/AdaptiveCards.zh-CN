---
title: JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 9684b96bba5168a1f07549468274ce5d74c01820
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553459"
---
# <a name="getting-started---javascript"></a>获取已开始-JavaScript

如我们所述[Getting Started](../../../authoring-cards/getting-started.md)页上，自适应卡是一个 JSON 序列化卡对象模型。 这是用于在浏览器中生成客户端的 HTML 的 JavaScript SDK。

> [!IMPORTANT]
> **从 v0.5 的重大更改**
> 
> 1. 从包重命名`microsoft-adaptivecards`到 `adaptivecards`
> 1. 静态`AdaptiveCards.setHostConfig()`已被移动到的实例成员`AdaptiveCard`。 例如， `myCard.hostConfig = {}` 
> 1. `HostConfig` 已进入，但各种重命名和移动。 请参阅[sample.json](https://github.com/Microsoft/AdaptiveCards/blob/master/samples/HostConfig/sample.json)主机配置的当前结构
> 1. 也已经 v0.5 预览版中，这是某些架构更改[此处所述](https://github.com/Microsoft/AdaptiveCards/pull/633)
> 1. 静态`renderCard()`函数已删除，因为它是冗余的类方法。 使用`adaptiveCard.render()`如下所述。 


## <a name="install"></a>安装

### <a name="node"></a>节点

[![npm 安装](https://img.shields.io/npm/v/adaptivecards.svg)](https://www.npmjs.com/package/adaptivecards)

```console
npm install adaptivecards --save
```

### <a name="cdn"></a>CDN

```html
<script src="https://unpkg.com/adaptivecards/dist/adaptivecards.js"></script>
```

## <a name="usage"></a>用法

### <a name="import-the-module"></a>导入模块

```js
// import the module
import * as AdaptiveCards from "adaptivecards";

// or require it
var AdaptiveCards = require("adaptivecards");

// or use the global variable if loaded from CDN
AdaptiveCards.renderCard(...);
```

## <a name="next-steps"></a>后续步骤

请参阅[呈现卡片](render-a-card.md)以了解后续步骤 ！
