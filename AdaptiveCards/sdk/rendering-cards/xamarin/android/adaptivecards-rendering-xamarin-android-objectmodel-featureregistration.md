---
title: FeatureRegistration 类-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: c1975197996e54626b464abe9181f0b02895ee4d
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76146141"
---
# <a name="feature-registration"></a>功能注册

```csharp
public class FeatureRegistration : Java.Lang.Object 
```

**命名空间**
```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.ObjectModel
```

## <a name="summary"></a>摘要

| 公共方法 | |
| --- | ---- |
| ```void``` | [```AddFeature(string featureName, string featureVersion)```](#addfeature) |
| ```string``` | [```GetFeatureVersion(string featureName)```](#getfeatureversion) |
| ```void``` | [```RemoveFeature (string featureName)```](#removefeature) |

## <a name="public-methods"></a>公共方法

---

### <a id="addfeature"></a>AddFeature
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public void AddFeature (string featureName, 
                        string featureVersion)
```

向呈现器功能注册添加包含其名称和版本的功能。

| 参数 | |
| --- | --- |
| 名 | ```string``` |
| featureVersion | ```string``` |

#### <a name="sample"></a>示例

```csharp
FeatureRegistration featureRegistration = new FeatureRegistration();
featureRegistration.AddFeature("MyFeature", "1.2.0");
CardRendererRegistration.Instance.RegisterFeatureRegistration(featureRegistration);
```

---

### <a id="getfeatureversion"></a>GetFeatureVersion
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public string GetFeatureVersion (string featureName)
```

检索给定功能的版本。 

| 参数 | |
| --- | --- |
| 名 | ```string``` |

| Returns | |
| --- | --- |
| ```string``` | 给定功能的功能版本 |

#### <a name="sample"></a>示例

```csharp
FeatureRegistration featureRegistration = new FeatureRegistration();
featureRegistration.AddFeature("MyFeature", "1.2.0");
string featureVersion = featureRegistration.GetFeatureVersion("MyFeature"); // 1.2.0
```

---

### <a id="removefeature"></a>RemoveFeature
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public void RemoveFeature (string featureName)
```

从功能字典中移除给定的功能。

| 参数 | |
| --- | --- |
| 名 | ```string``` |

#### <a name="sample"></a>示例

```csharp
FeatureRegistration featureRegistration = new FeatureRegistration();
featureRegistration.AddFeature("MyFeature", "1.2.0");
featureRegistration.RemoveFeature("MyFeature");
```