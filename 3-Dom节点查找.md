#### 题目描述

查找两个节点的最近的一个共同父节点，可以包括节点自身

#### 输入描述:

```
oNode1 和 oNode2 在同一文档中，且不会为相同的节点
```

#### 题解：

```javascript
function commonParentNode(oNode1, oNode2) {
    var parent1 = [];   //用于存储包括oNode1的所有oNode1父节点
    parent1.push(oNode1);
    while(oNode1.parentNode){
        parent1.push(oNode1.parentNode);
        oNode1 = oNode1.parentNode;
    }
    while(oNode2){   //看oNode2及其祖先节点是否有包含在oNode1中所有祖先节点的
        for(var i in parent1){
            if( parent1[i] == oNode2 ){
                return oNode2;
            }
        }
        oNode2 = oNode2.parentNode;
    }
    return oNode2;
}
```