---
title: 用于自适应卡 JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 6372f2f23a817ecc4d07d950d6513d14357547b7
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552659"
---
# <a name="javascript-sdk-for-creating-cards"></a>用于创建卡 JavaScript SDK

> [!IMPORTANT]
> 用于序列化 JSON 的库仍处于开发阶段，你 milage 可能发生改变。

如我们所述入门部分，自适应卡，则没有其他任何卡对象模型的序列化的 json 对象。  若要轻松地操作对象模型我们定义一些库定义很容易进行序列化/反序列化 json 的强类型化的类层次结构。

可以使用任何你想要创建的自适应卡 json 的工具。

`adaptivecards` Npm 包定义用于与自适应卡在 javascript 中使用的库

## <a name="to-install"></a>若要安装
```console
npm install adaptivecards
```

## <a name="example-creating"></a>创建示例 
有在接口定义`schema.d.ts`描述的架构

```typescript
let card = {
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "Container",
            "items": [
                {
                    "type": "TextBlock",
                    "text": "Meow!"
                },
                {
                    "type": "Image",
                    "url": "http://adaptivecards.io/content/cats/1.png"
                }
            ]
        }
    ]
};
```

此外没有用于创建卡的对象模型。


```typescript
let card :IAdaptiveCard =  new AdaptiveCard();
card.body.add(new TextBlock() 
{
    text = "hello world"
});
```
