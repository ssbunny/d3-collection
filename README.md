# d3-collection

## 源代码

源码获取 key 的方法使用 for in 遍历，因此顺序是未知的。

* [x] keys.js - 返回对象的键构成的数组
* [x] values.js - 返回对象值构成的数组
* [x] entries.js - 返回对象键值对构成的数组
* [x] map.js - 类似 ES6 的 Map
* [x] set.js - 类似 ES6 的 Set
* [x] nest.js - 列表结构转树结构

## Objects

```javascript
var person = {name: 'qiang', age: 30};

d3.keys(person);    // ["name", "age"]
d3.values(person);  // ["qiang", 30]
d3.entries(person); // [{key: "name", value: "qiang"}, {key: "age", value: 30}]
```

## Maps

和 ES6 Map 提供的方法非常类似。

```javascript
var map = d3.map(
    [{name: "foo"}, {name: "bar"}],
    function (d) {
        return d.name;
    }
);
map.get("foo"); // {"name": "foo"}
map.get("bar"); // {"name": "bar"}
map.get("baz"); // undefined

var map2 = d3.map()
    .set("foo", 1)
    .set("bar", 2)
    .set("baz", 3);
map2.get("foo"); // 1
```

## Sets

和 ES6 Set 提供的方法非常类似。

```javascript
var set = d3.set()
    .add("foo")
    .add("bar")
    .add("baz");
set.has("foo"); // true
```

## Nests

用来将列表结构的数组转成树结构。`entries` 和 `object` 两个方法用来返回最终结果。

```javascript
var users = [
    {dep: '001', user: 'zhangsan', age: 30, gender: 'male'},
    {dep: '002', user: 'lise', age: 28, gender: 'male'},
    {dep: '001', user: 'wangwu', age: 32, gender: 'female'},
    {dep: '001', user: 'zhaoliu', age: 28, gender: 'male'},
    {dep: '002', user: 'sunqi', age: 35, gender: 'female'},
    {dep: '003', user: 'zhouba', age: 42, gender: 'female'},
    {dep: '003', user: 'wujiu', age: 34, gender: 'male'},
    {dep: '001', user: 'zhengshi', age: 30, gender: 'male'}
];

var munge = d3.nest()
    .key(function (d) { return d.gender; })
    .key(function (d) { return d.dep; })
    .sortKeys(d3.descending)
    .entries(users);

/* 结果为：
    [{
        key: 'male',
        values: [
            {key: '003', values: ...},
            {key: '002', values: ...},
            {key: '001', values: ...},
        ]
    }, {
        key: 'female',
        values: ...
    }]
*/
```