```css
	@-webkit-keyframes rotation{
	from {-webkit-transform: rotate(0deg);}
	to {-webkit-transform: rotate(360deg);}
	}
	
	.demo_div{
	-webkit-transform: rotate(360deg);
	animation: rotation 3s linear infinite;
	-moz-animation: rotation 3s linear infinite;
	-webkit-animation: rotation 3s linear infinite;
	-o-animation: rotation 3s linear infinite;
	}

```

使用方法：①新建一个DIV，class="demo_div",div里面放一个图片，就能让图片一直进行旋转了，很好玩