---
title: 动态 REM
date: 2018-02-27 00:56:17
tags:
- CSS
categories:
- CSS
description: 利用 JavaScript 控制 CSS 来进行等比缩放，阿里的程序员想了好久才想到这种方法。
---

# 动态 REM

REM 是手机专用的自适应方案。（不是响应式，只针对手机，PC 端就会拒绝访问）

[示例代码](https://github.com/FRANKIETANG/Understanding-CSS/tree/master/example/rem)

## 什么是 REM

这里先来了解一下常用的长度单位。

px -> 像素。

em -> 一个 m 的长度。`em` == `font-size`（面试官：一斤鸭梨！明明是一个汉字的长度！）

rem -> root em 根元素的 font-size。（根元素就是 `<html>`，比如说 `<html>` 的根元素是 `16px`，那样 rem 就是 `16px` 。）

vh -> viewport height 视口高度，100vh == 视口高度。

vw -> viewport width 视口宽度，100vw == 视口宽度。

所以 em 和 rem 的关系和 JavaScript 和 Java 关系有一拼，也和雷锋和雷峰塔有一拼。

`<html>` 初始的 `font-size` 是 `16px` 。

举个例子：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .a {
      font-size: 1rem;
    }

    .b {
      font-size: 2rem;
    }

    .c {
      font-size: 3rem;
    }
  </style>
</head>

<body>
  <p class="a">123</p>
  <p class="b">456</p>
  <p class="c">789</p>
</body>

</html>
```

![](https://i.loli.net/2018/02/21/5a8d49e9704e9.png)

记住，字体大小和 `<html>` 的 `font-size` 很有关系。

## REM 和 EM 的区别是什么

em 的值是不固定的，是看父元素的 `font-size` 。（因为继承的原因父元素才会影响到 em 值）

建议不要用，很容易有奇奇怪怪的效果。

rem 就很好，什么都听根元素的话。

## 手机端方案的特点

还是要记住一点，有图才做。没图？怼他。

所以说第一点就是，要两张图。一张 PC 端，一张手机端。没有就响应个屁。

然后要确定页面要做多大。（收集市面上常用的手机屏幕有多大）

如果考虑响应式的话可能要对某些手机做适配。（0 - 320 一套 CSS / 321 - 375 一套 / 376 - 414 一套这样。其实挺麻烦。而且很容易让效果变怪，特别是用百分比做页面的时候。）

那手机端就有以下这几种写法：

- 百分比写法（高度有问题）
- 整体缩放

## 动态 REM 的写法

先看看一个百分比写法的例子：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    .child {
      background: #ddd;
      margin-top: 10px;
      margin-bottom: 10px;
      text-align: center;
    }

    .child {
      float: left;
      width: 40%;
      margin-left: 5%;
      margin-right: 5%;
    }

    .claerfix::after {
      content: '';
      display: block;
      clear: both;
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child">40%</div>
    <div class="child">40%</div>
    <div class="child">40%</div>
    <div class="child">40%</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/26/5a941debbda43.gif)

明显的一点就是，高度没有变。

接下来举一个缩放（就是 REM ）的例子：

有一个很重要的思路就是 1 rem == html font-size == viewport width

什么意思呢？就是让 html 的 font-size 和页面宽度有关系。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    * {
      margin: 0;
      padding: 0;
    }

    body {
      font-size: 16px;
      /* 不让字也变成 rem */
    }

    .child {
      background: #ddd;
      text-align: center;
      line-height: 0.2rem;
    }

    .child {
      width: 0.4rem;
      height: 0.2rem;
      margin: 0.05rem 0.05rem;
      float: left;
    }

    .clearfix::after {
      content: '';
      clear: both;
      display: block;
    }
  </style>
  <script>
    let pageWidth = window.innerWidth  // 获取页面宽度
    document.write(`
      <style>
        html {
          font-size: ${pageWidth}px;  /* 页面宽度等于 font-size */
        }
      </style>
    `)
  </script>
</head>

<body>
  <div class="parent">
    <div class="child">40%</div>
    <div class="child">40%</div>
    <div class="child">40%</div>
    <div class="child">40%</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/26/5a9429c5e7ef8.gif)

利用 JavaScript 控制 CSS 来进行等比缩放。

但是有一个问题啊，我能不能写 rem 的时候不用小数呢？

![](https://i.loli.net/2018/02/26/5a942b6d72ef9.png)

可以的，只用把 JavaScript 改一下。

```JavaScript
    let pageWidth = window.innerWidth  // 获取页面宽度
    document.write(`
      <style>
        html {
          font-size: ${pageWidth/10}px;  /* 页面宽度等于 font-size */
        }
      </style>
    `)
```

注意不能除 100 ，页面会错乱，因为浏览器内置最小字体大小是 `12px` 。

另外 REM 可以和其他单位同时存在。

```css
 font-size: 16px;
 border: 1px solid red;
 width: 0.5rem;
```

## 一些 REM 技巧：px 自动变成 rem

不需要用脑子算 rem，电脑帮忙算。

用 sass 写。

```shell
sudo gem install sass --no-user-install
```

然后用上 [PX2REM](https://github.com/imochen/luna/blob/master/root/src/px2rem.scss) 。

用 sass 翻译已经写好的 scss。

```shell
sass --watch scss:css
```

这样就能翻译成一模一样的的代码了。

![](https://i.loli.net/2018/02/27/5a943a79cb0ea.png)

重点是设计稿的宽度要写好，其他直接填就可以了。