## 常用meta整理

### 概要

标签提供关于HTML文档的元数据。元数据不会显示在页面上，但是对于机器是可读的。它可用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他 web 服务。


### 必要属性

属性    | 值         | 描述
--------|------------|----
content | some text  | 定义与http-equiv或name属性相关的元信息

### 可选属性

属性 | 值 | 描述
----|------|----
name | author / description / keywords / generator / revised / others  | 把 content 属性关联到一个名称。
http-equiv | content-type / expire / refresh / set-cookie  | 把content属性关联到HTTP头部。
content | some text  | 定义用于翻译 content 属性值的格式。


### 网页相关

* **申明编码**

```html
<!DOCTYPE html> <!-- 使用 HTML5 doctype，不区分大小写 -->
<html lang="zh-cmn-Hans"> <!-- 更加标准的 lang 属性写法 http://zhi.hu/XyIa -->
```

```html
<meta charset='utf-8' />
```

* **优先使用 IE 最新版本和 Chrome**

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<!-- 关于X-UA-Compatible -->
<meta http-equiv="X-UA-Compatible" content="IE=6" ><!-- 使用IE6 -->
<meta http-equiv="X-UA-Compatible" content="IE=7" ><!-- 使用IE7 -->
<meta http-equiv="X-UA-Compatible" content="IE=8" ><!-- 使用IE8 -->
```

* **浏览器内核控制：** 国内浏览器很多都是双内核（webkit和Trident），webkit内核高速浏览，IE内核兼容网页和旧版网站。而添加meta标签的网站可以控制浏览器选择何种内核渲染

```html
<meta name="renderer" content="webkit|ie-comp|ie-stand">
```

国内双核浏览器默认内核模式如下：
1. 搜狗高速浏览器、QQ浏览器：IE内核（兼容模式）
1. 360极速浏览器、遨游浏览器：Webkit内核（极速模式）

* **禁止浏览器从本地计算机的缓存中访问页面内容：** 这样设定，访问者将无法脱机浏览。

```html
<meta http-equiv="Pragma" content="no-cache">
```

* **设置http cache时间:** 在快速迭代的项目中，我们可以设置max-age=604800s，也就是七天

```html
<meta http-equiv="Cache-Control" content="max-age=604800" />
```

* **站点适配：** 主要用于PC-手机页的对应关系。


```html
<meta name="mobile-agent"content="format=[wml|xhtml|html5]; url=url">
<!--
[wml|xhtml|html5]根据手机页的协议语言，选择其中一种；
url="url" 后者代表当前PC页所对应的手机页URL，两者必须是一一对应关系。
 -->
```

* **申明网站为pc站，避免被转码：** 

```html
<meta name="applicable-device" content="pc">
```

* **转码申明：** 用百度打开网页可能会对其进行转码（比如贴广告），避免转码可添加如下meta

```html
<meta http-equiv="Cache-Control" content="no-siteapp" />
```

* **规定360安全浏览器使用webki内核进行渲染**

```html
<meta name="renderer" content="webkit">
```


### SEO优化

* **页面关键词：** 每个网页应具有描述该网页内容的一组唯一的关键字。
使用人们可能会搜索，并准确描述网页上所提供信息的描述性和代表性关键字及短语。标记内容太短，则搜索引擎可能不会认为这些内容相关。另外标记不应超过 874 个字符。

```html
<meta name="keywords" content="your tags" />
```

* **页面描述：** 每个网页都应有一个不超过 150 个字符且能准确反映网页内容的描述标签。

```html
<meta name="description" content="150 words" />
```

* **搜索引擎索引方式：** robotterms是一组使用逗号(,)分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。确保正确使用nofollow和noindex属性值。

```html
<meta name="robots" content="index,follow" />
<!--
    all：文件将被检索，且页面上的链接可以被查询；
    none：文件将不被检索，且页面上的链接不可以被查询；
    index：文件将被检索；
    follow：页面上的链接可以被查询；
    noindex：文件将不被检索；
    nofollow：页面上的链接不可以被查询。
 -->
```

* **页面重定向和刷新：** content内的数字代表时间（秒），既多少时间后刷新。如果加url,则会重定向到指定网页（搜索引擎能够自动检测，也很容易被引擎视作误导而受到惩罚）。

```html
<meta http-equiv="refresh" content="0;url=" />
```

* **其他**

```html
<meta name="author" content="author name" /> <!-- 定义网页作者 -->
```

### 移动设备

* **viewport：** 能优化移动浏览器的显示。如果不是响应式网站，不要使用initial-scale或者禁用缩放。
大部分4.7-5寸设备的viewport宽设为360px；5.5寸设备设为400px；iphone6设为375px；ipone6 plus设为414px。

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, user-scalable=no"/>
<!-- `width=device-width` 会导致 iPhone 5 添加到主屏后以 WebApp 全屏模式打开页面时出现黑边  -->
```

1. width：宽度（数值 / device-width）（范围从200到10,000，默认为980 像素）
1. height：高度（数值 / device-height）（范围从223 到10,000）
1. initial-scale：初始的缩放比例 （范围从>0 到10）
1. minimum-scale：允许用户缩放到的最小比例
1. maximum-scale：允许用户缩放到的最大比例
1. user-scalable：用户是否可以手动缩 (no,yes)
1. minimal-ui：可以在页面加载时最小化上下状态栏。（已弃用）

`注意` 很多人使用initial-scale=1到非响应式网站上，这会让网站以100%宽度渲染，用户需要手动移动页面或者缩放。如果和initial-scale=1同时使用user-scalable=no或maximum-scale=1，则用户将不能放大/缩小网页来看到全部的内容。

* **WebApp全屏模式：** 伪装app，离线应用。

