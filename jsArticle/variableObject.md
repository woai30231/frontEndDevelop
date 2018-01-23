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

