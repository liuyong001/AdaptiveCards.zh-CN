---
title: AdaptiveCard 类-Xamarin. Android SDK
author: almedina-ms
ms.author: almedina
ms.date: 12/02/2019
ms.topic: article
ms.openlocfilehash: 0f64bf635023271d8b40bf55fce079300aae7652
ms.sourcegitcommit: 9a9973129c36a41f5e4af30d95ffc146820ad173
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76146081"
---
# <a name="adaptivecard"></a>AdaptiveCard

```csharp
public class AdaptiveCard : Java.Lang.Object 
```

**命名空间**

```csharp
namespace AdaptiveCards.Rendering.Xamarin.Android.ObjectModel
```

## <a name="summary"></a>摘要

| 属性 | |
| ---- | --- |
| “操作” | 要在卡片的操作栏中显示的操作。 |
| BackgroundImage | 指定卡的背景图像。 |
| 正文 | 要在主要卡区域显示的卡片元素。 |
| {2&gt;ElementType&lt;2} | 必须为 "AdaptiveCard"。 |
| FallbackText | 当客户端不支持指定的版本时显示的文本（可能包含 markdown）。 |
| Height | |
| InputNecessityIndicators | |
| “语言” | 卡中使用的 2-字母 ISO-639-1 语言。 用于本地化所有日期/时间函数。 |
| MinHeight | 指定卡的最小高度。 |
| SelectAction | 在点击或选择卡时将调用的操作。 不支持 ShowCard。 |
| Speak | 指定应为此整个卡口述的内容。 这是简单文本或 SSML 片段。 |
| “造型” | |
| 版本 | 此卡所需的架构版本。 如果客户端低于此版本，将呈现 fallbackText。 注意： ShowCard 中的卡不需要版本。 但是，它对于顶级卡是必需的。 |
| System.windows.controls.control.verticalcontentalignment | 定义内容应在容器中垂直对齐的方式。 仅适用于固定高度的卡，或指定了 minHeight 的卡。 |

&nbsp;

**公共构造函数**

---

<a href="#ctor0"><div>
```csharp
AdaptiveCard(string version, string fallbackText, BackgroundImage backgroundImage, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight)
```
</div></a>

<a href="#ctor1"><div>
```csharp
AdaptiveCard(string version, string fallbackText, BackgroundImage backgroundImage, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight, BaseCardElementVector body, BaseActionElementVector actions)
```
</div></a>

<a href="#ctor2"><div>
```csharp
AdaptiveCard(string version, string fallbackText, string backgroundImageUrl, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight)
```
</div></a>

<a href="#ctor3"><div>
```csharp
AdaptiveCard(string version, string fallbackText, string backgroundImageUrl, ContainerStyle style, string speak, string language, VerticalContentAlignment verticalContentAlignment, HeightType height, long minHeight, BaseCardElementVector body, BaseActionElementVector actions)
```
</div></a>

