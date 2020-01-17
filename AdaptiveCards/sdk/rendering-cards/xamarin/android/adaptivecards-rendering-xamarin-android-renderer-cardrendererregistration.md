---
title: CardRendererRegistration 类-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 4254c1c3c0f275434fae2a92e20679b6fa136b16
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76145981"
---
# <a name="cardrendererregistration"></a>CardRendererRegistration

```csharp
public class CardRendererRegistration : Java.Lang.Object
```

**命名空间**
```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.Renderer.Registration
```

### <a name="summary"></a>摘要

| 公共方法 | |
| --- | ---- |
| ```void``` | [```RegisterFeatureRegistration (FeatureRegistration featureRegistration)```](#registerfeatureregistration) |

## <a name="public-methods"></a>公共方法

--- 

### <a id="registerfeatureregistration"></a>RegisterFeatureRegistration
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public void RegisterFeatureRegistration (FeatureRegistration featureRegistration)
```

注册要使用的卡呈现器的[```FeatureRegistration```](adaptivecards-rendering-xamarin-android-objectmodel-featureregistration.md)对象。

| 参数 | |
| --- | --- |
| featureRegistration | [```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.FeatureRegistration```](adaptivecards-rendering-xamarin-android-objectmodel-featureregistration.md) |

#### <a name="sample"></a>示例

```csharp
FeatureRegistration featureRegistration = new FeatureRegistration();
featureRegistration.AddFeature("MyFeature", "1.2.0");
CardRendererRegistration.Instance.RegisterFeatureRegistration(featureRegistration);
```