# 整理一些JS小方法
---

## 数组

### 删除数组的重复项
```
var fruits = [“banana”, “apple”, “orange”, “watermelon”, “apple”, “orange”, “grape”, “apple”];
// First method
var uniqueFruits = Array.from(new Set(fruits));
console.log(uniqueFruits); // returns [“banana”, “apple”, “orange”, “watermelon”, “grape”]
// Second method
var uniqueFruits2 = […new Set(fruits)];
console.log(uniqueFruits2); // returns [“banana”, “apple”, “orange”, “watermelon”, “grape”]
```
### form达到map效果
```
var friends = [
    { name: ‘John’, age: 22 },
    { name: ‘Peter’, age: 23 },
    { name: ‘Mark’, age: 24 },
    { name: ‘Maria’, age: 22 },
    { name: ‘Monica’, age: 21 },
    { name: ‘Martha’, age: 19 },
]
var friendsNames = Array.from(friends, ({name}) => name);
console.log(friendsNames); // returns [“John”, “Peter”, “Mark”, “Maria”, “Monica”, “Martha”]

```

### 代替forEach终止循环
```
[0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true;
  }
  console.log(val); // your code
});
//> 0, 1

//eg2
// Array contains 2
const isTwoPresent = [0, 1, 2, 3, 4].some(function(val, i) {
  if (val === 2) {
    return true; // break
  }
});
console.log(isTwoPresent);
//> true

// Using .evert to brack a loop
const isSmallerThan10 = num => num < 10;

console.log([2, 5, 8, 1, 4].every(isSmallerThan10));  // true
console.log([12, 5, 8, 1, 4].every(isSmallerThan10)); // false
```

### 将数组转换为对象
```
var fruits = [“banana”, “apple”, “orange”, “watermelon”];
var fruitsObj = { …fruits };
console.log(fruitsObj); // returns {0: “banana”, 1: “apple”, 2: “orange”, 3: “watermelon”, 4: “apple”, 5: “orange”, 6: “grape”, 7: “apple”}
```
### 数组合并
```
var fruits = [“apple”, “banana”, “orange”];
var meat = [“poultry”, “beef”, “fish”];
var vegetables = [“potato”, “tomato”, “cucumber”];
var food = […fruits, …meat, …vegetables];
console.log(food); // [“apple”, “banana”, “orange”, “poultry”, “beef”, “fish”, “potato”, “tomato”, “cucumber”]

```
### lastIndexOf() 方法
最后一次的下标
```
var nums = [1, 5, 2, 6, 3, 5, 2, 3, 6, 5, 2, 7];
var lastIndex = nums.lastIndexOf(5);
console.log(lastIndex); // returns 9
```
#### Except取差集
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

handlePrint=()=>{
    const { discData } = this.props;
    if(this.state.showTable && !isEmptyObject(discData)){
      const printContent = document.getElementById('discTable').innerHTML;
      const frame = document.getElementById('printWrap');
      frame.contentDocument.write(printContent);
      frame.contentDocument.close();
      frame.contentWindow.print();
    }else{
      message.warning('请先执行统计操作!');
    }
  }
