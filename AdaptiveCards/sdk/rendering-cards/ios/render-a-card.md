---
title: 呈现卡片的 iOS SDK
author: matthidinger
ms.author: mahiding
ms.date: 06/26/2017
ms.topic: article
ms.openlocfilehash: 625701e38389cc1a54682b72ce2315c14180e576
ms.sourcegitcommit: 99c7b64d6fc66da336c454951406fb42cd2a7427
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/12/2019
ms.locfileid: "59552469"
---
# <a name="render-a-card---ios"></a><span data-ttu-id="a61fb-102">呈现卡-iOS</span><span class="sxs-lookup"><span data-stu-id="a61fb-102">Render a card - iOS</span></span>

<span data-ttu-id="a61fb-103">下面介绍了如何呈现使用 iOS SDK 的卡。</span><span class="sxs-lookup"><span data-stu-id="a61fb-103">Here's how to render a card using the iOS SDK.</span></span>

## <a name="create-a-card-from-a-json-string"></a><span data-ttu-id="a61fb-104">从 JSON 字符串创建卡片</span><span class="sxs-lookup"><span data-stu-id="a61fb-104">Create a card from a JSON string</span></span>

<span data-ttu-id="a61fb-105">从 JSON 字符串生成 AdaptiveCard</span><span class="sxs-lookup"><span data-stu-id="a61fb-105">AdaptiveCard is generated from JSON string</span></span>

```objective-c
ACOParseResult *cardParseResult = [ACOAdaptiveCards FromJson:jsonStr];
/// access for parse warnings and errors
NSArray<NSError *> errors = cardParseResult.parseErrors;
NSArray<ACRParseWarning *> warnings = cardPraseResult.parseWarnings;
```

## <a name="render-a-card"></a><span data-ttu-id="a61fb-106">呈现数据卡</span><span class="sxs-lookup"><span data-stu-id="a61fb-106">Render a Card</span></span>

<span data-ttu-id="a61fb-107">Rederer 采用自适应卡和主机配置。HostConfig 可为零，而如果 nil，将使用默认值。</span><span class="sxs-lookup"><span data-stu-id="a61fb-107">Rederer takes adaptive card and host config. HostConfig can be nil, and if nil, default value will be used.</span></span>

```objective-c
ACRRenderResult *renderResult;
renderResult = [ACRRenderer render:cardParseResult.card
                            config:nil
                   widthConstraint:300.0];
``` 

### <a name="example"></a><span data-ttu-id="a61fb-108">示例</span><span class="sxs-lookup"><span data-stu-id="a61fb-108">Example</span></span>

```objective-c
ACRRenderResult *renderResult;
ACOHostConfigParseResult *hostconfigParseResult = [ACOHostConfig FromJson:self.hostconfig];
ACOAdaptiveCardsParseResult *cardParseResult       = [ACOAdaptiveCards FromJson:jsonStr];

// checking parse result
if(hostconfigParseResult.IsValid == YES && cardParseResult.IsValid == YES)
{
    renderResult = [ACRRenderer render:cardParseResult.card
                                config:hostconfigParseResult.config
                       widthConstraint:300.0];
}   
    
if(renderResult.Suceeded == YES)
{
    // access returned UIView object
    ACRView *adaptiveView = renderResult.view;
    [self.view addSubview:adcVc.view];
}
```

### <a name="render-a-card-as-uiviewcontroller"></a><span data-ttu-id="a61fb-109">呈现为 UIViewController 的卡片</span><span class="sxs-lookup"><span data-stu-id="a61fb-109">Render a Card as UIViewController</span></span>

<span data-ttu-id="a61fb-110">AdaptiveCard 呈现器还可以返回 UIViewController。</span><span class="sxs-lookup"><span data-stu-id="a61fb-110">AdaptiveCard renderer can also return UIViewController.</span></span>

```objective-c
ACRRenderResult *renderResult = [ACRRenderer renderAsViewController:card config:config frame:frame delegate:acrActionDelegate];

renderResult.viewif(renderResult.Suceeded == YES)
{
    ACRViewController *adaptiveViewController = renderResult.viewcontroller;
    [self addChildViewController:adaptiveViewController];
    [self.view addSubview:adaptiveViewController.view];
    [adaptiveViewController didMoveToParentViewController:self];
    ...
}
```

<span data-ttu-id="a61fb-111">返回 UIView 使用自动布局。</span><span class="sxs-lookup"><span data-stu-id="a61fb-111">Returned UIView uses autolayout.</span></span> <span data-ttu-id="a61fb-112">宽度为 widthConstraint 设置的值的约束。</span><span class="sxs-lookup"><span data-stu-id="a61fb-112">Width will be constraint to the value set by widthConstraint.</span></span> <span data-ttu-id="a61fb-113">如果使用值 0，则它不会绑定。</span><span class="sxs-lookup"><span data-stu-id="a61fb-113">If 0 value is used, it won't be bound.</span></span>
<span data-ttu-id="a61fb-114">未绑定高度，并返回它将具有高度的呈现的所有内容的总和时。</span><span class="sxs-lookup"><span data-stu-id="a61fb-114">Height is not bound, and when returned it will have the height of sums of all contents rendered.</span></span> <span data-ttu-id="a61fb-115">若要绑定的视图的维度，请使用 NSLayoutConstraint。</span><span class="sxs-lookup"><span data-stu-id="a61fb-115">To bound the view dimension, please use NSLayoutConstraint.</span></span> <span data-ttu-id="a61fb-116">如果使用 ACRViewController 的精确尺寸 viewDidLayoutSubview 其超 viewcontroller 或其方法具有相同名称的上下文中访问。</span><span class="sxs-lookup"><span data-stu-id="a61fb-116">The exact dimension is accessible from the context of viewDidLayoutSubview of its superview's viewcontroller or its method with the same name if ACRViewController is used.</span></span>


### <a name="compact-style-inputchoiceset"></a><span data-ttu-id="a61fb-117">Compact 样式 Input.ChoiceSet</span><span class="sxs-lookup"><span data-stu-id="a61fb-117">Compact Style Input.ChoiceSet</span></span>

<span data-ttu-id="a61fb-118">用户界面表示形式的 Input.ChoiceSet 具有 UINavigationController，并且需要向转换为允许用户选择的 UIView 目前 active UIViewController 呈现。</span><span class="sxs-lookup"><span data-stu-id="a61fb-118">UI representation of Input.ChoiceSet has UINavigationController, and it needs to be presented to a presently active UIViewController to transition into UIView that allows user selection.</span></span>

<span data-ttu-id="a61fb-119">若要完成此操作，请执行 didFecthSecondaryView ACRActionDelegate。</span><span class="sxs-lookup"><span data-stu-id="a61fb-119">To accomplish that, please implement didFecthSecondaryView of ACRActionDelegate.</span></span>

```objective-c
- (void)didFetchSecondaryView:(ACOAdaptiveCard *)card navigationController:(UINavigationController *)navigationController{
    [self presentViewController:navigationController animated:YES completion:nil];
}  
```

<span data-ttu-id="a61fb-120">如果赋不已挂钩，这样做。</span><span class="sxs-lookup"><span data-stu-id="a61fb-120">If the delgate has not been hooked up, do so.</span></span>

```objective-c
adaptiveView.acrActionDelegate = self
```