### 前言

年后回来上班，查看了一下自己的github,发现好久没有更新东西了，心里总觉得少了什么，所以整理了相关概念，决定来写这篇关于css flex布局介绍的文章，其目的主要有以下两点原因：一、年前用flex布局用得挺爽的，所以记录一下以便增加记忆；二、弥补自己好久没有更新github的心里空白。

当然了，写的不正确的地方，还望你带着“复杂”的心情阅读下，不胜感激！

### 概念介绍

首先我们需要理解一下什么flex布局！flex布局简单点来说就是通过设置css来建立一个容器，使得该容器拥有控制他的直接子元素拉伸、收缩的能力，从而能够在不同尺寸的屏幕上正确显示我们的内容。比如屏幕变宽时，子元素可以自适应边框来填充容器，亦或屏幕变窄时，子元素相应的收缩而不会产生溢出效果。说得再直接一点，flex布局是弹性的，它能自动根据屏幕宽窄来做相应尺寸调整。

还有一点需要注意，flex布局是与方向无关的，我们之前了解的float和定位布局都是基于方向流或者方向位置的有关的布局，而flex布局就是一个单独的模块，它通过直接控制子元素来实现相应的布局。并不是说基于方向的布局不好，只是某些情况下显得不是很灵活。

### 使用flex布局

在正式介绍如何使用flex布局之前，我们有必要强调一下，flex布局是一个独立的模块。所以我们使用它并不仅仅是设置某个属性而已，而是需要设置一系列属性来控制。这些属性有些设置container上，有些需要设置在item上。

此外我们需要整体来理解一下flex布局的container盒子，从而有一个形象的认识，看下图：

![flex布局架构图](https://cdn.css-tricks.com/wp-content/uploads/2011/08/flexbox.png)

如图所示，相关概念可以简单解释如下：

* **main axis**和**cross axis**分别控制着container里面item排列方向和对齐方式，打个比喻就好像小学语文练习本每个方格的横线和竖线一样，控制你写的内容如何排列，**main axis**就好比**横线**，而**cross axis**就好比**竖线**。
* **main-start | main-end**和**cross-start | cross-end**就是两条轴的两端位置，分别对应开始和结束。
* **main size**和**cross size**就是container容器的横向长度和竖向长度。

注：这里需要注意一点，**main axis**并不总是横向的那条轴，**cross axis**也不总是竖向的那条轴，这取决于container容器设置了怎样的flex-direction。但是可以确定一点**cross axis**是**main axis**顺时针旋转90度的那条轴。

下面将分别从container和item的角度来设置相关属性来说明这些属性是怎么使用的，以及他们的界面效果是怎么样的。

#### container上的属性

* **display**

css代码如下：

```css
    .container{
        display:flex;/*or inline-flex*/
    }
```
这个属性用于设置元素为使用flex布局，同时记住这个属性是其它属性的基础，这个没设置，其它的设置无效。

* **flex-direction**

css代码如下：

```css
    .container{
        display:flex;
        flex-direction:row | row-reverse | column | column-reverse;
    }
```

此属性用于设置container的里面item在空间上怎么排列，其实就是设置**main axis**轴在横向上还是在竖向上！默认值row，row对应从左到右，row-reverse对应从右到左，column对应从上到下，column-reverse对应从下到上。看下图一目了然：

![flex-direction设置](https://css-tricks.com/wp-content/uploads/2013/04/flex-direction2.svg)

#### item上的属性

...

### 相关资料链接

 [a complete guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

 [阮一峰flex布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
