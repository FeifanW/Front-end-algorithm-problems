#### 封装函数 f，使 f 的 this 指向指定的对象

```javascript
//法一：
function bindThis(f, oTarget) {
  return f.bind(oTarget);
}
//法二：
function bindThis(f, oTarget) {
    return function(){
        return f.apply(oTarget,arguments);
    }
}
```

因为apply的第二个参数是可选的，所以并不需要一定要有；我觉得原因是bind返回的是一个函数，而apply方法是立即执行函数，所以需要放在一个函数里面，到调用的时候再立即执行。小小拙见，望批评指正。
apply和call的区别主要是，apply只接收数组形式的参数输入 

