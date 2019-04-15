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
# <a name="javascript-sdk-for-creating-cards"></a><span data-ttu-id="2604d-102">用于创建卡 JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="2604d-102">JavaScript SDK for creating cards</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2604d-103">用于序列化 JSON 的库仍处于开发阶段，你 milage 可能发生改变。</span><span class="sxs-lookup"><span data-stu-id="2604d-103">The library for serializing JSON is still in development and your milage may vary.</span></span>

<span data-ttu-id="2604d-104">如我们所述入门部分，自适应卡，则没有其他任何卡对象模型的序列化的 json 对象。</span><span class="sxs-lookup"><span data-stu-id="2604d-104">As we described in the getting started section, an adaptive card is nothing more then a serialized json object of a card object model.</span></span>  <span data-ttu-id="2604d-105">若要轻松地操作对象模型我们定义一些库定义很容易进行序列化/反序列化 json 的强类型化的类层次结构。</span><span class="sxs-lookup"><span data-stu-id="2604d-105">To make it easy to manipulate the object model we have defined some libraries which define a strongly typed class hierarchy that is easy to serialize/deserialize json.</span></span>

<span data-ttu-id="2604d-106">可以使用任何你想要创建的自适应卡 json 的工具。</span><span class="sxs-lookup"><span data-stu-id="2604d-106">You can use any tooling that you want to create the adaptive card json.</span></span>

<span data-ttu-id="2604d-107">`adaptivecards` Npm 包定义用于与自适应卡在 javascript 中使用的库</span><span class="sxs-lookup"><span data-stu-id="2604d-107">The `adaptivecards` npm package defines a library for working with adaptive cards in javascript</span></span>

## <a name="to-install"></a><span data-ttu-id="2604d-108">若要安装</span><span class="sxs-lookup"><span data-stu-id="2604d-108">To install</span></span>
```console
npm install adaptivecards
```

## <a name="example-creating"></a><span data-ttu-id="2604d-109">创建示例</span><span class="sxs-lookup"><span data-stu-id="2604d-109">Example creating</span></span> 
<span data-ttu-id="2604d-110">有在接口定义`schema.d.ts`描述的架构</span><span class="sxs-lookup"><span data-stu-id="2604d-110">There are interface definitions in `schema.d.ts` which describe the shape of the schema</span></span>

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

<span data-ttu-id="2604d-111">此外没有用于创建卡的对象模型。</span><span class="sxs-lookup"><span data-stu-id="2604d-111">There is also an object model for creating cards.</span></span>


```typescript
let card :IAdaptiveCard =  new AdaptiveCard();
card.body.add(new TextBlock() 
{
    text = "hello world"
});
```
