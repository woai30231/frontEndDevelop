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

* **flex-wrap**

css代码如下：

```css
    .container{
        display:flex;
        flex-wrap: nowrap | wrap | wrap-reverse;
    }
```

因为flex布局本身是弹性的，它可以根据屏幕大小来自动缩放从而来适应屏幕。所以默认情况下container下的item元素都会排列在一行上，屏幕越小，item元素也会变得很窄。有些情况下，这种情况并不是我们想要的。我们希望屏幕缩小时候，一行放不下内容，又不想缩放item来达到效果。那么我们就可以明确设置换行来告诉流浪器在下一行显示内容，如图所示：

![flex-wrap设置](https://css-tricks.com/wp-content/uploads/2014/05/flex-wrap.svg)

其中wrap-reverse设置item从下往上开始换行。

* **flex-flow**

css代码如下：

```css
    .container{
        display:flex;
        flex-flow:<‘flex-direction’> || <‘flex-wrap’>
    }
```

不难理解，该属性是flex-direction和flex-wrap的简写形式，第一个值是flex-direction值，对应的，第二个值flex-wrap值。

* **justify-content**

css代码如下：

```css
    .container {
        display:flex;
        justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
    }
```

该属性设置item元素在**main axis**轴向上怎样排列，分别如下：

1、flex-start代表从开始点上一个一个的排下去，好比设置float布局设置属性为float为left；

2、flex-end代表从结束点上一个一个的排，好比设置float布局设置属性为float为right；

3、center，这个不能理解，居中排列；

4、space-between代表除了头尾两个item元素的左边距和右边距分别不存在，中间的间距一样；

5、space-around代表item的左右间距相等，但是头尾两个item因为分别没有前一个和后一个元素，所以视图上会少一半间距；

6、space-around代表所有item元素左右两侧的间距相等。

话不多说，来张图查看更能理解：

![justify-content设置](https://cdn.css-tricks.com/wp-content/uploads/2013/04/justify-content-2.svg)

 *注：flex-start值总是相对于容器的左上角而言的*

* **align-items**

css代码如下：

```css
    .container {
        align-items: flex-start | flex-end | center | baseline | stretch;
    }
```

该属性设置每一行(**注意是每一行内部**)上的item元素在**cross aixs**轴上的对齐方式，分别含义如下：

1、flex-start代表顶对齐；

2、flex-end代表底对齐；

3、center代表居中对齐；

4、baseline代表按baseline对齐；

5、stretch代表他们高度一样。

如下图形象所示：

![align-items设置](https://cdn.css-tricks.com/wp-content/uploads/2014/05/align-items.svg)

* **align-content**

css代码如下：

```css
    .container{
       .container {
            align-content: flex-start | flex-end | center | space-between | space-around | stretch;
        } 
    }    
```

该属性设置的**多行**item元素在**cross axis**轴上的对齐方式，分表含义跟justify-content差不多，不解释了，直接看图吧！

![align-content](https://css-tricks.com/wp-content/uploads/2013/04/align-content.svg)


#### item上的属性

* **order**

css代码如下：

```css
    .item{
        order: <integer>; /* default is 0 */
    }
```

设置item元素的排列顺序，默认是按书写代码的顺序排列的！该值越小越靠前。 如图所示：

![order设置](https://css-tricks.com/wp-content/uploads/2013/04/order-2.svg)

* **flex-grow**

css代码如下：

```css
    flex-grow: <number>; /* default 0 */
```

该属性设置item元素container的一行上屏幕拉伸时的宽度占比。你可以理解它定义了item元素怎么填充container的一行，很显然，数字越大，占的空间越大。来看图吧：

![](https://css-tricks.com/wp-content/uploads/2014/05/flex-grow.svg)

* **flex-shrink**

css代码如下：

```css
    .item {
        flex-shrink: <number>; /* default 1 */
    }
```
注意：负数无效，该属性用于设置当屏幕宽度不足时候，item元素收缩的比率。

* **flex-basis**

css代码如下：

```css
    .item {
        flex-basis: <length> | auto; /* default auto */
    }
```
该属性用来设置item元素原始的宽度，如果flex-grow和flex-shrink都设置为0，那么item的宽度值（或者说高度值，取决如果设置container的flex-direction属性）将始终保持这个宽度。

  **这里有个特别注意的地方，就是当我们设置flex-direction的值为column的时候，那么此时设置的flex-basis属性值的值就是指的是items的高度值，切记！**

* **flex**

css代码如下：

```css
    .item {
        flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    }
```
该属性是前面三个属性的简写形式，推荐使用这种方式写前面三个属性，该属性默认值是0 1 auto。

### 兼容性写法

毫无疑问，老一点的浏览器对flex布局是有兼容问题的,但这里我们不讨论flex布局的与其他布局方式的兼容问题，而是来说明一下flex布局在各大浏览器中本身写法上兼容问题，并不是简单的加下相应的浏览器厂商前缀。为什么会造成这样的写法，主要是历史发展的原因，各种版本之间权衡造成写法繁多，下面贴上flex布局的规范地址，遇到相关问题可以查阅！

![flex布局规范](https://www.w3.org/TR/css-flexbox-1/)

### 相关资料链接

 [a complete guide to flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

 [阮一峰flex布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
