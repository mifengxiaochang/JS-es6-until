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
```Js
//Way1
let intersectionSet = new Set([...arr1].filter(x => arr2.has(x)));
//Way2
var Intersect=()=>{
  var intersect = [];
  for (var i = 0; i < arr1.length; i++) {
      if (arr2.indexOf(arr1[i]) > -1) {
          intersect.push(arr1[i]);
      }
  }
  return intersect;
}
//Way3
function Intersect(a, b) { 
    var result = [];
    for(var i = 0; i < b.length; i ++) {
        var temp = b[i];
        for(var j = 0; j < a.length; j ++) {
            if(temp === a[j]) {
                result.push(temp);
                break;
            }
        }
    }
    return array_remove_repeat(result);
}

function array_remove_repeat(a) { // 去重
    var r = [];
    for(var i = 0; i < a.length; i ++) {
        var flag = true;
        var temp = a[i];
        for(var j = 0; j < r.length; j ++) {
            if(temp === r[j]) {
                flag = false;
                break;
            }
        }
        if(flag) {
            r.push(temp);
        }
    }
    return r;
}
```
- 并集
```JS
  // way1
let unionSet = new Set([...a, ...b]);
```
下班咯先跑咯┏(＾0＾)┛
