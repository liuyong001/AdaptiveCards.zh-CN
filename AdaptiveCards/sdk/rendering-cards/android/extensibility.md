---
title: Android SDK
author: bekao
ms.author: bekao
ms.date: 09/27/2017
ms.topic: article
ms.openlocfilehash: 378171186599dd8d103111da183b7fc2e6e01c42
ms.sourcegitcommit: e002a988c570072d5bc24a1242eaaac0c9ce90df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2019
ms.locfileid: "67134262"
---
# <a name="extensibility---android"></a><span data-ttu-id="683e7-102">扩展性 - Android</span><span class="sxs-lookup"><span data-stu-id="683e7-102">Extensibility - Android</span></span>

## <a name="custom-parsing-of-card-elements"></a><span data-ttu-id="683e7-103">对卡片元素的自定义分析</span><span class="sxs-lookup"><span data-stu-id="683e7-103">Custom Parsing of Card Elements</span></span>

<span data-ttu-id="683e7-104">可以扩展分析器，使之支持已定义的卡片元素。</span><span class="sxs-lookup"><span data-stu-id="683e7-104">You may extend the parser to support card elements that you have defined.</span></span> <span data-ttu-id="683e7-105">例如，假设我们有一个如下所示的新元素类型：</span><span class="sxs-lookup"><span data-stu-id="683e7-105">For example, say we have a new element type that looks like this:</span></span>
```json
{
    "type" : "MyType",
    "MyTypeData" : "My data"
}
```

<span data-ttu-id="683e7-106">那么，我们可以通过以下行来演示如何将其分析为从 BaseCardElement 扩展而来的 CardElement：</span><span class="sxs-lookup"><span data-stu-id="683e7-106">Then the following lines demonstrate how to parse it into a CardElement that extends from the BaseCardElement:</span></span>
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

<span data-ttu-id="683e7-107">下面演示如何注册分析器并获取一个包含自定义元素的 AdaptiveCard 对象：</span><span class="sxs-lookup"><span data-stu-id="683e7-107">And this is how to register the parser and get an AdaptiveCard object that contains the custom element:</span></span>
```java
// Create an ElementParserRegistrationObject and add your parser to it
ElementParserRegistration elementParserRegistration = new ElementParserRegistration();
elementParserRegistration.AddParser("MyType", new MyCardElementParser());

AdaptiveCard adaptiveCard = AdaptiveCard.DeserializeFromString(jsonText, elementParserRegistration);
```

<span data-ttu-id="683e7-108">接下来是呈现自定义元素</span><span class="sxs-lookup"><span data-stu-id="683e7-108">Next comes rendering the custom element</span></span>

## <a name="custom-rendering-of-card-elements"></a><span data-ttu-id="683e7-109">对卡片元素的自定义呈现</span><span class="sxs-lookup"><span data-stu-id="683e7-109">Custom Rendering of Card Elements</span></span>

<span data-ttu-id="683e7-110">若要针对类型定义我们自己的自定义呈现器，我们必须先创建一个从 BaseCardElementParser 扩展的类：</span><span class="sxs-lookup"><span data-stu-id="683e7-110">To define our own custom renderer for our type, we must first create a class that extends from BaseCardElementParser:</span></span>
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

<span data-ttu-id="683e7-111">然后注册该呈现器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="683e7-111">We then register this renderer like so:</span></span>
```java
CardRendererRegistration.getInstance().registerRenderer("MyType", new CustomBlahRenderer());

RenderedAdaptiveCard renderedCard = AdaptiveCardRenderer.getInstance().render(context, getSupportFragmentManager(), adaptiveCard, cardActionHandler, new HostConfig());
```

## <a name="custom-rendering-of-actions"></a><span data-ttu-id="683e7-112">对操作的自定义呈现</span><span class="sxs-lookup"><span data-stu-id="683e7-112">Custom rendering of actions</span></span>

[!IMPORTANT]
> <span data-ttu-id="683e7-113">我们计划在 v1.2 中更改对操作的自定义呈现，但目前尚未完成此项工作</span><span class="sxs-lookup"><span data-stu-id="683e7-113">Changes to the custom rendering of actions are planned for v1.2 but are not completed yet</span></span>

