---
title: 扩展性-iOS SDK
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
# <a name="extensibility---ios"></a><span data-ttu-id="812ee-102">扩展性-iOS</span><span class="sxs-lookup"><span data-stu-id="812ee-102">Extensibility - iOS</span></span>

## <a name="changing-per-element-rendering"></a><span data-ttu-id="812ee-103">更改每个元素的呈现</span><span class="sxs-lookup"><span data-stu-id="812ee-103">Changing per element rendering</span></span>

<span data-ttu-id="812ee-104">开发人员可以自定义 renderred AdaptiveCards 元素的外观, 例如 TextBlock。</span><span class="sxs-lookup"><span data-stu-id="812ee-104">Developers can customize the look of renderred AdaptiveCards elements such as TextBlock.</span></span>
<span data-ttu-id="812ee-105">下面的示例演示如何更改 NumberInput 的背景色。</span><span class="sxs-lookup"><span data-stu-id="812ee-105">Following example shows how one can change background color of NumberInput.</span></span>

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

 ## <a name="additional-property"></a><span data-ttu-id="812ee-106">其他属性</span><span class="sxs-lookup"><span data-stu-id="812ee-106">Additional Property</span></span>

 <span data-ttu-id="812ee-107">开发人员还可以作为 json 有效负载的一部分发送其他属性。</span><span class="sxs-lookup"><span data-stu-id="812ee-107">Developers can also send in additional properties as part of json payload.</span></span>
<span data-ttu-id="812ee-108">例如, 除了 "BaseCardElement" 的 json 有效负载的 "间距" 和 "id" 外, 还可以将 TextBlock 的圆角的半径添加到其 json 有效负载中。</span><span class="sxs-lookup"><span data-stu-id="812ee-108">For example, in addition to "spacing" and "id" of json payload for BaseCardElement, one can add radius for corners of TextBlock to its json payload.</span></span>

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
 ## <a name="custom-parsing"></a><span data-ttu-id="812ee-109">自定义分析</span><span class="sxs-lookup"><span data-stu-id="812ee-109">Custom Parsing</span></span>

<span data-ttu-id="812ee-110">开发人员还可以自定义分析, 并将新的 UI 元素添加到 adpative 卡, 如进度栏。</span><span class="sxs-lookup"><span data-stu-id="812ee-110">Developers can also have custom parsing and have new UI element added to adpative card such as progress bar.</span></span> <span data-ttu-id="812ee-111">有关详细信息, 请查看 CustomProgressBarRenderer.mm。</span><span class="sxs-lookup"><span data-stu-id="812ee-111">Please check CustomProgressBarRenderer.mm for detail.</span></span>
<span data-ttu-id="812ee-112">自定义分析器必须实现 ACOIBaseCardElementParser 协议。</span><span class="sxs-lookup"><span data-stu-id="812ee-112">Custom parser must implement ACOIBaseCardElementParser protocol.</span></span> <span data-ttu-id="812ee-113">deserializeToCustomElement 方法应将给定的 json 负载分析为外, 并返回一个指向 UIView 对象的指针, 该对象将添加到 AdaptiveCard 呈现的对象。</span><span class="sxs-lookup"><span data-stu-id="812ee-113">deserializeToCustomElement method should parses given json payload given as NSData and return a pointer to UIView object that will be added to AdaptiveCard rendered object.</span></span>

```objective-c
      CustomProgressBarRenderer *progressBarRenderer = [[CustomProgressBarRenderer alloc] init];
      [registration setCustomElementParser:progressBarRenderer];
```objective-c