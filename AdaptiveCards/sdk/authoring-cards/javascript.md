---
title: 适用于自适应卡的 JavaScript SDK
author: matthidinger
ms.author: mahiding
ms.date: 07/26/2019
ms.topic: article
ms.openlocfilehash: 4ddff841ec073c60a8aa6184f309e94052cb002d
ms.sourcegitcommit: 1e18c5dc0cf85d26f66335e312348bbfb903d95a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/19/2020
ms.locfileid: "77454800"
---
# <a name="javascript-sdk-for-creating-cards"></a><span data-ttu-id="a6d66-102">用于创建卡的 JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="a6d66-102">JavaScript SDK for creating cards</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a6d66-103">序列化 JSON 的库仍在开发中，你的 milage 可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="a6d66-103">The library for serializing JSON is still in development and your milage may vary.</span></span>

<span data-ttu-id="a6d66-104">如我们在[入门](../../authoring-cards/getting-started.md)中所述，自适应卡只是卡对象模型的序列化 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="a6d66-104">As we described in the [Getting Started](../../authoring-cards/getting-started.md), an Adaptive Card is nothing more than a serialized JSON object of a card object model.</span></span>  <span data-ttu-id="a6d66-105">为了使处理对象模型变得简单，我们定义了一些库，定义了一个易于序列化/反序列化 json 的强类型类层次结构。</span><span class="sxs-lookup"><span data-stu-id="a6d66-105">To make it easy to manipulate the object model we have defined some libraries which define a strongly typed class hierarchy that is easy to serialize/deserialize json.</span></span>

<span data-ttu-id="a6d66-106">您可以使用任何想要创建自适应卡 json 的工具。</span><span class="sxs-lookup"><span data-stu-id="a6d66-106">You can use any tooling that you want to create the adaptive card json.</span></span>

<span data-ttu-id="a6d66-107">`adaptivecards` npm 包定义用于在 javascript 中使用自适应卡的库</span><span class="sxs-lookup"><span data-stu-id="a6d66-107">The `adaptivecards` npm package defines a library for working with adaptive cards in javascript</span></span>

## <a name="to-install"></a><span data-ttu-id="a6d66-108">安装</span><span class="sxs-lookup"><span data-stu-id="a6d66-108">To install</span></span>
```console
npm install adaptivecards
```

## <a name="example"></a><span data-ttu-id="a6d66-109">示例</span><span class="sxs-lookup"><span data-stu-id="a6d66-109">Example</span></span>

<span data-ttu-id="a6d66-110">以下 API 演示了如何使用对象模型构造自适应卡并将其序列化为 JSON。</span><span class="sxs-lookup"><span data-stu-id="a6d66-110">The following API shows how to construct an Adaptive Card using the object model and serialize it to JSON.</span></span>

```typescript
let card = new Adaptive.AdaptiveCard();
card.version = new Adaptive.Version(1, 0);

let textBlock = new Adaptive.TextBlock();
textBlock.text = "Hello World";

card.addItem(textBlock);

let json = card.toJSON();
```
