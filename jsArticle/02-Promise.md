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