//way5

  // 差集
   let a = [1, 2, 3]
    let b = [2, 4, 5]
 
    let aSet = new Set(a)
    let bSet = new Set(b)

    let differenceNew = Array.from(new Set(a.concat(b).filter(v => aSet.has(v) && !bSet.has(v))) [1,3]
```
#### 并集
```
let union = Array.from(new Set(a.concat(b))) // [1,2,3,4,5]

```
#### Intersect数组取交集
```Js
//Way1
let a = [1, 2, 3];    let b = [2, 4, 5];
let bSet = new Set(b);
let intersection = Array.from(new Set(a.filter(v => bSet.has(v)))// [2]
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
#### 对对象数组某属性求和
```jS
const getSum = (arr,prop)=>{
  const total = arr.slice(10).reduce((sum, num) => {
      return sum + Number(num[prop]);
    }, 0) ;
    return total;
}

    
const getTop11 = (arr, prop) => {
  let attr = {};
  let rank;
  if (arr.length > 11) {
    const topTen = arr.slice(0, 10);
    rank = topTen;
    // 其他求平均值
    attr = (arr.slice(10).reduce((sum, num) => {
      return sum + Number(num[prop]);
    }, 0) / (arr.length - 10)).toFixed(4);

    rank.push({ level1NameZh: 'other', [prop]: attr });
  } else {
    rank = arr;
  }
  return rank;
};
    
```

#### 删除数组最后一个元素
```JS
var x = ['1','2','3','4'];
   x.splice(-1,1);
```
#### 并集
```JS
  // way1
let unionSet = new Set([...a, ...b]);
//way 2
var union = (a, b) => {
    return array_remove_repeat(a.concat(b));//上面去重
}
```
#### 排序
```JS
Array.prototype.orderBy = (property,byDesc = false) => {
        return (pre, next) => {
            let p = pre[property],
                n = next[property];
            if (!isNaN(Number(p)) && !isNaN(Number(n))) {
                p = Number(p);
                n = Number(n);
                if (p === n) {
                    return 0;
                } else {
                    return byDesc ? (p > n ? -1 : 1) : (p > n ? 1 : -1);
                }
            } else {
                return byDesc ? n.localeCompare(p) : p.localeCompare(n);
            }
        };
}
```

#### 深克隆数组

```JS
 let deepCloneObjArray = (_array) => {
    return [].concat(JSON.parse(JSON.stringify(_array)));
  }  
```
       针对对象引用问题（Converting circular structure to JSON）
  
```JS
  let deepCloneReferObjArray = (_array) => {
    return  [].concat(JSON.parse(JSON.stringify(_array, (key, value) => {
                if (typeof value === 'object' && value !== null) {
                    if (cache.indexOf(value) !== -1) {
                        return;
                    }
                    cache.push(value);
                }
                return value;
            })))
  }
```
#### 判断数组
```JS
//way1
  var isArray = (obj)=> {
    return Object.prototype.toString.call(obj) === '[object Array]';
  }
  
  //way2
  Array.isArray(arr)
  
  //判断对象是否为数组
  Object.isArray(obj)
```
#### 检索数据是否包含某个数据
```JS
[1,2,3,4].includes(5);//false
```

#### 对象数组指定属性是否相等
```JS
/**
 * 判断一个集合内的每个对象的指定属性的值是否全部相同
 * @param {any} items
 * @param {any} property
 */
 function hasValueAllSame(items, propertyName) {
    if (items == null || items.length == 0)
        return false;

    if (typeof items[0] == 'string') {
        for (let item of items) {
            if (item == null && items[0] == null) {
                continue;
            }
            if (item != items[0]) {
                return false;
            }
        }
        return true;
    } else {
        for (let item of items) {
            if (item[propertyName] == null && items[0][propertyName] == null) {
                continue;
            }
            if (item[propertyName] != items[0][propertyName]) {
                return false;
            }
        }
        return true;
    }
}

```
### 处理数组对象数据
1.数组对象元素相同,分组显示
```
let arry = [
    { expensedate: '2018/09/29', amount: 1, type: '交通费' },
    { expensedate: '2018/08/19', amount: 2.5, type: '补贴费' },
    { expensedate: '2018/09/29', amount: 6.3, type: '住宿费' },
    { expensedate: '2018/01/19', amount: 18.5, type: '采购经费' },
    { expensedate: '2018/09/22', amount: 8.4, type: '活动经费' },
    { expensedate: '2018/09/29', amount: 7.9, type: '材料打印费' }
]
let items = [];
let datelist = {};
for (let i = 0; i < arry.length; i++) {
    let element = arry[i];
    if (!datelist[element.expensedate]) {
        items.push({
            expensedate: element.expensedate,
            subitems: [element]
        })
        datelist[element.expensedate] = element;
    } else {
        for (let j = 0; j < items.length; j++) {
            let subment = items[j];
            if (subment.expensedate == element.expensedate) {
                subment.subitems.push(element)
            }
        }
    }
 
}
console.log(items);
```
2、数组对象元素相同,汇总显示
```
let arrys = [
    { expensedate: '2018/09/29', amount: 1, type: '交通费' },
    { expensedate: '2018/08/19', amount: 2.5, type: '补贴费' },
    { expensedate: '2018/09/29', amount: 6.3, type: '交通费' },
    { expensedate: '2018/01/08', amount: 18.5, type: '采购经费' },
    { expensedate: '2018/09/22', amount: 8.4, type: '活动经费' },
    { expensedate: '2018/09/29', amount: 7.9, type: '交通费' }
]
let otheritems = [];
let list = {};
for (let i = 0; i < arrys.length; i++) {
    let element = arry[i].expensedate;
    if (list[element]) {
        list[element].expensedate = list[element].expensedate;
        list[element].amount = list[element].amount + arrys[i].amount;
    } else {
        list[element] = {};
        list[element].expensedate = arrys[i].expensedate;
        list[element].amount = arrys[i].amount;
    }
    list[element].type = arrys[i].type;
}
//对象转数组
for (var i in list) {
    otheritems.push(list[i])
}
console.log(otheritems)
```
#### 过滤数据
```JS
const posts = [
  {id: 1, title: 'Title 1'},
  {id: 2, title: 'Title 2'},
  {id: 1, title: 'Title 1.1'}
];
// 找到第一个id为1的数据
const title1 = posts.find(p => p.id === 1).title;

const title1s = posts.filter(p => p.id === 1);//找到所有id为1的数据
```

- keys() - 获得数组中所有元素的键名（实际上就是下标索引号）
- values() - 获得数组中所有元素的数据
- entries() - 获得数组中所有数据的键名和数据
```JS
for(let index of ['a','b'].keys()){
  console.log(index);
}//=>0   1

for(let item of ['a','b'].values()){
  console.log(item);
}//=>'a'   'b'

for(let [index,iten] of ['a','b'].values()){
  console.log(index,iten);
}//=>0 'a'   1 'b'
```
#### 向数组中的指定位置添加数据
```
arr.splice(2,0,"10")
输出: array=[0,1,10,2,3,4,5];
```
#### 删除数组中的指定位置的数据并用新数据替换
```
arr.splice(2,1,"10")
输出: array=[0,1,10,3,4,5];
```
#### 删除数组中的指定位置开始的多个数据并用新数据替换
```
arr.splice(2,3,"10") 
输出: array=[0,1,10,5];
```
#### 删除数组中的指定位置的数据方法
####  获取数组中数据的下标
```
var index = array.indexOf(4);
```
#### 删除数据
```
if(index>-1){
array.splice(index,1);
}
```

### 删除数组虚值
在 JS 中，虚值有 false, 0，''， null, NaN, undefined。咱们可以 .filter() 方法来过滤这些虚值。
```
var mixedArr = [0, “blue”, “”, NaN, 9, true, undefined, “white”, false];
var trueArr = mixedArr.filter(Boolean);
console.log(trueArr); // returns [“blue”, 9, true, “white”]

```


## 数字、字符串、对象(⊙o⊙)…
#### 忽略大小写相等
```Js
  let EqualsIgnoreCase  = (str1,str2) => {  
    if (str1.toLowerCase() == str2.toLowerCase()) {
        return 1; // true
    }
    else {
        return 0; // false
    }
  }
```
#### 是否是整数
```JS
  //way1
  let isInt = (num) => {
    var partten = /(^[1-9][0-9]*$)|(^[0-9]$)/;
    return partten.test(num);
  }
  //way2
  
Number.isInteger(21)//true
Number.isInteger(1.11)//false

```

顺便记录下

转换 Number.parseInt - 将字符串或数字转换为整数 Number.parseFloat - 将字符串或数字转换为浮点数
### 判断是否是数字
```
Number.isFinite();//只对数值有效 判断是否是无穷也可以用为是否为数字
isFinite();// 将非数值的值转为数值，判断是否是数字

```
### 单词匹配
```jS
let url= "https://github.com/mifengxiaochang/JS-es6-until/edit/master/README.md";
let matchWord = new RegExp('\\b(' + word + ')\\b');//word变量 \b正则单词匹配
      if (url.match(matchWord)) {
        
      }

```

#### 是否是NaN
```JS
//测试是否NaN
Number.isNaN(Nan)//true
Number.isNaN(1)//false
```
#### 删除对象某个字段
```JS
const user = {name: 'S K', age: 23, password: 'SantaCl@use'};
const newUser = {...user};
delete newUser.password;
// {name: "S K", age: 23}不影响远对象

```
#### 字符串是否为空
```JS
  const isNullorEmpty = (str) => {
    return str == undefined || str == null || empty(str);    
  }
  const empty = (str) => {
    return str.trim() == '';    
  }
```

#### 字符串去首尾空格
```JS
//way1
 let a=" 123 " 
 a.trim();//=>"123"
 
 //way2
 let trim = (str)=>{
  return str.replace(/(^\s*)|(\s*$)/g, ""); 
 }


```

### 字符串长度
```
function GetLength(str) {
  // /<summary>获得字符串实际长度，中文2，英文1</summary>
  // /<param name="str">要获得长度的字符串</param>
  let realLength = 0;
  const len = str.length;
  let charCode = -1;
  for (let i = 0; i < len; i++) {
    charCode = str.charCodeAt(i);
    if (charCode >= 19968 && charCode <= 40869) realLength += 2;//4E00 9FA5
    else realLength += 1;
  }
  return realLength;
}
```
### 随机生成字符串
```
Math.random().toString(36).substr(2, 1);

```
### 判断字符状态
```
console.log(str.match(/[\u0000-\u00ff]/g))     //半角   
console.log(str.match(/[\u4e00-\u9fa5]/g))     //中文   
console.log(str.match(/[\uff00-\uffff]/g))     //全角  
```

####计算页数
```JS
let pageCont = Math.ceil(totalCount / pageSize); //Math.ceil返回大于等于参数x的最小整
```

#### 判断空对象
```JS
   const isEmptyObject = (e) =>{
    let t;
    for (t in e) {
        return false;
    } return true;
  };
  
//  敷衍eslint
export const isEmptyObject = (e) =>{
  // let t;
  for (const t in e) {
    if (Object.prototype.hasOwnProperty.call(e, t)) {
      return false;
    }
  } return true;
};
```
#### 选择和筛选对象属性
```
// pick
function pick(obj, keys) {
    return keys.map(k => k in obj ? {[k]: obj[k]} : {})
               .reduce((res, o) => Object.assign(res, o), {});
}
// eg
const row = {
    'accounts.id': 1,
    'client.name': 'John Doe',
    'bank.code': 'MDAKW213'
};
const table = [
    row,
    {'accounts.id': 3, 'client.name': 'Steve Doe', 'bank.code': 'STV12JB'}
];
pick(row, ['client.name'])  // 取到了 client name
table.map(row => pick(row, ['client.name'])); // 取到了一系列 client name


// reject 利用 pick
function reject(obj, keys) {
    const vkeys = Object.keys(obj)
        .filter(k => !keys.includes(k));
    return pick(obj, vkeys);
}

```
#### 深拷贝（解决对象引用问题）
```JS
function deepCopy(obj) {
    return JSON.parse(JSON.stringify(obj));
}

function deepReferenceObjCopy(obj){
      return JSON.parse(JSON.stringify(obj, (key, value) => {
                if (typeof value === 'object' && value !== null) {
                    if (cache.indexOf(value) !== -1) {
                        return;
                    }
                    cache.push(value);
                }
                return value;
            }))
}

```
#### 合并对象
```JS
let a = {a:1,b:2}, b = {b:3}, c = {b:4,c:5};
let d = Object.assign({}, a, b, c);
//第一个参数增加一个空对象，在合并时让它被更新，不影响实际的对象变量内容
console.log(d);
//{a:1,b:4,c:5}//与上面的方式合并结果一致，使用这种方式, a 对象的内容就不会被影响了
```
### 将一个对象的部分属性传给另一个对象
```
 //way1
 const pick = (obj, arr) => {
   return arr.reduce(
    (iter, val) => (val in obj && (iter[val] = obj[val]), iter),
  //   {}
  );
};

//way2


```

### 对象内容集合
- Object.keys() - 获得对象中所有的键名，以数组的形式返回
- Object.values() - 获得对象中所有的值内容，以数组的形式返回
- Object.entries() - 获得对象中所有的成员数据，以数组的形式返回，成员的内容也是数组形式
```JS
let obj={a:1,b:2};
let names = Object.keys(obj);//=>['a','b']
let values = Object.entries(obj);//[['a',1]['b',2]]
```

#### long 
 使用string模拟大数减法  
```JS
 function sub(num1, num2) {
    // 标识结果是否为负  
    let isNeg = false;
    let result = '';
    // 处理 负号  
    if (num1.indexOf('-') != -1 && num2.indexOf('-') == -1) {
        num1 = num1.replace("-", "");
        return "-" + add(num1, num2);
    } else if (num1.indexOf('-') != -1 && num2.indexOf('-') != -1) {
        num2 = num2.replace("-", "");
        num1 = num1.replace("-", "");
        return sub(num2, num1);
    } else if (num1.indexOf('-') == -1 && num2.indexOf('-') != -1) {
        return add(num1, num2);
    }
    // 判断两个数谁更大，使用大的减小的  
    if (isSmall(num1, num2)) {
        // 交换二者的值  
        let temp = num1;
        num1 = num2;
        num2 = temp;
        isNeg = true;
    }
    // 两个正数相减  
    if (num1.length < num2.length) {
        num1 = castSame(num1, num2.length);
    } else if (num1.length > num2.length) {
        num2 = castSame(num2, num1.length);
    }

    let index = num1.length - 1;
    let res = 0;
    // 借位标识  
    let borrow = 0;
    while (index >= 0) {
        let num1Int = parseInt(num1[index]);
        let num2Int = parseInt(num2[index]);
        if ((num1Int - borrow) < num2Int) {
            res = 10 + num1Int - borrow - num2Int;
            borrow = 1;
        } else {
            res = num1Int - borrow - num2Int;
            borrow = 0;
        }
        result = res.toString() + result;
        index--;
    }

    // 去掉前面的无效的0  
    let resultStr = "";
    if (isNeg) {
        resultStr = removeZero(result);
        resultStr = "-" + resultStr;
    } else {
        resultStr = removeZero(result);
    }
    return resultStr;
}
// 判断两个参数谁更小(输入的两个参数必须都为正数）  
export function isSmall(num1, num2) {
    if (num1.length < num2.length) {
        return true;
    } else if (num1.length > num2.length) {
        return false;
    }
    // 两个数 总位数一样  
    let index = 0;

    while (index < num1.length) {
        let num1Temp = parseInt(num1[index]);
        let num2Temp = parseInt(num2[index]);
        if (num1Temp < num2Temp) {
            return true;
        } else if (num1Temp > num2Temp) {
            return false;
        }
        index++;
    }
    return false;
}

// 去掉最前面的无效的0（参数必须为正数）  
function removeZero(input) {
    let length = input.length;
    let i = 0;
    for (; i < length; i++) {
        let current = input[i];
        if (current != '0') {
            break;
        }
    }
    if (i === length) {
        return '0';
    } else {
        return input.substring(i);
    }
}
function castSame(input, len) {
    if (input.length > len) {
        return null;
    }
    let result = '';
    let subLength = len - input.length;
    for (let i = 0; i < subLength; i++) {
        result = result + '0';
    }
    return result + input;
}

// 使用string模拟大数加法  
 function add(num1, num2) {
    let result = '';
    // 标识结果是否为负  
    let isNeg = false;
    // 处理符号  
    if (num1.indexOf('-') != -1 && num2.indexOf('-') != -1) {
        num1 = num1.replace("-", "");
        num2 = num2.replace("-", "");
        isNeg = true;
    } else if (num1.indexOf('-') != -1 && num2.indexOf('-') == -1) {
        num1 = num1.replace("-", "");
        return sub(num2, num1);
    } else if (num1.indexOf('-') == -1 && num2.indexOf('-') != -1) {
        num2 = num2.replace("-", "");
        return sub(num1, num2);
    }
    // 将两个加数处理成长度相同的字符串，长度不够，使用0填充  
    if (num1.length > num2.length) {
        num2 = castSame(num2, num1.length);
    } else if (num1.length < num2.length) {
        num1 = castSame(num1, num2.length);
    }

    let length = num1.length;
    let index = length - 1;
    // 进位标识  
    let add = 0;
    // 当前位的结果  
    let res = 0;
    let sum = 0;
    let num1Int;
    let num2Int;
    while (index >= 0) {
        num1Int = parseInt(num1[index]);
        num2Int = parseInt(num2[index]);
        sum = num1Int + num2Int + add;
        add = parseInt(sum / 10);
        res = sum % 10;
        result = res.toString() + result;
        index--;
    }
    // 处理最后一个进位  
    if (add == 1) {
        result = '1' + result;
    }
    let resultStr = removeZero(result);
    if (isNeg) {
        resultStr = "-" + resultStr;
    }
    return resultStr;
}


```

## 时间
#### 转换 C# ticks
```JS
   const defaultTicks = 621355968000000000;
   let convertDateToUtcTicks = (date = new Date()) => {
      return date.getTime() * 10000 + defaultTicks;
    }
```
- local
 ```JS
  convertUtcTicksToLocalDate(ticks) {
    return new Date((ticks - defaultTicks) / 10000);
  }
 ```
 - sort
 ```JS
  sortDatas(d1, d2, sortBy, asc) {
    let i1 = d1[sortBy], i2 = d2[sortBy];
    if (typeof i1 === "string")
        i1 = i1.toLocaleLowerCase();
    if (typeof i2 == "string")
        i2 = i2.toLocaleLowerCase();
    if (i1 == i2)
        return 0;
    let result = asc ? (i1 < i2) : (i1 > i2);
    return result ? -1 : 1;
  }
 
 ```
 
 #### 格式化yyyyMMddToYYYY-MM-DD
 ```
var r="20151201".replace(/^(\d{4})(\d{2})(\d{2})$/, "$1-$2-$3")
console.log(r);//2015-12-01
 
 ```
#### 格式化
```JS
/**
 * 格式化Date
 * @param {Date} date
 * @param {string} format 自定义格式下传递该参数，否则使用cp中设置的format
 */
  formatDate(date, hasTime, format) {
        if (hasTime == null)
            hasTime = true;

        if (typeof date == 'number')
            date = new Date(date);
        else if (typeof date == 'string')
            date = new Date(parseInt(date));

        if (format == null) {
            return window.formatDateTime(date, hasTime);
        } else {
            return $$.gcalendar('toFormatString', { date: date, format: format });
        }
    }
```
```
export function getQueryString(url) {
    var theRequest = new Object(), strs = [];
    if (url.indexOf("?") != -1) {
        var str = url.substr(1);
        strs = str.split("&");
        for (var i = 0; i < strs.length; i++) {
            theRequest[strs[i].split("=")[0]] = unescape(strs[i].split("=")[1]);
        }
    }
    return theRequest;
}

```
## 格式化国际化日期
```
new Date().toLocaleString('sv',{ year: 'numeric',month: 'numeric',day: 'numeric'});// 瑞典："2020-01-16"
new Date().toLocaleString('sv',{ year: 'numeric',month: 'numeric',day: 'numeric'});// 中国："2020/1/16"
```

#### 几个面试题

1.下面代码的输出结果是什么？
```
function MyObj(){
  this.p.pid++
}
MyObj.prototype.p = {'pid': 0}
MyObj.prototype.getNum = function(num){
  return this.p.pid + num
}
var _obj1 = new MyObj()
var _obj2 = new MyObj()
console.log(_obj1.getNum(1)+_obj2.getNum(2))  // 7
```
2.请手绘出html渲染结果，如下图：
3.请阅读以下代码，给出运行结果。
```
Var func = (function(a) {
  this.a = a;
  return function(a) {
  a += this.a;
  return a;
}
})(function(a, b){
  return a;
}(1, 2));
func(4);  // 5
```
4. 下面代码的输出结果是什么。
if(!(“a” in window)) {
var a = 1;
}
console.log (a);   // undefined
5. 请写出单例模式的实现，至少两种。

-- 传统单例模式：

 保证一个类仅有一个实例，并提供一个访问它的全局访问点。
 用一个变量来标志当前是否已经为某个类创建过对象，如果是，则在下一次获取该类的实例时，直接返回之前创建的对象
-- 实现单例核心思想
```
// 1、构造函数内部判断
function Construct(){
    // 确保只有单例
    if( Construct.unique !== undefined ){
        return Construct.unique; 
    }
    // 其他代码
    this.name = "NYF";
    this.age="24";
    Construct.unique = this;
}
var t1 = new Construct();
var t2 = new Construct();
//2、闭包方式
//2.1
var single = (function(){
    var unique;
    function Construct(){
        // ... 生成单例的构造函数的代码
    }
    unique = new Constuct();
    return unique;
})();
  如果希望会用调用 single() 方式来使用，那么也只需要将内部的 return 改为
    var single = (function(){
    var unique;
    function Construct(){
        // ... 生成单例的构造函数的代码
    }
    unique = new Constuct();
    return function(){
        return unique;
    } 
})
    
//2.2
var CreateDiv = function (html) {
        this.html = html;
        this.init();
    };
    
    CreateDiv.prototype.init = function () {
        var div = document.createElement('div');
        div.innerHTML = this.html;
        document.body.appendChild(div);
    };
    
    var ProxySingletonCreateDiv = (function () {
        var instance;
        return function (html) {
            if (!instance) {
                instance = new CreateDiv(html);
            }
            return instance;
        }
    })();
    
    var a = new ProxySingletonCreateDiv('sven1');
    var b = new ProxySingletonCreateDiv('sven2');

    alert(a === b); //true
    
   
    //3.单例模式抽象，分离创建对象的函数和判断对象是否已经创建
    var getSingle = function (fn) {
        var result;
        return function () {
            return result || ( result = fn.apply(this, arguments) );
        }
    };
```
6.请描述React组件加载时生命周期执行顺序，组件更新时生命周期执行顺序。
7.HTTP 状态消息 200 302 304 403 404 500 分别表示什么？
8.请写出ES6中Array.isArray()的代码实现。
/**
 * 判断一个对象是否是数组，参数不是对象或者不是数组，返回false
 * @param {Object} arg 需要测试是否为数组的对象
 * @return {Boolean} 传入参数是数组返回true，否则返回false
 */
 ```
Array.prototype.isArray = function(arg) {
  if (typeof arg === 'object') {
    return Object.prototype.toString.call(arg) === '[object Array]';
  }
  return false;
}
```

大写数字
```
function accMul(arg1, arg2) {
  let m = 0;
  const s1 = arg1.toString();
  const s2 = arg2.toString();
  m += s1.split('.').length > 1 ? s1.split('.')[1].length : 0;
  m += s2.split('.').length > 1 ? s2.split('.')[1].length : 0;
  return (Number(s1.replace('.', '')) * Number(s2.replace('.', ''))) / 10 ** m;
}

export function digitUppercase(n) {
  const fraction = ['角', '分'];
  const digit = ['零', '壹', '贰', '叁', '肆', '伍', '陆', '柒', '捌', '玖'];
  const unit = [['元', '万', '亿'], ['', '拾', '佰', '仟', '万']];
  let num = Math.abs(n);
  let s = '';
  fraction.forEach((item, index) => {
    s += (digit[Math.floor(accMul(num, 10 * 10 ** index)) % 10] + item).replace(/零./, '');
  });
  s = s || '整';
  num = Math.floor(num);
  for (let i = 0; i < unit[0].length && num > 0; i += 1) {
    let p = '';
    for (let j = 0; j < unit[1].length && num > 0; j += 1) {
      p = digit[num % 10] + unit[1][j] + p;
      num = Math.floor(num / 10);
    }
    s = p.replace(/(零.)*零$/, '').replace(/^$/, '零') + unit[0][i] + s;
  }

  return s
    .replace(/(零.)*零元/, '元')
    .replace(/(零.)+/g, '零')
    .replace(/^整$/, '零元整');
}


```
### >>> 无符号右移0
本质上就是保证x有意义（为数字类型），且为正整数，在有效的数组范围内（0 ～ 0xFFFFFFFF），且在无意义的情况下缺省值为0。
1、如果不能转换为Number，那就为0
2、如果为非整数，先转换为整数
  ```
  function ToInteger(x) {
    x = Number(x);
    return x < 0 ? Math.ceil(x) : Math.floor(x);
  }
  ```
3、如果是正数，返回正数，如果是负数，返回负数 + 2的32次方
    ```
    function modulo(a, b) {
        return a - Math.floor(a/b)*b;
    }
    function ToUint32(x) {
        return modulo(ToInteger(x), Math.pow(2, 32));
    }
    ```
随机颜色
```
// 生成随机颜色
      for ( var i = 0; i < count; i++ )  {
        colors.push( 
          'rgb( ' + 
            ( Math.random() * 255 >> 0 ) + ',' +   //>>>是无符号右移，>>是有符号移位
            ( Math.random() * 255 >> 0 ) + ',' +  //移位0,一将不是number类型的数据转换为number;二将number转换为整数
            ( Math.random() * 255 >> 0 ) +       //一个小于255的随机数
          ' )'
        );
    }
```