```html
<meta name="apple-mobile-web-app-capable" content="yes" /> <!-- 启用 WebApp 全屏模式 -->
```

* **隐藏状态栏/设置状态栏颜色：** 只有在开启WebApp全屏模式时才生效。content的值为default | black | black-translucent 。

```html
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
```

* **添加到主屏后的标题**

```html
<meta name="apple-mobile-web-app-title" content="标题">
```
![view](https://cloud.githubusercontent.com/assets/3378002/15988534/3b48533e-3087-11e6-9f74-f2c8721c15e0.png)

* **忽略数字自动识别为电话号码**

```html
<meta content="telephone=no" name="format-detection" /> 
```

* **忽略识别邮箱**

```html
<meta content="email=no" name="format-detection" />
```

* **添加智能 App 广告条 Smart App Banner：** 告诉浏览器这个网站对应的app，并在页面上显示下载banner(如下图)。

![view1](https://cloud.githubusercontent.com/assets/3378002/15988549/d90954ec-3087-11e6-8efb-a1447e01a167.png)

* **IOS相关**

```html
<meta name="apple-mobile-web-app-title" content="标题">
<!-- 添加到主屏后的标题（iOS 6 新增） -->
<meta name="apple-mobile-web-app-capable" content="yes"/>
<!-- 是否启用 WebApp 全屏模式，删除苹果默认的工具栏和菜单栏 --> 
<meta name="apple-itunes-app" content="app-id=myAppStoreID,
    affiliate-data=myAffiliateData, app-argument=myURL">
<!-- 添加智能 App 广告条 Smart App Banner（iOS 6+ Safari） -->
<meta name="apple-mobile-web-app-status-bar-style" content="black"/>
<!-- 设置苹果工具栏颜色 -->
```

```html
<!-- iOS 图标 begin -->
<link rel="apple-touch-icon-precomposed" href="/apple-touch-icon-57x57-precomposed.png"/>
<!-- iPhone 和 iTouch，默认 57x57 像素，必须有 -->
<link rel="apple-touch-icon-precomposed" sizes="114x114"
    href="/apple-touch-icon-114x114-precomposed.png"/>
<!-- Retina iPhone 和 Retina iTouch，114x114 像素，可以没有，但推荐有 -->
<link rel="apple-touch-icon-precomposed" sizes="144x144"
    href="/apple-touch-icon-144x144-precomposed.png"/>
<!-- Retina iPad，144x144 像素，可以没有，但推荐有 -->
<!-- iOS 图标 end -->
```

```html
<!-- iOS 启动画面 begin -->
<link rel="apple-touch-startup-image" sizes="768x1004" href="/splash-screen-768x1004.png"/>
<!-- iPad 竖屏 768 x 1004（标准分辨率） -->
<link rel="apple-touch-startup-image" sizes="1536x2008" href="/splash-screen-1536x2008.png"/>
<!-- iPad 竖屏 1536x2008（Retina） -->
<link rel="apple-touch-startup-image" sizes="1024x748" href="/Default-Portrait-1024x748.png"/>
<!-- iPad 横屏 1024x748（标准分辨率） -->
<link rel="apple-touch-startup-image" sizes="2048x1496" href="/splash-screen-2048x1496.png"/>
<!-- iPad 横屏 2048x1496（Retina） -->
<link rel="apple-touch-startup-image" href="/splash-screen-320x480.png"/>
<!-- iPhone/iPod Touch 竖屏 320x480 (标准分辨率) -->
<link rel="apple-touch-startup-image" sizes="640x960" href="/splash-screen-640x960.png"/>
<!-- iPhone/iPod Touch 竖屏 640x960 (Retina) -->
<link rel="apple-touch-startup-image" sizes="640x1136" href="/splash-screen-640x1136.png"/>
<!-- iPhone 5/iPod Touch 5 竖屏 640x1136 (Retina) -->
<!-- iOS 启动画面 end -->
```

* **其他**

```html
<!-- 不让百度转码 -->
<meta http-equiv="Cache-Control" content="no-siteapp" />
<!-- 针对手持设备优化，主要是针对一些老的不识别viewport的浏览器，比如黑莓 -->
<meta name="HandheldFriendly" content="true">
<!-- 微软的老式浏览器 -->
<meta name="MobileOptimized" content="320">
<!-- uc强制竖屏 -->
<meta name="screen-orientation" content="portrait">
<!-- QQ强制竖屏 -->
<meta name="x5-orientation" content="portrait">
<!-- UC强制全屏 -->
<meta name="full-screen" content="yes">
<!-- QQ强制全屏 -->
<meta name="x5-fullscreen" content="true">
<!-- UC应用模式 -->
<meta name="browsermode" content="application">
<!-- QQ应用模式 -->
<meta name="x5-page-mode" content="app">
<!-- windows phone 点击无高光 -->
<meta name="msapplication-tap-highlight" content="no">
```

```html
<meta name="msapplication-TileColor" content="#000"/>
<!-- Windows 8 磁贴颜色 -->
<meta name="msapplication-TileImage" content="icon.png"/>
<!-- Windows 8 磁贴图标 -->

<link rel="alternate" type="application/rss+xml" title="RSS" href="/rss.xml"/>
<!-- 添加 RSS 订阅 -->
<link rel="shortcut icon" type="image/ico" href="/favicon.ico"/>
<!-- 添加 favicon icon -->

<!-- sns 社交标签 begin -->
<!-- 参考微博API -->
<meta property="og:type" content="类型" />
<meta property="og:url" content="URL地址" />
<meta property="og:title" content="标题" />
<meta property="og:image" content="图片" />
<meta property="og:description" content="描述" />
<!-- sns 社交标签 end -->
```
