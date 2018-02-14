---
title: Flex 布局
date: 2018-02-13 10:52:27
tags:
- CSS
categories:
- CSS
description: Flex 布局是一种比较简单的 CSS 布局，只用不用兼容 IE 就可以用上这个比较新的语法。吊打大部分假三年经验前端。
---

# Flex 布局

最简单，最省事的一种布局。

- 老子加 `display: flex;`
- 老子加 `justify-content: space-between;`

[实例代码](https://github.com/FRANKIETANG/Understanding-CSS/tree/master/example/flex)

## Flex 前的布局

http://www.mycelly.com/

这个是那个年代常用的 12 种布局。

![](https://i.loli.net/2018/02/09/5a7d7b8c9ac5d.png)

不管你是写什么样子的页面，始终离不开

- normal flow
- float + clear
- position relative + absolute
- display inline-block
- 负 margin 

## Flex 布局

- 块级布局侧重垂直方向、行内布局侧重水平方向、Flex 布局是与方向无关的。
- Flex 布局可以实现空间自动分配、自动对齐。
- Flex 适用于简单的线性布局、更复杂的布局要交给 grid 布局。

基本概念

![](https://i.loli.net/2018/02/11/5a801ec80a24b.png)

下面举一个简单的例子

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      width: 100px;
      height: 50px;
      background: white;
      margin: 10px;
    }

    .parent {
      display: flex;
      background: #ddd;
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
  </div>
</body>

</html>
```

长这样。

![](https://i.loli.net/2018/02/11/5a8023b14ad12.png)

只要加上了 `display: flex;` 就会有类似 `float: left;` 的效果。

### flex container 的属性

| flex container 的属性 | 意思               |
| ------------------ | ---------------- |
| `flex-direction`   | 方向               |
| `flex-wrap`        | 换行               |
| `flex-flow`        | 上面两个的简写          |
| `justify-content`  | 主轴方向对齐方式         |
| `align-items`      | 侧轴对齐方式           |
| `align-content`    | 多行、列内容对齐方式（用得较少） |

先看看 `flex-direction` 的四个例子。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      width: 100px;
      height: 50px;
      background: white;
      margin: 10px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
      flex-direction: row;
    }

    .parent2 {
      display: flex;
      background: #ddd;
      flex-direction: row-reverse;
    }

    .parent3 {
      display: flex;
      background: #ddd;
      flex-direction: column;
    }

    .parent4 {
      display: flex;
      background: #ddd;
      flex-direction: column-reverse;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child3">3</div>
    <div class="child child4">4</div>
    <div class="child child5">5</div>
  </div>

  <div class="parent parent2">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child2">3</div>
    <div class="child child2">4</div>
    <div class="child child2">5</div>
  </div>

  <div class="parent parent3">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child2">3</div>
    <div class="child child2">4</div>
    <div class="child child2">5</div>
  </div>

  <div class="parent parent4">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child2">3</div>
    <div class="child child2">4</div>
    <div class="child child2">5</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a802bcfea8e4.png)

可以发现如果一个`<div>` 里有多个 `<div>` 那都会挤在一行，而 `flex-wrap` 可以解决这个问题。

```HTML
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      width: 100px;
      height: 50px;
      background: white;
      margin: 10px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
      flex-direction: row;
      flex-wrap: wrap;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child3">3</div>
    <div class="child child4">4</div>
    <div class="child child5">5</div>
    <div class="child child6">6</div>
    <div class="child child7">7</div>
    <div class="child child8">8</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a8030a400c50.gif)

这两个属性合在一起就是 `flex-flow: row wrap;` ，可以合在一起写。

`justify-content` 就是主轴方向对齐方式，这个也很好理解。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      width: 100px;
      height: 50px;
      background: white;
      margin: 10px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
      flex-flow: row nowrap;
      justify-content: space-between;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child3">3</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a803d832da06.gif)

`align-items` 字面意思就是把子元素对齐。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      width: 100px;
      background: white;
      margin: 10px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
      flex-flow: row nowrap;
      justify-content: space-around;
      align-items: center;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">1
      <br>1
      <br>1
      <br>1
      <br>1
      <br>
    </div>
    <div class="child child2">2
      <br>2
      <br>2
      <br>
    </div>
    <div class="child child3">3</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a804854b247f.gif)

这个动画里其实默认是 `align-items: stretch;` 。

`align-content` 用的比较少，了解就好。这个是用来控制行与行的空隙的。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      width: 100px;
      background: white;
      margin: 5px;
      height: 70px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
      flex-flow: row wrap;
      height: 400px;
      align-content: space-between;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child3">3</div>
    <div class="child child4">4</div>
    <div class="child child5">5</div>
    <div class="child child6">6</div>
    <div class="child child7">7</div>
    <div class="child child8">8</div>
    <div class="child child9">9</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a804ac74cafd.gif)

### flex item 的属性

