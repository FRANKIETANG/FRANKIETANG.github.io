---
title: CSS 学习思路
date: 2018-02-05 17:55:51
tags: 
- CSS
categories:
- CSS
description: 文科生们纷纷表示，我们 CSS 能吊打所有的理科生。
---

# CSS 学习思路

## CSS 是怎么来的

先想一个问题，怎么把一个页面的背景有颜色，并且有一个`<h1>`的标题并且居中，标题是红色。

![](https://i.loli.net/2018/02/05/5a78334dde02a.png)

在没有 CSS 的时候，HTML 是有自己的一套办法的。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body bgcolor="yellow">
  <h1><center><font color="red">标题</font></center></h1>
</body>
</html>
```

上面的 `bgcolor="yellow"` 、 `<center>` 和 `color="red"` 都是 HTML 的内置方法

这样内联写 CSS 不够美观，而且很难看。

那用 CSS 写的确是很方便，就像指哪打哪一样。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <style>
    body {
      background-color: yellow;
    }
    h1 {
      color: red;
      text-align: center;
    }
  </style>
</head>
<body>
  <h1>标题</h1>
</body>
</html>
```

做到一样的效果，但是逻辑更加清晰了。

当然这样写也不太好，CSS 写在 HTML 挤在一堆会看的眼疼的（想起大学在社团写的第一个页面，CSS 和 HTML 写在一起先写完 HTML 的标签，然后又滚上去 `<style>` 里面写 CSS ，体验真的很不友好 hhh）

解决办法也很明显： `<link>` 引入 CSS。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/2.10.0/github-markdown.css">
</head>
<body class="markdown-body">
  <h1>大标题</h1>
  <h2>小标题</h2>
  <ul>
    <li>项目1</li>
    <li>项目2</li>
    <li>项目3</li>
    <li>项目4</li>
  </ul>
</body>
</html>
```

在 `<link>` 也可以加上媒体查询

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/2.10.0/github-markdown.css" media="print">
<!-- 打印的时候使用 github-markdown-css -->
```

打印前的普通样子

![](https://i.loli.net/2018/01/22/5a65d1066e4a6.png)

按上打印之后自动加上样式

![](https://i.loli.net/2018/01/22/5a65d1068bd8e.png)

## CSS 为什么难学

因为效果基本靠抄（像我这种半吊子，直接就上 codepen.io 一搜一抄就好），抄完就不管了（肯定有很多人想我这样...），要么就用现成的（Bootstrap / elementUI）。结果就像现在这样只会 JS 不会 CSS 。

CSS经常会有很多地方冲突，举几个例子：

- 各属性之间互相影响

  - margin & border

    先看看这个例子

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .demo1 {
          border: 1px solid red;
          height: 100px;
          margin: 10px;
        }
      </style>
    </head>
    <body>
      <div class="demo1"></div>
      <div style="border-top: 0.1px solid green"></div>
      <div class="demo1"></div>
      <div class="demo1"></div>
    </body>
    </html>
    ```

    可以看到下面两个 div 盒子之间的 margin 是合在一起的（外边距合并），而上两个盒子之间加一个盒子加上 border 浏览器就会以为多了一个盒子。（其实我觉得这个也不难理解，因为中间这个盒子如果不加 border 加文本也会变成一个盒子，上下自动添加 margin 。）

    ![](https://i.loli.net/2018/02/05/5a78274a82102.png)

    但是特别的东西来了，看看下面这个代码。

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .demo1 {
          border: 1px solid red;
          height: 100px;
          margin: 10px;
        }
      </style>
    </head>
    <body>
      <div class="demo1"></div>
      <div style="display: table;"></div>
      <div class="demo1"></div>
      <div style="display: inline;"></div>
      <div class="demo1"></div>
      <div style="display:flex;"></div>
      <div class="demo1"></div>
    </body>
    </html>
    ```

    这个 `display:table;` 居然可以被当成是一个盒子（而 `display: inline;` 不能当成盒子， `display:flex;` 又可以当成盒子。）

    ![](https://i.loli.net/2018/02/05/5a7827a92d106.png)

    所以从这些例子可以看出只要加了 border 就会影响到 margin，而且经过上面的这些实验也发现不止 border 会有影响，像 display 的某些属性也会影响到 margin 。

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent {
          border-top: 1px solid green; /*这一句可以删掉看看效果*/
          background-color: yellow;
        }
        
        .child {
          height: 100px;
          border: 1px solid red;
          margin-top: 100px;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child"></div>
      </div>
    </body>
    </html>
    ```

    ![](https://i.loli.net/2018/02/05/5a7827e64cbff.png)

    可以影响到 margin 的属性其实还有很多，可以一个一个去试试。

  - 小圆点 & display

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        li {
          display: block;
        }
        
    /*     li {
          display: list-item;
        } */
        
    /*     li {
          display: inline;
        } */
      </style>
    </head>
    <body>
      <ul>
        <li>item1</li>
        <li>item2</li>
        <li>item3</li>
      </ul>
    </body>
    </html>
    ```

    ​![](https://i.loli.net/2018/02/05/5a78289883969.png)

    对 li 设置 display 的其他属性会覆盖掉 li 的原生 CSS `display: list-item` （我猜的）。这个很难理解只能死背。

    position: absolute & display: inline

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent {
          background: yellow;
          height: 100px;
          position: relative;
        }
        
        .child {
          display: inline;
          border: 1px solid red;
          position: absolute;
          bottom: 0;
          right: 0;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child">内联样式</div>
      </div>
    </body>
    </html>
    ```

    这里的主要问题是 `display: inline` 在 `position: absolute` 的影响下竟然变成了 `display: block` 。

    ![](https://i.loli.net/2018/01/27/5a6b53426c155.png)

- 各元素之间互相影响

  - position: fixed & transform

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent {
          background: yellow;
          height: 100px;
          position: relative;
          transform: scale(0.9); /*注意这里*/
        }
        
        /*脑补很多代码*/
        .xxxx{}
        .xxxx{}
        .xxxx{}
        .xxxx{}
        
        .child {
          display: inline;
          border: 1px solid red;
          position: fixed; /*注意这里*/
          bottom: 0;
          left: 0;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child">内联样式</div>
      </div>
    </body>
    </html>
    ```

    这个就很明显了，用了 `position: fixed` 那 child 的 div 应该是在左下角，但是加了 `transform: scale(0.9)` 就变成了想绝对定位的东西，这个的确是挺难理解的。

    ​![](https://i.loli.net/2018/02/05/5a7829070fb1d.png)

  - float 影响 inline 元素

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent {
          background: yellow;
          height: 100px;
        }
        .float {
          background: rgba(255,0,0,0.5);
          width: 100px;
          height: 60px;
          float: left;
        }
        .child {
          width: 300px;
          height: 50px;
          background: white
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="float">浮动</div>
        <div class="child">我是文字</div>
      </div>
    </body>
    </html>
    ```

    ​![](https://i.loli.net/2018/02/05/5a78295836c40.png)

    为什么浮动不会影响 child 里面的文字呢？这个也是很难理解的。

虽然方老师说 CSS 很难理解，但是对于文科出身的我其实没事么难度（倒是 JS 挺难学的...）。

## CSS 的套路

但是应付平时工作的话只用记点套路就好了，常用的东西来来去去就那么点东西。

- 套路

  - 布局（指的是两栏三栏布局）

    可以分 PC 端和 Mobile 端。而 PC 端分为 IE8 和 chrome，IE8 用 Float 布局，chrome 和 Mobile 端用 Flex 布局就好。

    Float 布局

    两栏

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
       .c {
         width: 960px;
         margin: 0 auto;
       }
       .l {
         float: left;
         width: 280px;
         height: 500px;
         background-color: #f1f1f1;
         box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
       }
       .r {
         float: left;
         width: 630px;
         height: 1000px;
         margin-left: 50px;
         background-color: #f1f1f1;
         box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
       } 
      </style>
    </head>
    <body>
      <div class="c">
        <div class="l">1111</div>
        <div class="r">2222</div>
      </div>
    </body>
    </html>
    ```

    三栏

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
         .c {
           width: 960px;
           margin: 0 auto;
         }
        .l {
          float: left;
          width: 200px;
          height: 700px;
          background-color: #f1f1f1;
          box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
        }
        .m {
          float: left;
          width: 500px;
          height: 1000px;
          margin-left: 30px;
          background-color: #f1f1f1;
          box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
        }
        .r {
          float: left;
          width: 200px;
          height: 500px;
          margin-left: 30px;
          background-color: #f1f1f1;
          box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
        }
      </style>
    </head>
    <body>
      <div class="c">
        <div class="l">1111</div>
        <div class="m">3333</div>
        <div class="r">2222</div>
      </div>
    </body>
    </html>
    ```

    Flex 布局

    两栏

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
         .c {
           width: 960px;
           margin: 0 auto;
           display: flex;
           flex-flow: row;
         }  
         .l {
           width: 280px;
           height: 500px;
           background-color: #f1f1f1;
           box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
         }
         .r {
           flex: 1;
           height: 1000px;
           margin-left: 50px;
           background-color: #f1f1f1;
           box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
         }    
      </style>
    </head>
    <body>
      <div class="c">
        <div class="l">1111</div>
        <div class="r">2222</div>
      </div>
    </body>
    </html>
    ```

    三栏

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
         .c {
           width: 960px;
           margin: 0 auto;
           display: flex;
           flex-flow: row;
         } 
        .l {
          width: 200px;
          height: 700px;
          background-color: #f1f1f1;
          box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
        }
        .m {
          flex: 0.7;
          height: 1000px;
          margin-left: 30px;
          background-color: #f1f1f1;
          box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
        }
        .r {
          flex: 0.3;
          height: 500px;
          margin-left: 30px;
          background-color: #f1f1f1;
          box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.16), 0 2px 10px 0 rgba(0, 0, 0, 0.12)!important;
        }
      </style>
    </head>
    <body>
      <div class="c">
        <div class="l">1111</div>
        <div class="m">3333</div>
        <div class="r">2222</div>
      </div>
    </body>
    </html>
    ```

  - 水平居中

    子元素宽度不确定（ `margin-left` 和 `margin-right` 要计算）

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .child{
          margin-left: 20px;
          margin-right: 20px;
          background: red;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child">加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试</div>
      </div>
    </body>
    </html>
    ```

    子元素 300px 的宽度

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .child{
          margin-left: auto;
          margin-right: auto;
          width: 300px;
          height: 100px;
          background: red;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child"></div>
      </div>
    </body>
    </html>
    ```

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent{
          text-align: center;
        }
        .child{
          display: inline-block;
          width: 300px;
          height: 100px;
          background: red;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child"></div>
      </div>
    </body>
    </html>
    ```

  - 垂直居中

    子元素高度确定

    ````html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent{
          border: 1px solid black;
          padding-top: 20px;
          padding-bottom: 20px;
        }
        .child{
          margin-left: auto;
          margin-right: auto;
          width: 300px;
          height: 100px;
          background: red;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child"></div>
      </div>
    </body>
    </html>
    ````

    子元素高度不确定

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent{
          border: 1px solid black;
          padding-top: 20px;
          padding-bottom: 20px;
        }
        .child{
          margin-left: auto;
          margin-right: auto;
          width: 300px;
          background: red;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child">加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试加字试试</div>
      </div>
    </body>
    </html>
    ```

    父元素高度确定（烂代码，尽量避免）

    兼容 IE8

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent{
          display: table-cell;
          vertical-align: middle;
          height: 500px;
          border: 1px solid black;
        }
        .child{
          margin: 100px;
          width: 300px;
          height: 100px;
          background: red;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child"></div>
      </div>
    </body>
    </html>
    ```

    其他用 Flex

    ```html
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8">
      <meta name="viewport" content="width=device-width">
      <title>JS Bin</title>
      <style>
        .parent{
          display: flex;
          align-items: center;
          border: 1px solid black;
          height: 500px;
        }
        .child{
          margin-left: auto;
          margin-right: auto;
          width: 300px;
          height: 100px;
          background: red;
        }
      </style>
    </head>
    <body>
      <div class="parent">
        <div class="child"></div>
      </div>
    </body>
    </html>
    ```

- 工具

  - CSS 3 Generator

    ![](https://i.loli.net/2018/01/28/5a6cb8c168f11.png)

    随便点开一个就好，这里就不细说了。

## CSS 资料

http://cndevdocs.com/

CSS 实际上是性价比很低的一个东西，大多数公司不需要 CSS 那么厉害的前端。