# CSS模糊筛选器
```js
<!--p是标签的类型，class是标签的属性，important是需要模糊查询的内容-->
p[class~="important"] {color: red;}
```

```js
div[id^="filePicker"]{
	width: 200px;
}
```
```js
img[title~="Figure"] {border: 1px solid gray;}
```
| 类型         | 描述                                       |
| ------------ | ------------------------------------------ |
| [abc^="def"] | 选择 abc 属性值以 "def" 开头的所有元素     |
| [abc$="def"] | 选择 abc 属性值以 "def" 结尾的所有元素     |
| [abc*="def"] | 选择 abc 属性值中包含子串 "def" 的所有元素 |

# jquery 给样式添加important的样式
```js
$(".tab_close").css("cssText","display:none !important");
```