&nbsp;
| 公共方法 | |
| --- | ---- |
| ```static ParseResult``` | [```DeserializeFromString(string jsonString, string rendererVersion)```](#deserializefromstring0) |
| ```static ParseResult``` | [```DeserializeFromString(string jsonString, string rendererVersion, ParseContext context)```](#deserializefromstring1) |
| ```static AdaptiveCard``` | [```MakeFallbackTextCard(string fallbackText, string language, string speak)```](#makefallbacktextcard) |
| ```string``` | [```Serialize()```](#serialize) |
| ```JsonValue``` | [```SerializeToJsonValue()```](#serializetojsonvalue) |

&nbsp;
## <a name="public-constructors"></a>公共构造函数
---

### <a id="ctor0"></a>AdaptiveCard
<p style='text-align:right'>在版本0.1 中添加</p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    BackgroundImage backgroundImage, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment, 
                    HeightType height, 
                    long minHeight) 
```

| 参数 | |
| --- | --- |
| version | ```string``` |
| fallbackText | ```string``` |
| backgroundImage | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BackgroundImage``` |
| 样式 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| speak | ```string``` |
| language | ```string``` |
| System.windows.controls.control.verticalcontentalignment | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| height | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| minHeight | ```long``` |

&nbsp;&nbsp;

### <a id="ctor1"></a>AdaptiveCard
<p style='text-align:right'>在版本0.1 中添加</p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    BackgroundImage backgroundImage, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment, 
                    HeightType height, 
                    long minHeight, 
                    BaseCardElementVector body, 
                    BaseActionElementVector actions)
```

| 参数 | |
| --- | --- |
| version | ```string``` |
| fallbackText | ```string``` |
| backgroundImage | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BackgroundImage``` |
| 样式 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| speak | ```string``` |
| language | ```string``` |
| System.windows.controls.control.verticalcontentalignment | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| height | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| minHeight | ```long``` |
| 正文 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElementVector``` |
| 操作 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseActionElementVector``` |

&nbsp;&nbsp;

### <a id="ctor2"></a>AdaptiveCard
<p style='text-align:right'>在版本0.1 中添加</p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    string backgroundImageUrl, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment,
                    HeightType height, 
                    long minHeight) 
```

| 参数 | |
| --- | --- |
| version | ```string``` |
| fallbackText | ```string``` |
| backgroundImage | ```string``` |
| 样式 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| speak | ```string``` |
| language | ```string``` |
| System.windows.controls.control.verticalcontentalignment | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| height | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| minHeight | ```long``` |

&nbsp;&nbsp;

### <a id="ctor3"></a>AdaptiveCard
<p style='text-align:right'>在版本0.1 中添加</p>

```csharp
public AdaptiveCard (string version, 
                    string fallbackText, 
                    string backgroundImageUrl, 
                    ContainerStyle style, 
                    string speak, 
                    string language, 
                    VerticalContentAlignment verticalContentAlignment,
                    HeightType height, 
                    long minHeight, 
                    BaseCardElementVector body,
                    BaseActionElementVector actions)

```

| 参数 | |
| --- | --- |
| version | ```string``` |
| fallbackText | ```string``` |
| backgroundImage | ```string``` |
| 样式 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ContainerStyle``` |
| speak | ```string``` |
| language | ```string``` |
| System.windows.controls.control.verticalcontentalignment | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.VerticalContentAlignment``` |
| height | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.HeightType``` |
| minHeight | ```long``` |
| 正文 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseCardElementVector``` |
| 操作 | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.BaseActionElementVector``` |

&nbsp;

## <a name="public-methods"></a>公共方法
---
### <a id="deserializefromstring0"></a>DeserializeFromString
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public static ParseResult DeserializeFromString (string jsonString, string rendererVersion)
```

反序列化给定的自适应卡作为指定呈现器版本的 json 字符串。

| 参数 | |
| --- | --- |
| jsonString | ```string``` |
| rendererVersion | ```string``` |

| Returns | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ParseResult``` | |

#### <a name="sample"></a>示例

```csharp
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.Version);
```

--- 
### <a id="deserializefromstring1"></a>DeserializeFromString
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public static ParseResult DeserializeFromString(string jsonString, string rendererVersion, ParseContext context)
```

使用[ParseContext]()对象将给定的自适应卡反序列化为指定呈现器版本的 json 字符串，以处理自定义元素分析。

| 参数 | |
| --- | --- |
| jsonString | ```string``` |
| rendererVersion | ```string``` |
| context | ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ParseContext``` |

| Returns | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.ParseResult``` | |

#### <a name="sample"></a>示例

```csharp
ParseContext parseContext = new ParseContext(elementParserRegistration, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.Version, parseContext);
```

---

### <a id="makefallbacktextcard"></a>MakeFallbackTextCard
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public static AdaptiveCard MakeFallbackTextCard (string fallbackText, string language, string speak)
```

反序列化给定的自适应卡作为指定呈现器版本的 json 字符串。

| 参数 | |
| --- | --- |
| fallbackText | ```string``` |
| language | ```string``` |
| speak | ```string``` |

| Returns | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.AdaptiveCard``` | 包含 unrendereable 卡的回退文本的自适应卡 |

#### <a name="sample"></a>示例

```csharp
AdaptiveCard adaptiveCard = AdaptiveCard.MakeFallbackTextCard("This card failed to render", "es", "Unrendereable card");
```

---

### <a id="serialize"></a>序列
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public string Serialize ()
```

将自适应卡序列化为其 json 字符串格式。

| Returns | |
| --- | --- |
| ```string``` | 作为 json 字符串的自适应卡 |

#### <a name="sample"></a>示例

```csharp
string jsonString = parseResult.AdaptiveCard.Serialize();
```

---

### <a id="serializetojsonvalue"></a>SerializeToJsonValue
<p style='text-align:right'>已在版本0.1.0 中添加</p>

```csharp
public JsonValue SerializeToJsonValue ()
```

将自适应卡序列化到 json 值对象中。

| Returns | |
| --- | --- |
| ```AdaptiveCards.Rendering.Xamarin.Android.ObjectModel.JsonValue``` | |

#### <a name="sample"></a>示例

```csharp
JsonValue value = parseResult.AdaptiveCard.SerializeToJsonValue();
```