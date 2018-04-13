[文档参考地址](http://dmitrysoshnikov.com/ecmascript/chapter-2-variable-object/)

### 介绍

在程序设计时，尽管我们成功地定义了变量和函数以致实现了系统的功能，但是解释器在解释的时候它是怎么知道去哪儿找这些我们定义的数据呢（函数、变量），并且当
我们在程序中引用这些数据的时候，解释器内部发生了什么？

许多ECMAScript程序员都知道,变量是与执行上下文是密切相关的：

```javascript
  var a = 10; //a变量存在于全局上下文中
  (function(){
    var b = 20;//b变量存在函数上下文自己的作用域中
  })();
  
  alert(a); //10
  alert(b); //"b" is not defined
```

不仅如此，就当前版本的ecmascript版本来说，javascript只存在函数作用域，相对于其它语言，如c/c++，javascript里面是不存在块级作用域的：

```javascript
  for(var k in {a:1,b:2}){
    alert(k);
  };
  alert(k);  //我们发现，在这里依然能alertk值，即便for循环已经结束了。
```

让我们来细看一下当我们定义一个数据的时候发生了什么！

### 数据声明

既然变量与执行上下文有关，那么执行上下文就应该知道数据存储在什么地方并且知道怎么取到数据，此种机制就叫作变量对象。

> 变量对象（简写VO）是一个特殊的对象，它与执行上下文有关，并且存储了下面的数据：
>
>    * 变量，通过var声明的变量
>
>    * 函数声明（FunctioniDeclaration，简称FD）
>
>    * 函数形参

举个例子，我们可以把变量对象看成一个普通的javascript对象：

```javascript
  VO = {};
```

并且前面说过，VO是执行上下文的一个属性：

```javascript
  activeExecutionContext = {
    VO:{
      //数据 包括（var声明的变量，函数声明，函数参数）
    }
  };
```

只有在全局上下文中，才可以间接引用变量（通过属性名）（在全局上下文中，变量对象就是全局对象）。相对于其它上下文而言，是不能直接引用到VO的，这纯粹是js内部实现的一个机制。

当我们定义一个变量或者函数的时候，其实就是在VO上新建了一个同名的属性和方法及其对应属性值的过程。

例如：

```javascript
  var a = 10;
  function test(x){
    var b = 20;
  };
  test(30);
```
那么对应的VO就是：

```javascript
  //全局上下文上的VO
  VO(globalContext) = {
    a: 10,
    test: <reference to function>
  };
  
  //test函数上下文的VO
  VO(test functionContext) = {
    x: 30,
    b: 20
  };
```

我们需要注意的是，在javascript内部实现层（规范中），变量对象是个抽象的概念，可能并不叫VO，并且最初的结构一步一定如此。

### 不同执行上下文中的变量对象

变量对象上的一些操作（比如：变量的初始化）和行为对于所有的执行上下文类型来说都已一样的。从这一点来说，将变量对象表示成抽象的概念更加合适。 函数上
下文还能定义额外的与变量对象相关的信息。


> AbstractVO (generic behavior of the variable instantiation process)
> 
>   ║
>
>   ╠══> GlobalContextVO
>
>   ║        (VO === this === global)
>
>   ║
>
>   ╚══> FunctionContextVO
>
>            (VO === AO, <arguments> object and <formal parameters> are added)
  


我们来详细讨论。

### 全局上下文中的变量对象

首先，我们给一下全局对象的定义：

> 全局对象就是








