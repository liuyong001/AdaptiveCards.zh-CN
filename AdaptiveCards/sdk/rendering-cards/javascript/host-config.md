---
title: 托管配置-JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 11/28/2017
ms.topic: article
ms.openlocfilehash: 1809a022481e4fb28d2db454cfe90e07d09279ff
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553599"
---
# <a name="host-config---javascript"></a>主机配置-JavaScript

```js
// Create an AdaptiveCard instance
var adaptiveCard = new AdaptiveCards.AdaptiveCard();

// Set its hostConfig property unless you want to use the default Host Config
// Host Config defines the style and behavior of a card
adaptiveCard.hostConfig = new AdaptiveCards.HostConfig({
    fontFamily: "Segoe UI, Helvetica Neue, sans-serif"
    // More host config options
});

// Render the card to an HTML element:
var renderedCard = adaptiveCard.render();
```

## <a name="customization"></a>自定义

有 3 种方式自定义的自适应卡呈现： 
1. 主机配置
2. CSS 样式
3. 自定义元素呈现

### <a name="hostconfig"></a>HostConfig 

一个[主机配置](../../../rendering-cards/host-config.md)是所有呈现器了解一个共享的配置对象。 这允许你定义常见样式 （例如，字体系列，字体大小，默认间距） 以及将被自动解释每个平台呈现器的行为 （例如，最大数量的操作）。 

目标是，每个平台呈现器生成的本机 UI 看起来非常类似，但对您来说最少的工作量。

```javascript
var renderOptions = {
    ...
    hostConfig: {
        // Define your host config object here
        // See the HostConfig docs for details
    }
};
```