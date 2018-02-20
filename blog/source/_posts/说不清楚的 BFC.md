---
title: 说不清楚的 BFC
date: 2018-02-20 22:53:19
tags:
- CSS
categories:
- CSS
description: BFC 只是一种 CSS 的实现方法，并不一定要用这种方法来写页面，因为写页面的方法千千万万。
---

# 说不清楚的 BFC

[CSS 规范中对 BFC 的描述](http://www.ayqy.net/doc/css2-1/visuren.html#block-formatting)

> 9.4.1 块格式化上下文
>
> 浮动，绝对定位元素，非块盒的块容器（例如，inline-blocks，table-cells和table-captions）和'overflow'不为'visible'的块盒会为它们的内容建立一个新的块格式化上下文
>
> 在一个块格式化上下文中，盒在竖直方向一个接一个地放置，从包含块的顶部开始。两个兄弟盒之间的竖直距离由'margin'属性决定。同一个块格式化上下文中的相邻块级盒之间的竖直margin会合并
>
> 在一个块格式化上下文中，每个盒的left外边（left outer edge）挨着包含块的left边（对于从右向左的格式化，right边挨着）。即使存在浮动（尽管一个盒的行盒可能会因为浮动收缩），这也成立。除非该盒建立了一个新的块格式化上下文（这种情况下，该盒自身可能会因为浮动变窄）

[MDN 对 BFC 的描述](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Block_formatting_context)

> 一个块格式化上下文（block formatting context） 是Web页面的可视化CSS渲染出的一部分。它是块级盒布局出现的区域，也是浮动层元素进行交互的区域。
>
> 一个块格式化上下文由以下之一创建：
>
> - 根元素或其它包含它的元素
> - 浮动元素 (元素的 float 不是 none)
> - 绝对定位元素 (元素具有 position 为 absolute 或 fixed)
> - 内联块 (元素具有 display: inline-block)
> - 表格单元格 (元素具有 display: table-cell，HTML表格单元格默认属性)
> - 表格标题 (元素具有 display: table-caption, HTML表格标题默认属性)
> - 具有overflow 且值不是 visible 的块元素，
> - display: flow-root
> - column-span: all 应当总是会创建一个新的格式化上下文，即便具有 column-span: all 的元素并不被包裹在一个多列容器中。
>
> 一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。
>
> 块格式化上下文对于定位 (参见 float) 与清除浮动 (参见 clear) 很重要。定位和清除浮动的样式规则只适用于处于同一块格式化上下文内的元素。浮动不会影响其它块格式化上下文中元素的布局，并且清除浮动只能清除同一块格式化上下文中在它前面的元素的浮动。

[张鑫旭对 BFC 的描述](http://www.zhangxinxu.com/wordpress/2015/02/css-deep-understand-flow-bfc-column-two-auto-layout/)

> BFC全称”Block Formatting Context”, 中文为“块级格式化上下文”。啪啦啪啦特性什么的，一言难尽，大家可以自行去查找，我这里不详述，免得乱了主次，总之，记住这么一句话：BFC元素特性表现原则就是，内部子元素再怎么翻江倒海，翻云覆雨都不会影响外部的元素。所以，避免margin穿透啊，清除浮动什么的也好理解了。

[实例代码](https://github.com/FRANKIETANG/Understanding-CSS/tree/master/example/bfc)

## 那 BFC 到底是什么

BFC 是一种方法。

实际上 BFC 只有两个功能：

- 爸爸管儿子
- 兄弟之间划清界限

### 爸爸管儿子

用 BFC 包住浮动元素。（注意不是清除浮动）

只要儿子加了浮动元素，爸爸的高度就会坍塌。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
    }

    .child {
      background: green;
      float: left;
      width: 300px;
      height: 100px;
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

![](https://i.loli.net/2018/02/20/5a8c0f2f8b567.png)

用 BFC 包住儿子有四种写法。

第一种是跟着儿子浮动。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      float: left;
    }

    .child {
      background: green;
      float: left;
      width: 300px;
      height: 100px;
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

![](https://i.loli.net/2018/02/20/5a8c17e0a8397.png)

第二种是父元素绝对定位。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      position: absolute;
    }

    .child {
      background: green;
      float: left;
      width: 300px;
      height: 100px;
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

效果和上面的一样，这里就不贴图了。

第三种是爸爸加 `display:inline-block`

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      display: inline-block;
    }

    .child {
      background: green;
      float: left;
      width: 300px;
      height: 100px;
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

效果和上面的一样，这里就不贴图了。

第四种是 `overflow` 不是 `visible` 的属性。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      overflow: auto;
    }

    .child {
      background: green;
      float: left;
      width: 300px;
      height: 100px;
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

![](https://i.loli.net/2018/02/20/5a8c1d0d23e8c.png)

这个空白不知道为什么，可能是因为 auto 的缘故吧。

第五种是 `display:table-cell`

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      display: table-cell;
    }

    .child {
      background: green;
      float: left;
      width: 300px;
      height: 100px;
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

![](https://i.loli.net/2018/02/20/5a8c17e0a8397.png)

第六种是 `display: flow-root`

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      display: flow-root;
    }

    .child {
      background: green;
      float: left;
      width: 300px;
      height: 100px;
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

![](https://i.loli.net/2018/02/20/5a8c1d0d23e8c.png)

和 `overflow: auto;` 一样的效果。

值得注意的是，**下面这种情况相邻块级盒之间的竖直 margin 会合并**。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      display: flow-root;
    }

    .child {
      background: green;
      width: 300px;
      height: 100px;
      margin: 10px;
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child"></div>
    <div class="child"></div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/20/5a8c23720f7d8.png)

还有一句话要记住的。

> 一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。

这是怎么意思呢？就是儿子的儿子不会被爸爸包住。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      border: 10px solid red;
      min-height: 10px;
      display: flow-root;
    }

    .child {
      float: left;
      background: green;
      width: 300px;
      height: 100px;
      margin-top: 100px;
    }
    
    .grandson {
      height: 50px;
      width: 200px;
      background: blue;
      margin-top: 200px;
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child">
      <div class="grandson"></div>
    </div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/20/5a8c2592dee71.png)

实际上只要儿子不要高度就能包起来，这里只是举个例子。

![](https://i.loli.net/2018/02/20/5a8c289e7cbc5.gif)

### 兄弟之间划清界限

用 float + div 做左右自适应布局

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .gege {
      width: 100px;
      min-height: 600px;
      border: 5px solid red;
      float: left;
      margin-right: 20px;
    }

    .didi {
      min-height: 600px;
      border: 10px solid green;
      overflow: auto;
    }
  </style>
</head>

<body>
  <div class="gege">gege</div>
  <div class="didi">1234</div>
</body>

</html>
```

![](https://i.loli.net/2018/02/20/5a8c3285948d8.gif)

## BFC 值得注意的地方

BFC 可以模拟清除浮动，但是建议还是用清除浮动，因为用 BFC 必须创造 BFC 的条件。（比如 overflow，天知道计算机会把样式搞成啥样子）

BFC 可以用在爸爸不让儿子出去的地方。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .parent {
      background: red;
      overflow: hidden;
    }

    .child {
      height: 100px;
      background: rgba(0, 255, 0, 0.5);
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

![](https://i.loli.net/2018/02/20/5a8c34946dcb0.gif)

不过还是建议用 `display: flow-root` ，副作用小。

实际上用 `border-top` 也可以做到。所以说没有什么必要用到 BFC。

面试才会问到 BFC。

- 千万别解释什么是 BFC，一解释就错。
- 用上面的例子回答什么是 BFC。