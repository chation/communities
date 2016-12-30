# communities

一个简单的,响应式的互动社区页面结构,用于学习Bootstrap框架

2016-12-30:添加了个人信息栏,广告栏

2016-12-29:添加了评论框,粉丝框

2016-12-28:添加了显示二维码,用户照片滚动播放

# about responsive

##Bootstrap
“Bootstrap 包含了一个响应式的、移动设备优先的、不固定的网格系统，可以随着设备或视口大小的增加而适当地扩展到 12 列。它包含了用于简单的布局选项的预定义类，也包含了用于生成更多语义布局的功能强大的混合类。”
###Bootstrap响应式开发
让我们来理解一下上面的语句。Bootstrap 3 是移动设备优先的，在这个意义上，Bootstrap 代码从小屏幕设备（比如移动设备、平板电脑）开始，然后扩展到大屏幕设备（比如笔记本电脑、台式电脑）上的组件和网格。
移动设备优先策略

    内容

        决定什么是最重要的。

    布局

        优先设计更小的宽度。

        基础的 CSS 是移动设备优先，媒体查询是针对于平板电脑、台式电脑。

    渐进增强

        随着屏幕大小的增加而添加元素。

响应式网格系统随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。

![这里写图片描述](http://img.blog.csdn.net/20161227192626863?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

###响应式工具
为了加快对移动设备友好的页面开发工作，利用媒体查询功能并使用这些工具类可以方便的针对不同设备展示或隐藏页面内容。另外还包含了针对打印机显示或隐藏内容的工具类。

有针对性的使用这类工具类，从而避免为同一个网站创建完全不同的版本。相反，通过使用这些工具类可以在不同设备上提供不同的展现形式。
####可用的类
通过单独或联合使用以下列出的类，可以针对不同屏幕尺寸隐藏或显示页面内容。

![这里写图片描述](http://img.blog.csdn.net/20161227193002609?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

通过了解以上的文档和理解响应式开发工具，我们便可以开始进行我们的开发实例，构建一个响应式的网页完成后如下：

![这里写图片描述](http://img.blog.csdn.net/20161227193251813?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

我们可以看到这个页面有五个部分
1.顶部导航栏
2.左侧信息栏
3.中间网页主体
4.右侧信息栏
5.右边恻导航栏

通过分析网站布局，我们可以拟定这样一个HTML结构：
```html
<!DOCTYPE html>
<html>
<body>
<div class="navbar navbar-fixed-top navbar-default" role="navigation">
</div>
<div class="container">
	<div class="row">
		<div class="col-md-3 col-sm-4">
		</div>
		<div class="col-md-6 col-sm-8">
		</div>
		<div class="col-md-3 hidden-sm hidden-xs">
		</div>
	</div>
</div>
<div class="rightNav">
</div>
</body>
</html>
```
好了，上面的结构已经搭建好了。解释一下上面的几个div类:

首先是顶部导航栏，使用了.navbar初始化导航栏 .navbar-fixed-top将导航栏锁定到顶部 .navbar-default导航栏默认样式

其次,初始化一个响应式框架,.container在这个div里面添加一个.row的div,用来调整布局,这个.row的类里面放置三个网页主体模块左中右,这里在浏览器窗口都是大于md的时候中间占容器的一半,左右两个div分别占剩下的一半,当浏览器的窗口小于sm的时候隐藏右侧栏,并加宽中间的主窗口.

最后,添加一个右侧导航栏

这样,我们就能初步实现在不同尺寸的设备上产生不同的效果了.

![这里写图片描述](http://img.blog.csdn.net/20161227195955964?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

##让页面更加实用
###右侧导航栏
我们设计的右侧导航栏的HTML代码如下:
```html
<div id="bottomNav" class="bottom-tools" style="top: 600px; width: 67px;height:100%;visibility: hidden">
    <div id="btn-nav" class="btn-group-vertical">
        <div title="联系我们"><span class="icon-phone"></span></div>
        <a href="https://github.com/chation" target="_blank">
            <div title="访问在GitHub上的主页"><span class="icon-github-alt"></span></div>
        </a>
        <div title="扫一扫"><span class="glyphicon glyphicon-qrcode"></span></div>
        <a style="visibility: hidden" id="sToTop">
            <div title="返回顶部"><span class="icon-angle-up"></span></div>
        </a>
    </div>
</div>
```
需求:
1.随窗口大小改变而改变位置,始终在屏幕可见的地方,并在右侧
2.当使用者向下滑动页面后才会显示返回顶部按钮,在顶部时不显示

随之,我们编写js代码:
```javascript
/* 设置导航栏的偏移量 */
function navPosition() {
    var windowHeight = window.screen.availHeight;
    var windowWidth = document.body.clientWidth;
    var divMainWidth = document.getElementById("divMain").clientWidth;
    var navWidth = Math.ceil((windowWidth - divMainWidth) / 2 + divMainWidth) + "px";
    var navHeight = windowHeight - Math.ceil(windowHeight / 2);
    var nav = document.getElementById("bottomNav");

    if ((windowWidth - divMainWidth) < 67) {
        nav.style.left = (document.body.clientWidth - 66) + "px";
        nav.style.top = navHeight + "px";
        nav.style.display = "block";
        nav.style.visibility = "";
    } else {
        nav.style.left = navWidth;
        nav.style.top = navHeight + "px";
        nav.style.display = "block";
        nav.style.visibility = "";
    }
}

/* 窗口resize之后重新调用navPosition设置偏移量 */
function navPositionResize() {
    window.addEventListener("resize", navPosition, false);
}

window.addEventListener("scroll", function () { //判断是否显示返回顶部按钮
        var scrollTopElem = document.getElementById("sToTop");
        if ((document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop) > 225) {
            scrollTopElem.style.visibility = "";
        } else {
            scrollTopElem.style.visibility = "hidden";
        }
    }, false);
```
这里,讲解一下我的思路:

让这个导航栏在主div(也就是放左中右三个div的容器)的大小被浏览器窗口大小减去后的值小于我们导航栏的宽度67px时,就让导航栏贴近屏幕右边侧,反之,则让导航栏的左边贴近主div的右侧,这样显得更为美观.

其次,我让这个导航栏始终显示在页面二分之一的位置

最后,监听是否显示返回顶部按钮,代码如下:
```javascript
window.addEventListener("scroll", function () { //判断是否显示返回顶部按钮
   var scrollTopElem = document.getElementById("sToTop");
   if ((document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop) > 225) {
       scrollTopElem.style.visibility = "";
   } else {
       scrollTopElem.style.visibility = "hidden";
   }
}, false);
```

> 这里引用一下从博客园里看来的一段关于屏幕内容滑动的博文
> 1、各浏览器下 scrollTop的差异
IE6/7/8：
对于没有doctype声明的页面里可以使用  document.body.scrollTop 来获取 scrollTop高度 ；
对于有doctype声明的页面则可以使用 document.documentElement.scrollTop；
Safari:
safari 比较特别，有自己获取scrollTop的函数 ： window.pageYOffset ；
Firefox:
火狐等等相对标准些的浏览器就省心多了，直接用 document.documentElement.scrollTop ；
2、获取scrollTop值
完美的获取scrollTop 赋值短语 ：
var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;
通过这句赋值就能在任何情况下获得scrollTop 值。
仔细观察这句赋值，你发现啥了没？？
没错， 就是 window.pageYOffset  (Safari)   被放置在 || 的中间位置。
因为当 数字0 与 undefine 进行 或运算时，系统默认返回最后一个值。即或运算中 0 == undefine ;
当页面滚动条刚好在最顶端，即scrollTop值为 0 时。  IE 下 window.pageYOffset  (Safari) 返回为 undefine ，此时将window.pageYOffset  (Safari) 放在或运算最后面时， scrollTop 返回 undefine ,  undefine 用在接下去的运算就会报错咯。
而其他浏览器 无论 scrollTop 赋值或运算顺序如何都不会返回 undefine.  可以安全使用..
所以说到头还是IE的问题咯. 杯具…
精神有点恍惚，不知道有没有表达清楚。
不过最后总结出来这句实验过OK，大家放心使用；
var scrollTop = document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop;

###底部添加注册按钮
在前面介绍到,通过响应式开发工具,我们隐藏了部分"不重要的内容",为了使页面保持功能的完善,我们需要让注册的界面以另一种方式显示出来!

我们先添加一段HTML代码:
```html
<nav id="smallScreen-nav" class="navbar navbar-default navbar-fixed-bottom" role="navigation"
     style="visibility: hidden">
    <div class="row">
        <div style="padding-top: 8px" class="col-xs-6">
            <a href="#" class="btn btn-danger btn-block" role="button">注 册</a></div>
        <div style="padding-top: 8px" class="col-xs-6">
            <a href="#" class="btn btn-success btn-block" role="button">登 录</a></div>
    </div>
</nav>
```
这里,我们初始化一个底部导航栏,这个导航栏只有两个按钮,一个登陆,一个注册
我们继续添加js代码让他能在浏览器窗口小于指定大小的时候自动显示在底部~
```javascript
var bNav = document.getElementById("smallScreen-nav");
if (windowWidth < 973) {
        bNav.style.visibility = "";
    } else {
        bNav.style.visibility = "hidden";
    }
}
```
然后我们把它同上一个部分的js封装到一起,并作为window.addEventListener的参数函数传入进去

![这里写图片描述](http://img.blog.csdn.net/20161227210347541?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![这里写图片描述](http://img.blog.csdn.net/20161227210401291?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
![这里写图片描述](http://img.blog.csdn.net/20161227210422998?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

以上是添加了一系列效果之后的样式.

###滑动到顶部的动画效果
普通的滑动到顶部只是迅速跳转到网页顶部,而没有实现滑动的动画效果,
包括jquery的方法
```javascript
$('#elem').click(function(){
        $('html,body').animate({
            scrollTop: '0px'
        }, 500);
    });
```
这里虽然实现了动画效果,但是如果网页非常非常的长,那该怎么办,所以这里我决定让滑动效果看起来更加的平滑,让网页距顶部越远的时候一次滑动的越多,越近的时候越小.

首先,我们需要算出当前网页到顶部的距离,然后每次移动取它的百分之十,代码如下:
```javascript
function moveToTOP() {
    var dist = Math.ceil((document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop) / 10);
    //这里采用Math.ceil()表示向上取整,因为像素距px是没有小数的
    window.scrollBy(0, -dist);
    var scrollDelay = setTimeout('moveToTOP()', 10); //每0.01s,调用自身
    var sTop = document.documentElement.scrollTop + document.body.scrollTop;
    if (sTop === 0) {
        clearTimeout(scrollDelay);
    }
}
```
这样我们的网页返回顶部的效果就更加平滑了

![这里写图片描述](http://img.blog.csdn.net/20161227212108642?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvQ2hhdGlvbl85OQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

代码托管在GitHub :
https://github.com/chation/communities