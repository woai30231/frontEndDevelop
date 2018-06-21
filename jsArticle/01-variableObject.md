[文档参考地址](http://dmitrysoshnikov.com/ecmascript/chapter-2-variable-object/)

[更多文章](https://github.com/woai30231/webDevDetails)

### 说明

下面代码演示基于window系统chrome浏览器环境，版本号为63.0.3239.132，32位！相关结果可能会有一点出入，请也实际为准！

相关代码调试的过程中查看结果的步骤：

* 打开浏览器控制台，切换到sources板块，并选择相应的源文件；

* 在对应的源文件代码左边的行号上打上断点；

* 然后刷新浏览器，浏览器会在对应打断点的代码出停止执行，此时我们根据需要按f11键一步一步的运行代码，并同时查看代码的调用栈，作用域等情况，主要查看source板块下最右边子板块的Call Stack和Scope项。

### 相关概念梳理

其实从我自身出发，我觉的如果需要更好地理解变量对象的话，那么需要对以下概念有一个比较基本的理解会更方便些！

* **函数调用栈**

为了理解函数调用栈，我们先写一段代码：

```javascript
  function fn1(){
    console.log('fn1');
    fn2();
  };
  function fn2(){
    console.log('fn2');
  };
  fn1();
```
我们在fn2函数调用的地方打上断点，然后刷新浏览器，查看Call Stack选项，会看到下面的结果：

```bash
  fn1
  (anonymous)
```
此时再按一次f11键，此时Call Stack显示结果如下：

```bash
  fn2
  fn1
  (anonymous)
```
这里说明一下，anonymous指代全局匿名调用函数环境，而fn1和fn2分别指代fn1函数作用域和fn2作用域环境。

* **函数作用域**

* **闭包**