## <a name="custom-image-loading"></a><span data-ttu-id="683e7-114">自定义图像加载</span><span class="sxs-lookup"><span data-stu-id="683e7-114">Custom image loading</span></span>

### <a name="ionlineimageloader"></a><span data-ttu-id="683e7-115">IOnlineImageLoader</span><span class="sxs-lookup"><span data-stu-id="683e7-115">IOnlineImageLoader</span></span>

> [!IMPORTANT]
> <span data-ttu-id="683e7-116">**只能注册一个 IOnlineImageLoader，注册后会覆盖默认的图像检索方式**</span><span class="sxs-lookup"><span data-stu-id="683e7-116">**Only one IOnlineImageLoader can be registered and it takes precedence against the default way of retrieving images**</span></span>

<span data-ttu-id="683e7-117">为了让开发人员获取无法直接从在线源下载或检索的图像，或者获取在检索之前需要执行以前的步骤的图像，我们添加了 IOnlineImageLoader，目的是解决这种情况。</span><span class="sxs-lookup"><span data-stu-id="683e7-117">In order to allow developers to get images that could not just be downloaded or retrieved from an online source or required previous steps before they could be retrieved, the IOnlineImageLoader was added to solve this kind of situations.</span></span> <span data-ttu-id="683e7-118">若要实现 OnlineImageLoader，只能实现以下方法</span><span class="sxs-lookup"><span data-stu-id="683e7-118">To implement an OnlineImageLoader you must only implement the method</span></span> 

```java
public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException
```

<span data-ttu-id="683e7-119">下面是 OnlineImageLoader 的示例，用于更改一只猫的所有图像</span><span class="sxs-lookup"><span data-stu-id="683e7-119">Here's an example of an OnlineImageLoader which changes all images for a cat image</span></span>

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

<span data-ttu-id="683e7-120">最后，若要注册此图像加载器，必须只将以下行添加到代码。</span><span class="sxs-lookup"><span data-stu-id="683e7-120">Finally, to register this image loader, you must only add this line to your code.</span></span>

```java
CardRendererRegistration.getInstance().registerOnlineImageLoader(new OnlineImageLoader());
```

### <a name="iresourceresolver-deprecates-ionlineimageloader"></a><span data-ttu-id="683e7-121">IResourceResolver（弃用 IOnlineImageLoader）</span><span class="sxs-lookup"><span data-stu-id="683e7-121">IResourceResolver (deprecates IOnlineImageLoader)</span></span>

<span data-ttu-id="683e7-122">在 v1.2 中，已向 Android 呈现器添加对完整 ResourceResolver 的支持。</span><span class="sxs-lookup"><span data-stu-id="683e7-122">For v1.2, the support for full ResourceResolvers was added to the android renderer.</span></span> <span data-ttu-id="683e7-123">资源解析程序的实现实际上类似于 IOnlineImageLoader 的实现，但 ResourceResolver 允许开发人员添加多种图像检索方式，可以从单张卡片的任何类型的资源中检索图像，方法是：将每个 ResourceResolver 关联到唯一前缀，在尝试检索图像时，可以查询该前缀。</span><span class="sxs-lookup"><span data-stu-id="683e7-123">The implementation of a resource resolver is really similar to that of a IOnlineImageLoader but having ResourceResolvers allows a developer to add multiple ways to retrieve images from any kind of source in a single card, this is done by linking each ResourceResolver to a unique prefix which will be queried when trying to retrieve an image.</span></span> 

<span data-ttu-id="683e7-124">可以采用如下所示的方式实现 ResourceResolver</span><span class="sxs-lookup"><span data-stu-id="683e7-124">You can implement a ResourceResolver similar to this</span></span>

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

<span data-ttu-id="683e7-125">如前所述，可以注册多个 ResourceResolver。若要注册 ResourceResolver，可以执行以下代码</span><span class="sxs-lookup"><span data-stu-id="683e7-125">As mentioned previously, you can register multiple ResourceResolvers, to register a ResourceResolver you can do this</span></span>

```java
 CardRendererRegistration.getInstance().registerResourceResolver("data", new ResourceResolver());
 CardRendererRegistration.getInstance().registerResourceResolver("anotherPrefix", new AnotherResourceResolver());
```

