# 整理一些JS小方法
## 数组
- Except取差集
```JS
  //way1
Array.prototype.diff = function(a) {
    return this.filter(function(i) {return a.indexOf(i) < 0;});
};
//way2
  let exceptArr = a1.filter(key => !a2.includes(key));
//wa3
  var Except = function(arr1, arr2) {
  
    var set1 = new Set(arr1);
    var set2 = new Set(arr2);
    var subset = [];
    for (let item of set1) {
    
        if (!set2.has(item)) {
            subset.push(item);
        }
        
    }

    return subset;
};
//way4
let exceptArr = a1.filter(ea=>a2.every(eb=>eb!==ea));
//filter筛选a集合的元素，如果当前筛选的元素与b集合中的every每一个元素都不相等vb!==va，则将此元素加入到返回集合中

```
- Intersect数组取交集
