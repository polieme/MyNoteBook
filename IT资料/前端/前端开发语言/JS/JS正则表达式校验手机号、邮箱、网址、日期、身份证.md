## 常规正则表达式
```javascript
验证手机号：/^1\d{10}$/

验证邮箱：/^([a-zA-Z0-9_\.\-])+\@(([a-zA-Z0-9\-])+\.)+([a-zA-Z0-9]{2,4})+$/

验证url：/(^#)|(^http(s*):\/\/[^\s]+\.[^\s]+)/

日期：/^(\d{4})[-\/](\d{1}|0\d{1}|1[0-2])([-\/](\d{1}|0\d{1}|[1-2][0-9]|3[0-1]))*$/

证身份证：/(^\d{15}$)|(^\d{17}(x|X|\d)$)/

中文：[\u4e00-\u9fa5]

电话号码（国内）：[0-9-()（）]{7,18}

邮政编码：\d{6}

IP地址：(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)\.(25[0-5]|2[0-4]\d|[0-1]\d{2}|[1-9]?\d)

正整数：[1-9]\d*

负整数：-[1-9]\d*

用户名：[A-Za-z0-9_\-\u4e00-\u9fa5]+

```
## 使用方法
```javascript
var reg=/(^#)|(^http(s*):\/\/[^\s]+\.[^\s]+)/;
if(!reg.test(data.field.link)){
     layer.msg('外链格式错误，请输入以http://或https://开头的完整url！',{icon: 5});
     return false;
}
```