| flex item 的属性 | 意思          |
| ------------- | ----------- |
| `flex-grow`   | 增长比例（空间过多）  |
| `flex-shrink` | 收缩比例（空间不够时） |
| `flex-basis`  | 默认大小（一般不用）  |
| `flex`        | 上面是三个的缩写    |
| `order`       | 顺序（代替双飞翼）   |
| `align-self`  | 自身的对齐方式     |

`flex-grow` 就是按比例分配，但是是按行算。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      background: white;
      margin: 5px;
      height: 70px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
    }

    .child:nth-child(1) {
      flex-grow: 2;
    }

    .child:nth-child(2) {
      flex-grow: 1;
    }

    .child:nth-child(3) {
      flex-grow: 3;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">213472819371</div>
    <div class="child child2">273821973981</div>
    <div class="child child3">218973482112</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a804fa712de8.gif)

`flex-shrink` 很少用，了解就好。

![](https://i.loli.net/2018/02/11/5a8053b6dec59.gif)

`flex-basis` 设置原始大小，也很少用。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      background: white;
      margin: 5px;
      height: 70px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
    }

    .child:nth-child(1) {
      flex-basis: 300px;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">2134728 1 9371</div>
    <div class="child child2">27382 197 3981</div>
    <div class="child child3">21897 348 2112</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a80545e1ba18.gif)

`flex` 就不举例子了，也就上面三个功能合在一起写的样子。

`order` 可以改变顺序。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      background: white;
      margin: 5px;
      height: 70px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
    }

    .child:nth-child(1) {
      flex-grow: 2;
      order: 3;
    }

    .child:nth-child(2) {
      flex-grow: 1;
      order: 2;
    }

    .child:nth-child(3) {
      flex-grow: 3;
      order: 1;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">1</div>
    <div class="child child2">2</div>
    <div class="child child3">3</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a805ac03b379.png)

`align-self` 控制单个子元素。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    .child {
      background: white;
      margin: 5px;
      width: 100px;
    }

    .parent {
      margin-top: 10px;
    }

    .parent1 {
      display: flex;
      background: #ddd;
      justify-content: space-around;
      align-items: flex-start;
    }

    .child:nth-child(3) {
      align-self: center;
    }
  </style>
</head>

<body>
  <div class="parent parent1">
    <div class="child child1">11111
      <br>1111
      <br>111
      <br>11
      <br>1
      <br>
    </div>
    <div class="child child2">222
      <br>22
      <br>2
      <br>
    </div>
    <div class="child child3">3</div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a805c3b812de.gif)

## 怎么用 Flex 布局写点东西

### 手机页面布局（torbar + main + tabs）

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
      box-sizing: border-box;
    }

    ul {
      list-style: none;
    }

    .container {
      height: 100vh;
      display: flex;
      flex-direction: column;
    }

    header {
      height: 100px;
      background: green;
    }

    footer ul {
      height: 100px;
      background: yellow;
    }

    main {
      flex-grow: 1;
      overflow: auto;
    }

    footer>ul {
      display: flex;
    }

    footer>ul>li {
      background: red;
      width: 25%;
      height: 100%;
      border: 1px solid black;
    }
  </style>
</head>

<body>
  <div class="container">
    <header>header</header>
    <main>
		<!--很多字-->
    </main>
    <footer>
      <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </footer>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a8060acdbd59.gif)

### 产品列表（ul>li*9）

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
      box-sizing: border-box;
    }

    ul {
      list-style: none;
    }

    ul {
      display: flex;
      flex-wrap: wrap;
      width: 350px;
      margin: auto;
      border: 1px solid black;
      justify-content: space-between;
    }

    li {
      width: 100px;
      height: 100px;
      background: #ddd;
      border: 1px solid red;
      margin: 10px 0;
    }
  </style>
</head>

<body>
  <ul>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
</body>

</html>
```

![](https://i.loli.net/2018/02/11/5a806274eb231.png)

### PC 页面布局

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    header {
      height: 50px;
      background: #ddd;
    }

    footer {
      height: 50px;
      background: #ddd;
    }

    .content {
      display: flex;
    }

    .content>#aside1 {
      width: 120px;
      background: #444;
    }

    .content>main {
      height: 400px;
      flex: 1;
      background: red;
    }

    .content>#aside2 {
      width: 100px;
      background: green;
    }
  </style>
</head>

<body>
  <header></header>
  <div class="content">
    <aside id="aside1"></aside>
    <main></main>
    <aside id="aside2"></aside>
  </div>
  <footer></footer>
</body>

</html>
```

![](https://i.loli.net/2018/02/12/5a806ac17b8aa.png)

### 完美居中

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
      height: 400px;
      background: #ddd;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .child {
      border: 1px solid red;
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child">
      abcdefg
    </div>
  </div>
</body>

</html>
```

![](https://i.loli.net/2018/02/12/5a806becb5643.png)

## 另一种布局 Gird 布局

同时也是另一种布局，没用过但可以了解一下。

[网格布局 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Grid_Layout)

[网格布局的基本概念 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)

[CSS 网格布局学习指南](http://blog.jirengu.com/?p=990)