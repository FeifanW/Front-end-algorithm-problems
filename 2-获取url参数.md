#### 题目描述

获取 url 中的参数

1. 指定参数名称，返回该参数的值 或者 空字符串
2. 不指定参数名称，返回全部的参数对象 或者 {}
3. 如果存在多个同名参数，则返回数组

示例1

#### 输入

```
http://www.nowcoder.com?key=1&key=2&key=3&test=4#hehe key
```

#### 输出

```
[1, 2, 3]
```

#### 题解：

```javascript
function getUrlParam(sUrl, sKey) {
    var paramsN = sUrl.split("?")[1];//取出url后的字符串
    var params = paramsN.split("#")[0];//剔除字符串#后的杂质
    var param = params.split("&");//将字符串分割为键值对为一项的数组
    var arr = [];

    if(sKey){//如果有参数
        for(var i = 0;i<param.length;i++){//遍历键值对数组
            var keyV = param[i].split("=");//分开键和值
            if(keyV[0] === sKey){//如果有和传入的参数一样的键，则将其值插入到空数组中
                arr.push(keyV[1]);
            }
        }
        if(arr.length === 0){//如果数组仍为空，则证明没有传入的参数的值
            return "";
        }else if(arr.length > 1){//有多个值
            return arr;
        }else{//只有一个值
            return arr[0];
        }
    }else{//没有传入参数，返回对象
        var obj = {};
        for(var i = 0;i<param.length;i++){//遍历
            var keyV = param[i].split("=");//分开键和值
            if(obj[keyV[0]]){//如果对象中有该属性
                obj[keyV[0]].push(keyV[1])//插入该属性中的数组中
            }else{
                obj[keyV[0]] = [keyV[1]]//如果没有则创建一个数组并且把值放入该数组中
            }
        }
        for(var key in obj){//遍历插入数据的对象
            if(obj[key].length === 1){//如果该对象的属性值的数组的长度为一
                obj[key] = obj[key][0]//则让该对象的该属性值为数组里的值
            }
        }
        return obj;
    }
}
```