---
title: icon 的 N 种搞法
date: 2018-02-11 23:36:15
tags:
- CSS
categories:
- CSS
description: 好的 icon 决定了页面看起来舒不舒服。
---

# icon 的 N 种搞法

icon 是怎么搞出来的。

[示例代码](https://github.com/FRANKIETANG/Understanding-CSS/tree/master/example/icon)

## img 搞法

黑话叫切图。

在 [iconfont](http://www.iconfont.cn) 把微信微博 QQ 的 icon 下载为 PNG 格式。 

放到 GIMP 那里对齐成这样，保存。

![](https://i.loli.net/2018/02/05/5a785b9d4b75a.png)

值得注意的是 GIMP 要保存成 `.xcf` 格式，Photoshop 保存成 `.psd` 格式。

或者 Export 成 PNG 格式。

如果是 `.xcf` 裁剪单独 icon 操作如下。

![](https://i.loli.net/2018/02/06/5a791bbcb14f3.gif)

不过我个人更倾向于把所有 icon 放在一起。

把所有 icon 做成下面这个样子。

![](https://i.loli.net/2018/02/06/5a793e7673e68.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .box {
      float: left;
      position: relative;
      left: 50%;
    }

    .clearfix {
      zoom: 1;
    }

    .clearfix::after {
      content: '';
      clear: both;
      visibility: hidden;
    }

    .icons {
      width: 100px;
      height: 100px;
      overflow: hidden;
    }

    .box div {
      float: left;
      margin: 0 10px;
      position: relative;
      right: 50%;
    }

    .qq img {
      position: relative;
      right: 0px;
    }

    .weixin img {
      position: relative;
      right: 400px;
    }

    .weibo img {
      position: relative;
      right: 200px;
    }
  </style>
</head>

<body>
  <div class="box clearfix">
    <div class="icons qq">
      <img src="./xxx.png" alt="qq">
    </div>
    <div class="icons weixin">
      <img src="./xxx.png" alt="weixin">
    </div>
    <div class="icons weibo">
      <img src="./xxx.png" alt="weibo">
    </div>
  </div>
</body>

</html>
```

反正我是很不喜欢切图的，还不如直接用 icon 来的快。

因为 GIMP 切出来的图有点问题，我直接切成雪碧图了

## 背景流搞法

就是利用背景图来做 icon，优点嘛，就是不受 div 影响，不会拉伸啥的。利用 `background-position` 来移位置。

![](https://i.loli.net/2018/02/06/5a79820048055.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .box {
      text-align: center;
    }

    .icons .icon-qq {
      margin: 5px 25px;
      border: 1px solid red;
      display: inline-block;
      width: 100px;
      height: 100px;
      background: transparent url('./img/xxx.png') no-repeat;
      background-position: 0px 0px;
    }

    .icons .icon-weibo {
      margin: 5px 25px;
      border: 1px solid red;
      display: inline-block;
      width: 100px;
      height: 100px;
      background: transparent url('./img/xxx.png') no-repeat;
      background-position: -200px 0px;
    }

    .icons .icon-weixin {
      margin: 5px 25px;
      border: 1px solid red;
      display: inline-block;
      width: 100px;
      height: 100px;
      background: transparent url('./img/xxx.png') no-repeat;
      background-position: -400px 0px;
    }
  </style>
</head>

<body>
  <div class="box icons">
    <div class="icon-qq"></div>
    <div class="icon-weibo"></div>
    <div class="icon-weixin"></div>
  </div>
</body>

</html>
```

其实雪碧图不一定要用 Photoshop 或者 GIMP 来切，通常上会有 CSS Sprites Generator 或者用 CSS Sprites cli 。基本上 Google 一大堆教程，只要不是傻子很快就能学会的。

## iconfont 搞法

用 iconfont 整三个图标添加到项目去

![](https://i.loli.net/2018/02/06/5a7998fbb09bd.png)

点击生成在线链接，然后引入。

![](https://i.loli.net/2018/02/06/5a799ac31c150.png)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    @font-face {
      font-family: 'iconfont';
      /* project id 565963 */
      src: url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.eot');
      src: url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.eot?#iefix') format('embedded-opentype'),
      url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.woff') format('woff'),
      url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.ttf') format('truetype'),
      url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.svg#iconfont') format('svg');
    }

    .icons {
      font-family: iconfont;
    }
  </style>
</head>

<body>
  <div class="icons">
    &#xe622;&#xe623;&#xe655;
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/06/5a799b924154d.png)

当然也可以用 CSS 引入。（注意的是 `&#xe622` 要换成 `\e622` ，因为 `&#x` 等于 `\`）

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    @font-face {
      font-family: 'iconfont';
      /* project id 565963 */
      src: url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.eot');
      src: url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.eot?#iefix') format('embedded-opentype'),
      url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.woff') format('woff'),
      url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.ttf') format('truetype'),
      url('//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.svg#iconfont') format('svg');
    }

    .icons {
      font-family: iconfont;
    }

    .xxx::before {
      content: '\e622';
    }

    .yyy::before {
      content: '\e623';
    }

    .zzz::before {
      content: '\e655';
    }
  </style>
</head>

<body>
  <div class="icons xxx"></div>
  <div class="icons yyy"></div>
  <div class="icons zzz"></div>
</body>

</html>
```

![](https://i.loli.net/2018/02/07/5a7a85a569cee.png)

下面来看看 CSS Font class 的写法。

这个的好处是，CSS icon 是一种字体，可以用 `font-size` 来调整字体。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <link rel="stylesheet" href="//at.alicdn.com/t/font_565963_8sd26i2z2ci0be29.css">
  <style>
    .iconfont {
      font-size: 100px;
      color: yellow;
    }
  </style>
</head>

<body>
  <span class="iconfont icon-weixin"></span>
  <span class="iconfont icon-qq"></span>
  <span class="iconfont icon-weibo"></span>
</body>

</html>
```

![](https://i.loli.net/2018/02/07/5a7a8c80e01c1.png)

还有一种使用 JS 来引入 icon，是这样的。（实际上就是 SVG ）

在 iconfont 里基本上有颜色的图标都是 SVG。

![](https://i.loli.net/2018/02/07/5a7a9163bd0df.png)

可以打开那个 JS 文件，可以发现是用 JS 写 SVG。而且引入这个 JS 文件可以发现 SVG 已经躺在 HTML 页面里了。

![](https://i.loli.net/2018/02/07/5a7a9243eed3b.png)

按照文档就可以愉快的使用了。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="//at.alicdn.com/t/font_566506_su1rg4kx92ne9udi.js"></script>
  <style type="text/css">
    .icon {
      width: 1em;
      height: 1em;
      vertical-align: -0.15em;
      fill: currentColor;
      overflow: hidden;
    }
  </style>
</head>

<body>
  <svg style="width: 100px; height: 100px;" class="icon" aria-hidden="true">
    <use xlink:href="#icon-bianfu"></use>
  </svg>
  <svg class="icon" aria-hidden="true">
    <use xlink:href="#icon-bianselong"></use>
  </svg>
  <svg class="icon" aria-hidden="true">
    <use xlink:href="#icon-baitu"></use>
  </svg>
  <svg class="icon" aria-hidden="true">
    <use xlink:href="#icon-daxiang"></use>
  </svg>
</body>

</html>
```

![](https://i.loli.net/2018/02/07/5a7a954009f03.png)

而且如果是没用颜色的 icon（像上面的 QQ 微信微博），可以用 CSS 来改颜色或者描边（如 `fill: red;` 和 `stroke: black; stroke-width: 10px;`）

## 最后一种搞法：CSS 就是干

这种搞法比较高阶，通常新手是玩不来的。

[CSS ICON -- project by Wenting Zhang](http://cssicon.space/)

比如说画一个放大镜为例子

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .magnifier {
      display: inline-block;
      width: 20px;
      height: 20px;
      border: 1px solid red;
      border-radius: 50%;
      position: relative;
    }

    .magnifier::after {
      content: '';
      display: inline-block;
      width: 10px;
      border-top: 1px solid red;
      position: absolute;
      bottom: 0;
      left: 100%;
      transform: rotate(45deg);
      margin-left: -3px;
      margin-bottom: -1px;
    }
  </style>
</head>

<body>
  <span class="magnifier"></span>
</body>

</html>
```

![](https://i.loli.net/2018/02/07/5a7a9988b3ac7.png)

所以，万图皆可 CSS （笑）

所以可以参考一下 Wenting Zhang 的 icon 学一学。