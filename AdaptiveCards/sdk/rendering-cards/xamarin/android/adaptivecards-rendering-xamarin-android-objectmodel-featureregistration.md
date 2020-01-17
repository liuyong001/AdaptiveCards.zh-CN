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
# <a name="feature-registration"></a><span data-ttu-id="425cb-102">功能注册</span><span class="sxs-lookup"><span data-stu-id="425cb-102">Feature Registration</span></span>

```csharp
public class FeatureRegistration : Java.Lang.Object 
```

<span data-ttu-id="425cb-103">**命名空间**</span><span class="sxs-lookup"><span data-stu-id="425cb-103">**Namespace**</span></span>
```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.ObjectModel
```

## <a name="summary"></a><span data-ttu-id="425cb-104">摘要</span><span class="sxs-lookup"><span data-stu-id="425cb-104">Summary</span></span>

| <span data-ttu-id="425cb-105">公共方法</span><span class="sxs-lookup"><span data-stu-id="425cb-105">Public methods</span></span> | |
| --- | ---- |
| ```void``` | [```AddFeature(string featureName, string featureVersion)```](#addfeature) |
| ```string``` | [```GetFeatureVersion(string featureName)```](#getfeatureversion) |
| ```void``` | [```RemoveFeature (string featureName)```](#removefeature) |

## <a name="public-methods"></a><span data-ttu-id="425cb-106">公共方法</span><span class="sxs-lookup"><span data-stu-id="425cb-106">Public Methods</span></span>

---

### <a id="addfeature"></a><span data-ttu-id="425cb-107">AddFeature</span><span class="sxs-lookup"><span data-stu-id="425cb-107">AddFeature</span></span>
<p style='text-align:right'><span data-ttu-id="425cb-108">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="425cb-108">Added in version 0.1.0</span></span></p>

```csharp
public void AddFeature (string featureName, 
                        string featureVersion)
```

<span data-ttu-id="425cb-109">向呈现器功能注册添加包含其名称和版本的功能。</span><span class="sxs-lookup"><span data-stu-id="425cb-109">Adds a feature containing its name and version to the renderer feature registration.</span></span>

| <span data-ttu-id="425cb-110">参数</span><span class="sxs-lookup"><span data-stu-id="425cb-110">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="425cb-111">名</span><span class="sxs-lookup"><span data-stu-id="425cb-111">featureName</span></span> | ```string``` |
| <span data-ttu-id="425cb-112">featureVersion</span><span class="sxs-lookup"><span data-stu-id="425cb-112">featureVersion</span></span> | ```string``` |

#### <a name="sample"></a><span data-ttu-id="425cb-113">示例</span><span class="sxs-lookup"><span data-stu-id="425cb-113">Sample</span></span>

```csharp
FeatureRegistration featureRegistration = new FeatureRegistration();
featureRegistration.AddFeature("MyFeature", "1.2.0");
CardRendererRegistration.Instance.RegisterFeatureRegistration(featureRegistration);
```

---

### <a id="getfeatureversion"></a><span data-ttu-id="425cb-114">GetFeatureVersion</span><span class="sxs-lookup"><span data-stu-id="425cb-114">GetFeatureVersion</span></span>
<p style='text-align:right'><span data-ttu-id="425cb-115">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="425cb-115">Added in version 0.1.0</span></span></p>

```csharp
public string GetFeatureVersion (string featureName)
```

<span data-ttu-id="425cb-116">检索给定功能的版本。</span><span class="sxs-lookup"><span data-stu-id="425cb-116">Retrieves the version for a given feature.</span></span> 

| <span data-ttu-id="425cb-117">参数</span><span class="sxs-lookup"><span data-stu-id="425cb-117">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="425cb-118">名</span><span class="sxs-lookup"><span data-stu-id="425cb-118">featureName</span></span> | ```string``` |

| <span data-ttu-id="425cb-119">Returns</span><span class="sxs-lookup"><span data-stu-id="425cb-119">Returns</span></span> | |
| --- | --- |
| ```string``` | <span data-ttu-id="425cb-120">给定功能的功能版本</span><span class="sxs-lookup"><span data-stu-id="425cb-120">Feature version for the given feature</span></span> |

#### <a name="sample"></a><span data-ttu-id="425cb-121">示例</span><span class="sxs-lookup"><span data-stu-id="425cb-121">Sample</span></span>

```csharp
FeatureRegistration featureRegistration = new FeatureRegistration();
featureRegistration.AddFeature("MyFeature", "1.2.0");
string featureVersion = featureRegistration.GetFeatureVersion("MyFeature"); // 1.2.0
```

---

### <a id="removefeature"></a><span data-ttu-id="425cb-122">RemoveFeature</span><span class="sxs-lookup"><span data-stu-id="425cb-122">RemoveFeature</span></span>
<p style='text-align:right'><span data-ttu-id="425cb-123">已在版本0.1.0 中添加</span><span class="sxs-lookup"><span data-stu-id="425cb-123">Added in version 0.1.0</span></span></p>

```csharp
public void RemoveFeature (string featureName)
```

<span data-ttu-id="425cb-124">从功能字典中移除给定的功能。</span><span class="sxs-lookup"><span data-stu-id="425cb-124">Removes the given feature from the feature dictionary.</span></span>

| <span data-ttu-id="425cb-125">参数</span><span class="sxs-lookup"><span data-stu-id="425cb-125">Parameters</span></span> | |
| --- | --- |
| <span data-ttu-id="425cb-126">名</span><span class="sxs-lookup"><span data-stu-id="425cb-126">featureName</span></span> | ```string``` |

#### <a name="sample"></a><span data-ttu-id="425cb-127">示例</span><span class="sxs-lookup"><span data-stu-id="425cb-127">Sample</span></span>

```csharp
FeatureRegistration featureRegistration = new FeatureRegistration();
featureRegistration.AddFeature("MyFeature", "1.2.0");
featureRegistration.RemoveFeature("MyFeature");
```