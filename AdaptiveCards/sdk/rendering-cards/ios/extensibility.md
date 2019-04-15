---
title: 可扩展性-iOS SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: c3dcae7ef2347201b5f7ce02baf3204db7ee27d6
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59553559"
---
# <a name="extensibility---ios"></a><span data-ttu-id="12e50-102">可扩展性-iOS</span><span class="sxs-lookup"><span data-stu-id="12e50-102">Extensibility - iOS</span></span>

## <a name="changing-per-element-rendering"></a><span data-ttu-id="12e50-103">更改每个元素呈现</span><span class="sxs-lookup"><span data-stu-id="12e50-103">Changing per element rendering</span></span>

<span data-ttu-id="12e50-104">开发人员可以自定义查找范围 renderred AdaptiveCards 元素，如 TextBlock。</span><span class="sxs-lookup"><span data-stu-id="12e50-104">Developers can customize the look of renderred AdaptiveCards elements such as TextBlock.</span></span>
<span data-ttu-id="12e50-105">下面的示例演示如何一个可以更改 NumberInput 背景色。</span><span class="sxs-lookup"><span data-stu-id="12e50-105">Following example shows how one can change background color of NumberInput.</span></span>

```objective-c
ACRRegistration *registration = [ACRRegistration getInstance];
// register custom renderer with registration
// custom renderer must implement ACRIBaseCardElementRenderer protocol
// for more information, please refer to CustomInputNumberRenderer.mm
 [registration setBaseCardElementRenderer:[CustomInputNumberRenderer getInstance] cardElementType:ACRNumberInput];
 ...
/// CustiomInputNumberRenderer.mm
- (UIView *)render:(UIView<ACRIContentHoldingView> *)viewGroup
              rootViewController:(UIViewController *)vc
              inputs:(NSArray *)inputs
     baseCardElement:(ACOBaseCardElement *)acoElem
          hostConfig:(ACOHostConfig *)acoConfig
  {
      ACRInputNumberRenderer *defaultRenderer = [ACRInputNumberRenderer getInstance];
 
      UIView *input = [defaultRenderer render:viewGroup
                           rootViewController:vc
                                       inputs:inputs
                              baseCardElement:acoElem
                                   hostConfig:acoConfig];
      if(input)
      {   
          // customize background color of input
          [input setBackgroundColor: [UIColor colorWithRed:1.0
                                                     green:59.0/255.0
                                                      blue:48.0/255.0
                                                     alpha:1.0]];
      }
      return input;
  }
  ```

 ## <a name="additional-property"></a><span data-ttu-id="12e50-106">附加属性</span><span class="sxs-lookup"><span data-stu-id="12e50-106">Additional Property</span></span>

 <span data-ttu-id="12e50-107">开发人员还可以在其他属性作为 json 有效负载的一部分发送。</span><span class="sxs-lookup"><span data-stu-id="12e50-107">Developers can also send in additional properties as part of json payload.</span></span>
<span data-ttu-id="12e50-108">例如，除了"间距"和"id"的 BaseCardElement 的 json 有效负载，其中一个可以向其 json 有效负载添加 TextBlock 的角半径。</span><span class="sxs-lookup"><span data-stu-id="12e50-108">For example, in addition to "spacing" and "id" of json payload for BaseCardElement, one can add radius for corners of TextBlock to its json payload.</span></span>

 ```objective-c
 "type":"TextBlock",
 ...
 "radius":20,
 ...
 ```

 ```objective-c
         NSData *additionalProperty = [acoElem additionalProperty];
          if(additionalProperty) {
              NSDictionary *dictionary = [NSJSONSerialization JSONObjectWithData:additionalProperty options:NSJSONReadingMutableLeaves error:nil];
              radiusForMyTextBlock = dictionary[@"radius"];
          ...
```
 ## <a name="custom-parsing"></a><span data-ttu-id="12e50-109">自定义分析</span><span class="sxs-lookup"><span data-stu-id="12e50-109">Custom Parsing</span></span>

<span data-ttu-id="12e50-110">开发人员也可以具有自定义分析，并已添加到 adpative 卡如进度栏的新 UI 元素。</span><span class="sxs-lookup"><span data-stu-id="12e50-110">Developers can also have custom parsing and have new UI element added to adpative card such as progress bar.</span></span> <span data-ttu-id="12e50-111">请有关详细信息，检查 CustomProgressBarRenderer.mm。</span><span class="sxs-lookup"><span data-stu-id="12e50-111">Please check CustomProgressBarRenderer.mm for detail.</span></span>
<span data-ttu-id="12e50-112">自定义分析程序必须实现 ACOIBaseCardElementParser 协议。</span><span class="sxs-lookup"><span data-stu-id="12e50-112">Custom parser must implement ACOIBaseCardElementParser protocol.</span></span> <span data-ttu-id="12e50-113">deserializeToCustomElement 方法应分析给定外被当作 json 有效负载，并返回指向 UIView 对象，它将添加到 AdaptiveCard 呈现对象的指针。</span><span class="sxs-lookup"><span data-stu-id="12e50-113">deserializeToCustomElement method should parses given json payload given as NSData and return a pointer to UIView object that will be added to AdaptiveCard rendered object.</span></span>

```objective-c
      CustomProgressBarRenderer *progressBarRenderer = [[CustomProgressBarRenderer alloc] init];
      [registration setCustomElementParser:progressBarRenderer];
```objective-c