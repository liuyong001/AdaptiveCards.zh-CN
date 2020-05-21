---
title: Android SDK 扩展性
author: almedina-ms
ms.author: almedina
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: 1281a31c333474c1899831acab28c962ce8e4514
ms.sourcegitcommit: c921a7bb15a95c0ceb803ad375501ee3b8bef028
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83631310"
---
# <a name="extensibility---android"></a><span data-ttu-id="664ee-102">扩展性 - Android</span><span class="sxs-lookup"><span data-stu-id="664ee-102">Extensibility - Android</span></span>

<span data-ttu-id="664ee-103">可对 Android 呈现器进行扩展，以支持多个方案，包括：</span><span class="sxs-lookup"><span data-stu-id="664ee-103">The Android renderer can be extended to support multiple scenarios including:</span></span>
* [<span data-ttu-id="664ee-104">对卡片元素的自定义分析</span><span class="sxs-lookup"><span data-stu-id="664ee-104">Custom Parsing of Card Elements</span></span>](#custom-parsing-of-card-elements)
* [<span data-ttu-id="664ee-105">对卡片元素的自定义呈现</span><span class="sxs-lookup"><span data-stu-id="664ee-105">Custom Rendering of Card Elements</span></span>](#custom-rendering-of-card-elements)
* <span data-ttu-id="664ee-106">[自定义操作呈现](#custom-rendering-of-actions)（自1.2 版后）</span><span class="sxs-lookup"><span data-stu-id="664ee-106">[Custom Rendering of Actions](#custom-rendering-of-actions) (Since v1.2)</span></span>
* <span data-ttu-id="664ee-107">[自定义图像加载](#custom-image-loading)（自 v 1.0.1）</span><span class="sxs-lookup"><span data-stu-id="664ee-107">[Custom Image Loading](#custom-image-loading) (Since v1.0.1)</span></span>
* <span data-ttu-id="664ee-108">[自定义媒体加载](#custom-media-loading)（自1.1 以来）</span><span class="sxs-lookup"><span data-stu-id="664ee-108">[Custom Media Loading](#custom-media-loading) (Since v1.1)</span></span>

## <a name="custom-parsing-of-card-elements"></a><span data-ttu-id="664ee-109">对卡片元素的自定义分析</span><span class="sxs-lookup"><span data-stu-id="664ee-109">Custom Parsing of Card Elements</span></span>

<span data-ttu-id="664ee-110">可以扩展分析器，使之支持已定义的卡片元素。</span><span class="sxs-lookup"><span data-stu-id="664ee-110">You may extend the parser to support card elements that you have defined.</span></span> <span data-ttu-id="664ee-111">例如，假设我们有一个如下所示的新元素类型：</span><span class="sxs-lookup"><span data-stu-id="664ee-111">For example, say we have a new element type that looks like this:</span></span>
```json
{
    "type" : "MyType",
    "MyTypeData" : "My data"
}
```

<span data-ttu-id="664ee-112">那么，我们可以通过以下行来演示如何将其分析为从 BaseCardElement 扩展而来的 CardElement：</span><span class="sxs-lookup"><span data-stu-id="664ee-112">Then the following lines demonstrate how to parse it into a CardElement that extends from the BaseCardElement:</span></span>
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

<span data-ttu-id="664ee-113">下面演示如何注册分析器并获取一个包含自定义元素的 AdaptiveCard 对象：</span><span class="sxs-lookup"><span data-stu-id="664ee-113">And this is how to register the parser and get an AdaptiveCard object that contains the custom element:</span></span>
```java
// Create an ElementParserRegistrationObject and add your parser to it
ElementParserRegistration elementParserRegistration = new ElementParserRegistration();
elementParserRegistration.AddParser("MyType", new MyCardElementParser());

AdaptiveCard adaptiveCard = AdaptiveCard.DeserializeFromString(jsonText, elementParserRegistration);
```

<span data-ttu-id="664ee-114">接下来是呈现自定义元素</span><span class="sxs-lookup"><span data-stu-id="664ee-114">Next comes rendering the custom element</span></span>

## <a name="custom-rendering-of-card-elements"></a><span data-ttu-id="664ee-115">对卡片元素的自定义呈现</span><span class="sxs-lookup"><span data-stu-id="664ee-115">Custom Rendering of Card Elements</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="664ee-116">**重大更改列表**</span><span class="sxs-lookup"><span data-stu-id="664ee-116">**List of Breaking Changes**</span></span>
>
> [<span data-ttu-id="664ee-117">v1.2 的重大更改</span><span class="sxs-lookup"><span data-stu-id="664ee-117">Breaking changes for v1.2</span></span>](#breaking-changes-for-v12)

<span data-ttu-id="664ee-118">若要为类型定义我自己的自定义呈现器，必须首先创建一个扩展自的类 ```BaseCardElementRenderer``` ：</span><span class="sxs-lookup"><span data-stu-id="664ee-118">To define our own custom renderer for our type, we must first create a class that extends from ```BaseCardElementRenderer```:</span></span>
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

<span data-ttu-id="664ee-119">然后注册该呈现器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="664ee-119">We then register this renderer like so:</span></span>
```java
CardRendererRegistration.getInstance().registerRenderer("MyType", new CustomBlahRenderer());

RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, adaptiveCard, cardActionHandler,  hostConfig);
```

### <a name="breaking-changes-for-v12"></a><span data-ttu-id="664ee-120">v1.2 的重大更改</span><span class="sxs-lookup"><span data-stu-id="664ee-120">Breaking changes for v1.2</span></span>

<span data-ttu-id="664ee-121">```render```方法已更改为包含 ```RenderedAdaptiveCard``` 参数，并且 ```ContainerStyle``` 已针对 ContainerStyle 现在包含的 RenderArgs 进行了更改，以便扩展 BaseCardElementRenderer 的类应如下所示</span><span class="sxs-lookup"><span data-stu-id="664ee-121">The ```render``` method was changed to include the ```RenderedAdaptiveCard``` parameter and ```ContainerStyle``` was changed for a RenderArgs where the ContainerStyle is now contained so a class that extends BaseCardElementRenderer should look like this</span></span>

```
public class MyCardElementRenderer extends BaseCardElementRenderer
{
    @Override
    public View render(RenderedAdaptiveCard renderedAdaptiveCard, Context context, FragmentManager fragmentManager, ViewGroup viewGroup,
                       BaseCardElement baseCardElement, ICardActionHandler cardActionHandler, HostConfig hostConfig, RenderArgs renderArgs)
    { }
}
```

## <a name="custom-parsing-of-card-actions"></a><span data-ttu-id="664ee-122">自定义卡操作分析</span><span class="sxs-lookup"><span data-stu-id="664ee-122">Custom Parsing of Card Actions</span></span>

<span data-ttu-id="664ee-123">类似于分析中的自定义卡片元素。</span><span class="sxs-lookup"><span data-stu-id="664ee-123">Similarly to parsing custom card elements in v1.2 the possibility to parse custom actions was introduced.</span></span> <span data-ttu-id="664ee-124">例如，假设我们有一个新的操作类型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="664ee-124">For example, say we have a new action type that looks like this:</span></span>
```json
{
    "type" : "MyAction",
    "ActionData" : "My data"
}
```

<span data-ttu-id="664ee-125">下面的代码行演示了如何将其分析为从扩展的 ActionElement ```BaseActionElement``` ：</span><span class="sxs-lookup"><span data-stu-id="664ee-125">Then the following lines demonstrate how to parse it into a ActionElement that extends from the ```BaseActionElement```:</span></span>
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

<span data-ttu-id="664ee-126">接下来的代码行演示如何注册分析器并获取包含自定义 action 元素的 AdaptiveCard 对象：</span><span class="sxs-lookup"><span data-stu-id="664ee-126">And the next lines demonstrate how to register the parser and get an AdaptiveCard object that contains the custom action element:</span></span>
```java
// Create an ActionParserRegistration and add your parser to it
ActionParserRegistration actionParserRegistration = new ActionParserRegistration();
actionParserRegistration.AddParser(MyActionElement.MyActionId, new MyActionParser());

ParseContext context = new ParseContext(null, actionParserRegistration);
ParseResult parseResult = AdaptiveCard.DeserializeFromString(jsonText, AdaptiveCardRenderer.VERSION, context);
```

<span data-ttu-id="664ee-127">接下来，呈现自定义操作</span><span class="sxs-lookup"><span data-stu-id="664ee-127">Next comes rendering the custom action</span></span>

## <a name="custom-rendering-of-actions"></a><span data-ttu-id="664ee-128">操作的自定义呈现</span><span class="sxs-lookup"><span data-stu-id="664ee-128">Custom Rendering of Actions</span></span>

<span data-ttu-id="664ee-129">若要为类型定义我自己的自定义操作呈现器，必须首先创建一个扩展自的类 ```BaseActionElementRenderer``` ：</span><span class="sxs-lookup"><span data-stu-id="664ee-129">To define our own custom action renderer for our type, we must first create a class that extends from ```BaseActionElementRenderer```:</span></span>
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

<span data-ttu-id="664ee-130">然后注册该呈现器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="664ee-130">We then register this renderer like so:</span></span>
```java
CardRendererRegistration.getInstance().registerActionRenderer("myAction", new CustomActionRenderer());

RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, fragmentManager, adaptiveCard, cardActionHandler, hostConfig);
```

## <a name="custom-rendering-of-actions"></a><span data-ttu-id="664ee-131">对操作的自定义呈现</span><span class="sxs-lookup"><span data-stu-id="664ee-131">Custom rendering of actions</span></span>

> [!IMPORTANT]
> <span data-ttu-id="664ee-132">我们计划在 v1.2 中更改对操作的自定义呈现，但目前尚未完成此项工作</span><span class="sxs-lookup"><span data-stu-id="664ee-132">Changes to the custom rendering of actions are planned for v1.2 but are not completed yet</span></span>

## <a name="custom-image-loading"></a><span data-ttu-id="664ee-133">自定义图像加载</span><span class="sxs-lookup"><span data-stu-id="664ee-133">Custom image loading</span></span>

### <a name="ionlineimageloader"></a><span data-ttu-id="664ee-134">IOnlineImageLoader</span><span class="sxs-lookup"><span data-stu-id="664ee-134">IOnlineImageLoader</span></span>

> [!IMPORTANT]
> <span data-ttu-id="664ee-135">**只能注册一个 IOnlineImageLoader，注册后会覆盖默认的图像检索方式**</span><span class="sxs-lookup"><span data-stu-id="664ee-135">**Only one IOnlineImageLoader can be registered and it takes precedence against the default way of retrieving images**</span></span>

<span data-ttu-id="664ee-136">为了让开发人员获取无法直接从在线源下载或检索的图像，或者获取在检索之前需要执行以前的步骤的图像，我们添加了 IOnlineImageLoader，目的是解决这种情况。</span><span class="sxs-lookup"><span data-stu-id="664ee-136">In order to allow developers to get images that could not just be downloaded or retrieved from an online source or required previous steps before they could be retrieved, the IOnlineImageLoader was added to solve this kind of situations.</span></span> <span data-ttu-id="664ee-137">若要实现 OnlineImageLoader，只能实现以下方法</span><span class="sxs-lookup"><span data-stu-id="664ee-137">To implement an OnlineImageLoader you must only implement the method</span></span> 

```java
public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException
```

<span data-ttu-id="664ee-138">下面是 OnlineImageLoader 的示例，用于更改一只猫的所有图像</span><span class="sxs-lookup"><span data-stu-id="664ee-138">Here's an example of an OnlineImageLoader which changes all images for a cat image</span></span>

```java
public class OnlineImageLoader implements IOnlineImageLoader
{
    public OnlineImageLoader(){}

    @Override
    public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException
    {
        String catImageUri = "http://adaptivecards.io/content/cats/1.png";
        byte[] bytes = HttpRequestHelper.get(catImageUri);
        if (bytes == null)
        {
            throw new IOException("Failed to retrieve content from " + catImageUri);
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

<span data-ttu-id="664ee-139">最后，若要注册此图像加载器，必须只将以下行添加到代码。</span><span class="sxs-lookup"><span data-stu-id="664ee-139">Finally, to register this image loader, you must only add this line to your code.</span></span>

```java
CardRendererRegistration.getInstance().registerOnlineImageLoader(new OnlineImageLoader());
```

### <a name="iresourceresolver-deprecates-ionlineimageloader"></a><span data-ttu-id="664ee-140">IResourceResolver（弃用 IOnlineImageLoader）</span><span class="sxs-lookup"><span data-stu-id="664ee-140">IResourceResolver (deprecates IOnlineImageLoader)</span></span>

<span data-ttu-id="664ee-141">在 v1.2 中，已向 Android 呈现器添加对完整 ResourceResolver 的支持。</span><span class="sxs-lookup"><span data-stu-id="664ee-141">For v1.2, the support for full ResourceResolvers was added to the android renderer.</span></span> <span data-ttu-id="664ee-142">资源解析程序的实现实际上类似于 IOnlineImageLoader 的实现，但 ResourceResolver 允许开发人员添加多种图像检索方式，可以从单张卡片的任何类型的资源中检索图像，方法是：将每个 ResourceResolver 关联到唯一前缀，在尝试检索图像时，可以查询该前缀。</span><span class="sxs-lookup"><span data-stu-id="664ee-142">The implementation of a resource resolver is really similar to that of a IOnlineImageLoader but having ResourceResolvers allows a developer to add multiple ways to retrieve images from any kind of source in a single card, this is done by linking each ResourceResolver to a unique prefix which will be queried when trying to retrieve an image.</span></span> 

<span data-ttu-id="664ee-143">可以采用如下所示的方式实现 ResourceResolver</span><span class="sxs-lookup"><span data-stu-id="664ee-143">You can implement a ResourceResolver similar to this</span></span>

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

<span data-ttu-id="664ee-144">如前所述，可以注册多个 ResourceResolver。若要注册 ResourceResolver，可以执行以下代码</span><span class="sxs-lookup"><span data-stu-id="664ee-144">As mentioned previously, you can register multiple ResourceResolvers, to register a ResourceResolver you can do this</span></span>

```java
 CardRendererRegistration.getInstance().registerResourceResolver("data", new ResourceResolver());
 CardRendererRegistration.getInstance().registerResourceResolver("anotherPrefix", new AnotherResourceResolver());
```

#### <a name="transforming-an-ionlineimageloader-to-an-iresourceresolver"></a><span data-ttu-id="664ee-145">将 IOnlineImageLoader 转换为 IResourceResolver</span><span class="sxs-lookup"><span data-stu-id="664ee-145">Transforming an IOnlineImageLoader to an IResourceResolver</span></span> 

<span data-ttu-id="664ee-146">将 IOnlineImageLoader 转换为 IResourceResolver 相当简单，因为我们已尝试尽量让后者的方法与 IOnlineImageLoader 的方法类似</span><span class="sxs-lookup"><span data-stu-id="664ee-146">Transforming an IOnlineImageLoader to an IResourceResolver is a fairly easy task as the methods for the latter were tried to keep as similar as the IOnlineImageLoader as possible</span></span>

```java
 // IOnlineImageLoader
 public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException

 // IResourceResolver
 public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync) throws IOException, URISyntaxException
 public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync, int maxWidth) throws IOException, URISyntaxException
```

<span data-ttu-id="664ee-147">可以看到，最大的更改是</span><span class="sxs-lookup"><span data-stu-id="664ee-147">As you can see, the biggest changes are</span></span>

* <span data-ttu-id="664ee-148">```loadOnlineImage(String, GenericImageLoaderAsync)``` 已重命名为 ```resolveImageResource(String, GenericImageLoaderAsync)```</span><span class="sxs-lookup"><span data-stu-id="664ee-148">```loadOnlineImage(String, GenericImageLoaderAsync)``` was renamed to ```resolveImageResource(String, GenericImageLoaderAsync)```</span></span>
* <span data-ttu-id="664ee-149">为 ```resolveImageResource(String, GenericImageLoaderAsync)``` 添加了的重载， ```resolveImageResource(String, GenericImageLoaderAsync, int)``` 以便支持最大宽度是必需的方案</span><span class="sxs-lookup"><span data-stu-id="664ee-149">an overload for ```resolveImageResource(String, GenericImageLoaderAsync)``` was added as ```resolveImageResource(String, GenericImageLoaderAsync, int)``` in order to support scenarios where the max width is required</span></span>

## <a name="custom-media-loading"></a><span data-ttu-id="664ee-150">自定义媒体加载</span><span class="sxs-lookup"><span data-stu-id="664ee-150">Custom Media Loading</span></span>

> [!IMPORTANT]
> <span data-ttu-id="664ee-151">**请 ```IOnlineMediaLoader``` 记住 ```MediaDataSource``` ，要求在 API 级别23或 Android M 中添加了**</span><span class="sxs-lookup"><span data-stu-id="664ee-151">**Remember ```IOnlineMediaLoader``` requires ```MediaDataSource``` which was added in API level 23 or Android M**</span></span>

<span data-ttu-id="664ee-152">除了包括媒体元素，还包括 IOnlineMediaLoader 接口，这样开发人员就可以重写用于基础 mediaPlayer 元素的 [MediaDataSource](https://developer.android.com/reference/android/media/MediaDataSource)。</span><span class="sxs-lookup"><span data-stu-id="664ee-152">Along with the inclusion of the media element, also was the inclusion of the IOnlineMediaLoader interface which allows developers to override the [MediaDataSource](https://developer.android.com/reference/android/media/MediaDataSource) used for the underlying mediaPlayer element.</span></span> <span data-ttu-id="664ee-153">**（需要 Android M）**</span><span class="sxs-lookup"><span data-stu-id="664ee-153">**(Requires android M)**</span></span>

<span data-ttu-id="664ee-154">首先需要创建用于实现 IOnlineImageLoader 的类</span><span class="sxs-lookup"><span data-stu-id="664ee-154">The first needed thing to do is creating a class that implements IOnlineImageLoader</span></span>

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

<span data-ttu-id="664ee-155">实现该类以后，即可添加以下代码来注册 OnlineMediaLoader 类</span><span class="sxs-lookup"><span data-stu-id="664ee-155">Once this class has been implemented, you can register your OnlineMediaLoader class by adding</span></span> 
```java
  CardRendererRegistration.getInstance().registerOnlineMediaLoader(new OnlineMediaLoader());
```