#### <a name="transforming-an-ionlineimageloader-to-an-iresourceresolver"></a><span data-ttu-id="683e7-126">将 IOnlineImageLoader 转换为 IResourceResolver</span><span class="sxs-lookup"><span data-stu-id="683e7-126">Transforming an IOnlineImageLoader to an IResourceResolver</span></span> 

<span data-ttu-id="683e7-127">将 IOnlineImageLoader 转换为 IResourceResolver 相当简单，因为我们已尝试尽量让后者的方法与 IOnlineImageLoader 的方法类似</span><span class="sxs-lookup"><span data-stu-id="683e7-127">Transforming an IOnlineImageLoader to an IResourceResolver is a fairly easy task as the methods for the latter were tried to keep as similar as the IOnlineImageLoader as possible</span></span>

```java
 // IOnlineImageLoader
 public HttpRequestResult<Bitmap> loadOnlineImage(String url, GenericImageLoaderAsync loader) throws IOException, URISyntaxException

 // IResourceResolver
 public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync) throws IOException, URISyntaxException
 public HttpRequestResult<Bitmap> resolveImageResource(String uri, GenericImageLoaderAsync genericImageLoaderAsync, int maxWidth) throws IOException, URISyntaxException
```

<span data-ttu-id="683e7-128">可以看到，最大的更改是</span><span class="sxs-lookup"><span data-stu-id="683e7-128">As you can see, the biggest changes are</span></span>
* <span data-ttu-id="683e7-129">loadOnlineImage(String, GenericImageLoaderAsync) 已重命名为 resolveImageResource(String, GenericImageLoaderAsync)</span><span class="sxs-lookup"><span data-stu-id="683e7-129">loadOnlineImage(String, GenericImageLoaderAsync) was renamed to resolveImageResource(String, GenericImageLoaderAsync)</span></span>
* <span data-ttu-id="683e7-130">已将 resolveImageResource(String, GenericImageLoaderAsync) 的重载添加为 resolveImageResource(String, GenericImageLoaderAsync, int)，目的是支持需要最大宽度的方案</span><span class="sxs-lookup"><span data-stu-id="683e7-130">an overload for resolveImageResource(String, GenericImageLoaderAsync) was added as resolveImageResource(String, GenericImageLoaderAsync, int) in order to support scenarios where the max width is required</span></span>

## <a name="custom-media-loading"></a><span data-ttu-id="683e7-131">自定义媒体加载</span><span class="sxs-lookup"><span data-stu-id="683e7-131">Custom media loading</span></span>

> [!IMPORTANT]
> <span data-ttu-id="683e7-132">**请记住，IOnlineMediaLoader 要求已在 API 级别 23 或 Android M 中添加 MediaDataSource**</span><span class="sxs-lookup"><span data-stu-id="683e7-132">**Remember IOnlineMediaLoader requires MediaDataSource was added in API level 23 or Android M**</span></span>

<span data-ttu-id="683e7-133">除了包括媒体元素，还包括 IOnlineMediaLoader 接口，这样开发人员就可以重写用于基础 mediaPlayer 元素的 [MediaDataSource](https://developer.android.com/reference/android/media/MediaDataSource)。</span><span class="sxs-lookup"><span data-stu-id="683e7-133">Along with the inclusion of the media element, also was the inclusion of the IOnlineMediaLoader interface which allows developers to override the [MediaDataSource](https://developer.android.com/reference/android/media/MediaDataSource) used for the underlying mediaPlayer element.</span></span> <span data-ttu-id="683e7-134">**（需要 Android M）**</span><span class="sxs-lookup"><span data-stu-id="683e7-134">**(Requires android M)**</span></span>

<span data-ttu-id="683e7-135">首先需要创建用于实现 IOnlineImageLoader 的类</span><span class="sxs-lookup"><span data-stu-id="683e7-135">The first needed thing to do is creating a class that implements IOnlineImageLoader</span></span>

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

<span data-ttu-id="683e7-136">实现该类以后，即可添加以下代码来注册 OnlineMediaLoader 类</span><span class="sxs-lookup"><span data-stu-id="683e7-136">Once this class has been implemented, you can register your OnlineMediaLoader class by adding</span></span> 
```java
  CardRendererRegistration.getInstance().registerOnlineMediaLoader(new OnlineMediaLoader());
```
