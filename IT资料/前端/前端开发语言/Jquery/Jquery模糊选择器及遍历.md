## jQuery常规选择器

### 1. 首先是常规使用

#### 选择所有元素
```js
$("*")
$("body *")

$(document).ready(function(){
    $("body *").css("background-color","#B2E0FF");
});

$(function(){
    $("body *").css("background-color","red");
})
```

#### 根据id选择元素
```js
$("#id")

$(document).ready(function(){
   $("#choose").css("background-color","#B2E0FF");
})
```

#### 根据样式class选择元素
该方法常用作选择多个元素
```js
$(".class")

$(document).ready(function(){
    $(".className").css("background-color","red");
})

$(function(){
     $(".className").css("background-color","red");
})
```

#### 获取第一个、最后一个元素
```js
$("p:first")
$("p:last")
```

#### 所有偶数或者所有奇数标签

这里的偶数和奇数是索引，索引是从0开始的，因此第一个偶数就是0
```js
$("tr:even") //偶数
$("tr:odd") //奇数
$("tr:even").css("background-color","#B2E0FF");
```

#### 选择index>n 或者小于n的所有对象
```js
$("ul li:gt(3)")
$("ul li:lt(3)")
$("tr:lt(2)")
```

#### 选择所有不为空的input
```js
$("selector:not(selector)")
$("input:not(:empty)")
$("input:not(:empty)")
```

#### 所有标题元素
```js
$(":header") //所有标题元素 <h1> - <h6>
```

#### 所有动画元素
```js
$(":animated")
```

#### 包含指定字符串的所有元素
```js
$(":contains('W3School')")
$("p:contains(is)")
$("p:contains(is)").css("background-color","#B2E0FF");
$("div:contains(is)").css("background-color","red")
```

#### 所有无子节点的所有元素
```js
$(":empty")
```

#### 所有隐藏的标签
```js
$(":hidden")
$("p:hidden")
```

#### 所有可见表格
```js
$("table:visible")
```

#### 所有带匹配选择的元素
```js
$("th,td,.intro")
```

#### 所有带某个属性的元素
```js
//公式$("[attribute]")
$("[href]")
$("li[name]").css("background-color","#B2E0FF");//li标签中带name属性的
```

#### 所有带某个属性值等于或者不等于XXX的元素
```js
$("[href='#']")
$("input[name='123123']")
$("input[name^='123123']")

$("[name!='123123']")
$("[href!='#']")
```

#### 包含以XXX开头 XXX结尾的元素
```
$("input[name^='aaa']")//以aaa开头的所有input元素
$("input[name$='bbb']")//所有以bbb结尾的input元素
```

#### input的各种类型元素筛选器
```js
$(":input") //	所有 <input> 元素
$(":text") //
$(":password")//
$(":radio")//
$(":checkbox")//
$(":submit")//
$(":reset")//
$(":button")//
$(":image")//
$(":file")//
```

#### 所有激活或者禁用的元素
```js
$(":enabled")
$(":disabled")
```

#### 下拉框选择中被选中的
```
$(":selected")
```

```js
  $(".btn1").click(function(){
    $(":selected").hide();
  });

<select multiple="multiple">
  <option>Volvo</option>
  <option selected="selected">Saab</option>
  <option>Mercedes</option>
  <option>Audi</option>
```
### 单选框、复选框中被选中的
```js
$(":checked").hide();
```

### 2. 模糊选择器

#### 前后缀为XXX的选择器
```js
$("[name^='aaa']")//前缀
$("input[name^='aaa']")//前缀

$("[name$='aaa']")//后缀
$("input[name$='aaa']")//后缀
```

#### name中包含XXX的选择器
```js
$("input[name*='aaaa']")
```
```js
$("input:text[name='xx']") 
```


### 3. 遍历
```js
$("input[name^='aaa']").each(function(i){
    
})
```