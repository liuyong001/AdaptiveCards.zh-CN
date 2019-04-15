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
# <a name="render-a-card---ios"></a>呈现卡-iOS

下面介绍了如何呈现使用 iOS SDK 的卡。

## <a name="create-a-card-from-a-json-string"></a>从 JSON 字符串创建卡片

从 JSON 字符串生成 AdaptiveCard

```objective-c
ACOParseResult *cardParseResult = [ACOAdaptiveCards FromJson:jsonStr];
/// access for parse warnings and errors
NSArray<NSError *> errors = cardParseResult.parseErrors;
NSArray<ACRParseWarning *> warnings = cardPraseResult.parseWarnings;
```

## <a name="render-a-card"></a>呈现数据卡

Rederer 采用自适应卡和主机配置。HostConfig 可为零，而如果 nil，将使用默认值。

```objective-c
ACRRenderResult *renderResult;
renderResult = [ACRRenderer render:cardParseResult.card
                            config:nil
                   widthConstraint:300.0];
``` 

### <a name="example"></a>示例

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

### <a name="render-a-card-as-uiviewcontroller"></a>呈现为 UIViewController 的卡片

AdaptiveCard 呈现器还可以返回 UIViewController。

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

返回 UIView 使用自动布局。 宽度为 widthConstraint 设置的值的约束。 如果使用值 0，则它不会绑定。
未绑定高度，并返回它将具有高度的呈现的所有内容的总和时。 若要绑定的视图的维度，请使用 NSLayoutConstraint。 如果使用 ACRViewController 的精确尺寸 viewDidLayoutSubview 其超 viewcontroller 或其方法具有相同名称的上下文中访问。


### <a name="compact-style-inputchoiceset"></a>Compact 样式 Input.ChoiceSet

用户界面表示形式的 Input.ChoiceSet 具有 UINavigationController，并且需要向转换为允许用户选择的 UIView 目前 active UIViewController 呈现。

若要完成此操作，请执行 didFecthSecondaryView ACRActionDelegate。

```objective-c
- (void)didFetchSecondaryView:(ACOAdaptiveCard *)card navigationController:(UINavigationController *)navigationController{
    [self presentViewController:navigationController animated:YES completion:nil];
}  
```

如果赋不已挂钩，这样做。

```objective-c
adaptiveView.acrActionDelegate = self
```