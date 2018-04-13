### 前言

这篇文档希望通过简洁话语带领大家认识一下es6的Promise到底是个什么api，文中的案例代码都是我自己写的，因相关原因，难免有误的地方，**欢迎指出！**

### 什么是Promise?

从其英文字面意思来理解，Promise有承诺的意思，我们结合实际操作来理解就是：Promise在某个异步或同步的操作过程中，最后终将给出一个确切的“承诺”，用于后续的回调函数处理这个“承诺”！

来看个简单的例子：

```javascript
  var promise1 = new Promise((resolve,reject)=>{
      setTimeout(()=>{
        resolve('承诺1');//这里resolve函数的参数就是Promise用于给后续回调的一个“承诺”，且这个“承诺”是Promise给出的成功“承诺”
      },1000);
  });
  promise1.then((data)=>console.log(data));//输出：“承诺1”
  var promise2 = new Promise((resolve,reject)=>{
     setTimeout(()=>{
        reject("承诺2");//Promise给出的失败“承诺2”
     },1000);  
  });
  promise2.catch(data=>console.log(data));//输出：“承诺2”
```

从这里我们看出，两个Promise实例在setTimeout异步操作过程中，最后都给出了“承诺”（要嘛是成功“承诺”，要嘛是失败“承诺”）。所谓的“承诺”就是后续回调函数要处理的数据。

### Promise状态转换

我们知道，Promise最终都将给出承诺，那么给出怎样的承诺是跟我们实际业务逻辑联系在一起的，但这不是我们需要关心的，我们需要关心的就是Promise内部是怎么衔接给出“承诺”前后两个状态的。其实在Promise的工作过程中，Promise实例是通过状态机制来管理自身何时给出“承诺”的。主要有三个状态：pending、fulfilled及rejected，最开始是pending状态，有两种发展方向，1、pending-->fulfilled；2、pending-->rejected，不管Promise实例往何种方向发展，只要状态变为fulfilled或者rejected状态，那么就不会再发生状态变化，fulfilled和rejected之间是不会转换的。 我们看下下面的例子：

```javascript
  var promise = new Promise((resolve,reject)=>{
    resolve('成功');
    reject("失败");
  });
  promise.then(data=>{console.log(data)}).catch(e=>{console.log(e)});//只会输出“成功”
```
在上面的代码中，我们强制迫使Promise实例进行两种状态的变换，只要我们的状态一经变化到fulfilled或rejected的一种，就不会再发生状态变化，所以这里只会输出“成功”。

**注：** 调用resolve方法就是fulfilled，调用reject就是rejected！

### 为什么需要Promise

在没有Promise之前，我们在实际业务开发过程中，往往会有下面的需求
