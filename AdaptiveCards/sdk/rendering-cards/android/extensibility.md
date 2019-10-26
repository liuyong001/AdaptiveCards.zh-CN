---
title: Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: 9e13ebad04c780db83d25129a9f5829a9d43ef69
ms.sourcegitcommit: ce044dc969d9b9c47a52bd361bfe2b746071913b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72917121"
---
# <a name="extensibility---android"></a>扩展性 - Android

可对 Android 呈现器进行扩展，以支持多个方案，包括：
* [自定义卡片元素分析](#custom-parsing-of-card-elements)
* [卡片元素的自定义呈现](#custom-rendering-of-card-elements)
* [自定义操作呈现](#custom-rendering-of-actions)（自1.2 版后）
* [自定义图像加载](#custom-image-loading)（自 v 1.0.1）
* [自定义媒体加载](#custom-media-loading)（自1.1 以来）

## <a name="custom-parsing-of-card-elements"></a>对卡片元素的自定义分析

可以扩展分析器，使之支持已定义的卡片元素。 例如，假设我们有一个如下所示的新元素类型：
```json
{
    "type" : "MyType",
    "MyTypeData" : "My data"
}
```

那么，我们可以通过以下行来演示如何将其分析为从 BaseCardElement 扩展而来的 CardElement：
```java
public class MyCustomCardElement extends BaseCardElement
{

    public MyCustomCardElement(CardElementType type) {
        super(type);
    }

    public String getMyTypeData()
    {
        return myTypeData;
    }

    public void setMyTypeData(String data)
    {
        myTypeData = data;
    }

    private String myTypeData;
}

public class MyCardElementParser extends BaseCardElementParser
{
    @Override
    public BaseCardElement Deserialize(ElementParserRegistration elementParserRegistration, ActionParserRegistration actionParserRegistration, JsonValue value)
    {
        MyCustomCardElement element = new CustomCardElement(CardElementType.Custom);
        element.SetElementTypeString("MyType");
        String val = value.getString();
        try {
            JSONObject obj = new JSONObject(val);
            element.setMyTypeData(obj.getString("secret"));
        } catch (JSONException e) {
            e.printStackTrace();
            element.setMyTypeData("Failed");
        }
        return element;
    }
}
```

下面演示如何注册分析器并获取一个包含自定义元素的 AdaptiveCard 对象：
```java
// Create an ElementParserRegistrationObject and add your parser to it
ElementParserRegistration elementParserRegistration = new ElementParserRegistration();
elementParserRegistration.AddParser("MyType", new MyCardElementParser());

AdaptiveCard adaptiveCard = AdaptiveCard.DeserializeFromString(jsonText, elementParserRegistration);
```

接下来是呈现自定义元素

## <a name="custom-rendering-of-card-elements"></a>对卡片元素的自定义呈现

> [!IMPORTANT]
>
> **重大更改列表**
>
> [v1.2 的重大更改](#breaking-changes-for-v12)

若要为类型定义我自己的自定义呈现器，必须首先创建一个从 ```BaseCardElementRenderer```扩展的类：
```java
public class MyCardElementRenderer extends BaseCardElementRenderer
{
    @Override
    public View render(Context context, FragmentManager fragmentManager, ViewGroup viewGroup, BaseCardElement baseCardElement, Vector<IInputHandler> inputActionHandlerList, ICardActionHandler cardActionHandler, HostConfig hostConfig, ContainerStyle containerStyle) {

        //Call findImplObj on baseCardElement to get the instance we returned at parse. We can then cast that object to our type
        CustomCardElement element = (CustomCardElement) baseCardElement.findImplObj();

        //Create some view and add it to the view group
        TextView textView = new TextView(context);
        textView.setText(element.getMyTypeData());
        textView.setAllCaps(true);
        viewGroup.addView(textView);

        //return the view
        return textView;
    }
}
```

然后注册该呈现器，如下所示：
```java
CardRendererRegistration.getInstance().registerRenderer("MyType", new CustomBlahRenderer());

RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, adaptiveCard, cardActionHandler,  hostConfig);
```

### <a name="breaking-changes-for-v12"></a>针对1.2 版的重大更改

已将 ```render``` 方法更改为包括 ```RenderedAdaptiveCard``` 参数，并更改了 ContainerStyle 当前包含的 RenderArgs 的 ```ContainerStyle```，以便扩展 BaseCardElementRenderer 的类应如下所示

```
public class MyCardElementRenderer extends BaseCardElementRenderer
{
    @Override
    public View render(RenderedAdaptiveCard renderedAdaptiveCard, Context context, FragmentManager fragmentManager, ViewGroup viewGroup,
                       BaseCardElement baseCardElement, ICardActionHandler cardActionHandler, HostConfig hostConfig, RenderArgs renderArgs)
    { }
}
```

## <a name="custom-parsing-of-card-actions"></a>自定义卡操作分析

类似于分析中的自定义卡片元素。 例如，假设我们有一个新的操作类型，如下所示：
```json
{
    "type" : "MyAction",
    "ActionData" : "My data"
}
```

下面的代码行演示了如何将其分析为从 ```BaseActionElement```扩展的 ActionElement：
```java
public class MyActionElement extends BaseActionElement
{
    public MyActionElement(ActionType type) 
    {
        super(type);
    }

    public String getActionData()
    {
        return mActionData;
    }

    public void setActionData(String s)
    {
        mActionData = s;
    }

    private String mActionData;
    public static final String MyActionId = "myAction";
}

public class MyActionParser extends ActionElementParser
{
    @Override
    public BaseActionElement Deserialize(ParseContext context, JsonValue value)
    {
        MyActionElement element = new MyActionElement(ActionType.Custom);
        element.SetElementTypeString(MyActionElement.MyActionId);
        String val = value.getString();
        try {
            JSONObject obj = new JSONObject(val);
            element.setActionData(obj.getString("ActionData"));
        } catch (JSONException e) {
            e.printStackTrace();
            element.setActionData("Failure");
        }
        return element;
    }

    @Override
    public BaseActionElement DeserializeFromString(ParseContext context, String jsonString)
    {
        MyActionElement element = new MyActionElement(ActionType.Custom);
        element.SetElementTypeString(MyActionElement.MyActionId);
        try {
            JSONObject obj = new JSONObject(jsonString);
            element.setBackwardString(obj.getString("ActionData"));
        } catch (JSONException e) {
            e.printStackTrace();
            element.setBackwardString("Failure");
        }
        return element;
    }
}
```

接下来的代码行演示如何注册分析器并获取包含自定义 action 元素的 AdaptiveCard 对象：
```java
// Create an ActionParserRegistration and add your parser to it
ActionParserRegistration actionParserRegistration = new ActionParserRegistration();
actionParserRegistration.AddParser(MyActionElement.MyActionId, new MyActionParser());

ParseContext context = new ParseContext(null, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

接下来，呈现自定义操作

## <a name="custom-rendering-of-actions"></a>操作的自定义呈现

若要定义自己的类型的自定义操作呈现器，必须首先创建一个从 ```BaseActionElementRenderer```扩展的类：
```java
public class MyActionRenderer extends BaseActionElementRenderer
{
    @Override
    public Button render(RenderedAdaptiveCard renderedCard,
                         Context context,
                         FragmentManager fragmentManager,
                         ViewGroup viewGroup,
                         BaseActionElement baseActionElement,
                         ICardActionHandler cardActionHandler,
                         HostConfig hostConfig,
                         RenderArgs renderArgs)
    {
        Button myActionButton = new Button(context);

        CustomActionElement customAction = (CustomActionElement) baseActionElement.findImplObj();

        myActionButton.setBackgroundColor(getResources().getColor(R.color.greenActionColor));
        myActionButton.setText(customAction.getMessage());
        myActionButton.setAllCaps(false);
        myActionButton.setOnClickListener(new BaseActionElementRenderer.ActionOnClickListener(renderedCard, baseActionElement, cardActionHandler));

        viewGroup.addView(myActionButton);

        return myActionButton;
    }
}
```

然后注册该呈现器，如下所示：
```java
CardRendererRegistration.getInstance().registerActionRenderer("myAction", new CustomActionRenderer());

RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, adaptiveCard, cardActionHandler, hostConfig);
```

## <a name="custom-rendering-of-actions"></a>对操作的自定义呈现

> [!IMPORTANT]
> 我们计划在 v1.2 中更改对操作的自定义呈现，但目前尚未完成此项工作

## <a name="custom-image-loading"></a>自定义图像加载

### <a name="ionlineimageloader"></a>IOnlineImageLoader

> [!IMPORTANT]
> **只能注册一个 IOnlineImageLoader，注册后会覆盖默认的图像检索方式**

为了让开发人员获取无法直接从在线源下载或检索的图像，或者获取在检索之前需要执行以前的步骤的图像，我们添加了 IOnlineImageLoader，目的是解决这种情况。 若要实现 OnlineImageLoader，只能实现以下方法 

```java
public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException
```

下面是 OnlineImageLoader 的示例，用于更改一只猫的所有图像

```java
public class OnlineImageLoader implements IOnlineImageLoader
{
    public OnlineImageLoader(){}

    @Override
    public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException
    {
        String catImnageUri = "http://adaptivecards.io/content/cats/1.png";
        byte[] bytes = HttpRequestHelper.get(catImnageUri);
        if (bytes == null)
        {
            throw new IOException("Failed to retrieve content from " + catImnageUri);
        }

        Bitmap bitmap = BitmapFactory.decodeByteArray(bytes, 0, bytes.length);

        if (bitmap == null)
        {
            throw new IOException("Failed to convert content to bitmap: " + new String(bytes));
        }

        return new HttpRequestResult<>(bitmap);
    }
}
```

最后，若要注册此图像加载器，必须只将以下行添加到代码。

```java
CardRendererRegistration.getInstance().registerOnlineImageLoader(new OnlineImageLoader());
```

### <a name="iresourceresolver-deprecates-ionlineimageloader"></a>IResourceResolver（弃用 IOnlineImageLoader）

在 v1.2 中，已向 Android 呈现器添加对完整 ResourceResolver 的支持。 资源解析程序的实现实际上类似于 IOnlineImageLoader 的实现，但 ResourceResolver 允许开发人员添加多种图像检索方式，可以从单张卡片的任何类型的资源中检索图像，方法是：将每个 ResourceResolver 关联到唯一前缀，在尝试检索图像时，可以查询该前缀。 

可以采用如下所示的方式实现 ResourceResolver

```java
public class ResourceResolver implements IResourceResolver
{
    @Override
    public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync) throws IOException, URISyntaxException
    {
        Bitmap bitmap;
        String dataUri = AdaptiveBase64Util.ExtractDataFromUri(uri);
        CharVector decodedDataUri = AdaptiveBase64Util.Decode(dataUri);
        byte[] decodedByteArray = Util.getBytes(decodedDataUri);
        bitmap = BitmapFactory.decodeByteArray(decodedByteArray, 0, decodedByteArray.length);

        return new HttpRequestResult<>(bitmap);
    }

    @Override
    public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync, int maxWidth) throws IOException, URISyntaxException
    {
        Bitmap bitmap;
        String dataUri = AdaptiveBase64Util.ExtractDataFromUri(uri);
        CharVector decodedDataUri = AdaptiveBase64Util.Decode(dataUri);

        if (uri.startsWith("data:image/svg")) {
            String svgString = AdaptiveBase64Util.ExtractDataFromUri(uri);
            String decodedSvgString = URLDecoder.decode(svgString, "UTF-8");
            Sharp sharp = Sharp.loadString(decodedSvgString);
            Drawable drawable = sharp.getDrawable();
            bitmap = ImageUtil.drawableToBitmap(drawable, maxWidth);
        }
        else
        {
            try
            {
                return genericImageLoaderAsync.loadDataUriImage(uri);
            }
            catch (Exception e)
            {
                return new HttpRequestResult<>(e);
            }
        }

        return new HttpRequestResult<>(bitmap);
    }
}
```

如前所述，可以注册多个 ResourceResolver。若要注册 ResourceResolver，可以执行以下代码

```java
 CardRendererRegistration.getInstance().registerResourceResolver("data", new ResourceResolver());
 CardRendererRegistration.getInstance().registerResourceResolver("anotherPrefix", new AnotherResourceResolver());
```

#### <a name="transforming-an-ionlineimageloader-to-an-iresourceresolver"></a>将 IOnlineImageLoader 转换为 IResourceResolver 

将 IOnlineImageLoader 转换为 IResourceResolver 相当简单，因为我们已尝试尽量让后者的方法与 IOnlineImageLoader 的方法类似

```java
 // IOnlineImageLoader
 public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException

 // IResourceResolver
 public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync) throws IOException, URISyntaxException
 public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync, int maxWidth) throws IOException, URISyntaxException
```

可以看到，最大的更改是

* 已将 ```loadOnlineImage(String, GenericImageLoaderAsync)``` 重命名为 ```resolveImageResource(String, GenericImageLoaderAsync)```
* ```resolveImageResource(String, GenericImageLoaderAsync)``` 的重载已添加为 ```resolveImageResource(String, GenericImageLoaderAsync, int)``` 以支持最大宽度需要的方案

## <a name="custom-media-loading"></a>自定义媒体加载

> [!IMPORTANT]
> **请记住 ```IOnlineMediaLoader``` 需要在 API 级别23或 Android M 中添加 ```MediaDataSource```**

除了包括媒体元素，还包括 IOnlineMediaLoader 接口，这样开发人员就可以重写用于基础 mediaPlayer 元素的 [MediaDataSource](https://developer.android.com/reference/android/media/MediaDataSource)。 **（需要 Android M）**

首先需要创建用于实现 IOnlineImageLoader 的类

```java
@RequiresApi(api = Build.VERSION_CODES.M)
public class OnlineMediaLoader implements IOnlineMediaLoader
{
    /* This class checks if the media source exists */
    public class OnlineFileAvailableChecker extends AsyncTask<String, Void, Boolean>
    {
        public OnlineFileAvailableChecker(String uri)
        {
            m_uri = uri;
        }

        @Override
        protected Boolean doInBackground(String... strings) {
            // if the provided uri is a valid uri or is valid with the resource resolver, then use that
            // otherwise, try to get the media from a local file
            try
            {
                HttpRequestHelper.query(m_uri);
                return true;
            }
            catch (Exception e)
            {
                // Do nothing if the media was not found at all
                e.printStackTrace();
                return false;
            }
        }

        private String m_uri;
   }

       
   @Override
   public MediaDataSource loadOnlineMedia(MediaSourceVector mediaSources, IMediaDataSourceOnPreparedListener mediaDataSourceOnPreparedListener)
   {
       final long mediaSourcesSize = mediaSources.size();
       for(int i = 0; i < mediaSourcesSize; i++)
       {
           String mediaUri = mediaSources.get(i).GetUrl();

           OnlineFileAvailableChecker checker = new OnlineFileAvailableChecker(mediaUri);
           try
           {
               Boolean fileExists = checker.execute("").get();
               if(fileExists)
               {
                   return new MediaDataSourceImpl(mediaUri, mediaDataSourceOnPreparedListener);
               }
           }
           catch (Exception e) { }
       }
       return null;
    }
}
```

实现该类以后，即可添加以下代码来注册 OnlineMediaLoader 类 
```java
  CardRendererRegistration.getInstance().registerOnlineMediaLoader(new OnlineMediaLoader());
```
