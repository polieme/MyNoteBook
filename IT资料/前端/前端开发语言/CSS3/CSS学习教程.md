## CSS3

---

- CSS 用于控制网页的样式和布局。

- CSS3 是最新的 CSS 标准。

- 本教程向您讲解 CSS3 中的新特性

## CSS3 模块

---

CSS3 被划分为模块。

其中最重要的 CSS3 模块包括：

- 选择器
- 框模型
- 背景和边框
- 文本效果
- 2D/3D 转换
- 动画
- 多列布局
- 用户界面

## CSS3 标准

---

W3C 仍然在对 CSS3 规范进行开发。

不过，现代浏览器已经实现了相当多的 CSS3 属性。

## CSS3 边框

---

通过 CSS3，您能够创建圆角边框，向矩形添加阴影，使用图片来绘制边框 - 并且不需使用设计软件，比如 PhotoShop。

在本章中，您将学到以下边框属性：

- border-radius
- box-shadow
- border-image

## CSS3 圆角边框

---

在 CSS2 中添加圆角矩形需要技巧。我们必须为每个圆角使用不同的图片。

在 CSS3 中，创建圆角是非常容易的。

在 CSS3 中，border-radius 属性用于创建圆角：

实例：

```css
div
{
border:2px solid;
border-radius:25px;
-moz-border-radius:25px; /* Old Firefox */
}
```

## CSS3 边框阴影

在 CSS3 中，box-shadow 用于向方框添加阴影：

```css

div{
box-shadow: 10px 10px 5px #888888;//三个参数分别是右边阴影大小，下面阴影大小，模糊距离，阴影颜色
}
```

## CSS3 边框图片

通过 CSS3 的 border-image 属性，您可以使用图片来创建边框：

border-image 属性允许您规定用于边框的图片！

用于创建上面的边框的原始图片：

![](https://github.com/polieme/MyNoteBook/blob/master/%E5%9B%BE%E7%89%87/%E5%89%8D%E7%AB%AF/border.png?raw=true)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>border_img</title>
    <style>
        div {
            border: 15px solid transparent;
            width: 300px;
            padding: 10px 20px;
        }

        #round {
            border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 round;
            -moz-border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 round;
            -webkit-border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 round;
            -o-border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 round;
        }

        #stretch{
            -webkit-border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 stretch;
            -moz-border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 stretch;
            -o-border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 stretch;
            border-image: url(http://www.w3school.com.cn/i/border.png) 30 30 stretch;
        }
    </style>
</head>
<body>
<div id="round">在这里图片铺满整个Border</div>
<br>
<div id="stretch">这个是拉长图片的样式</div>
<br>
<p>这个是我们使用的图片</p>
<img src="http://www.w3school.com.cn/i/border.png">
</body>
</html>
```

