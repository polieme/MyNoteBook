## 效果图

![效果图](https://note.youdao.com/yws/public/resource/76830233cf02d1d76656c9ddfd999350/xmlnote/8B7672764F5F414B8FDCA1930376777D/7836)

---

## HTML代码
```html
<button id="searchTypeBtn"  class="btn btn-default" type="button" style="padding: 2px;margin-left:2px;background-color: #000 !important">
	<i class="glyphicon glyphicon-sort" style="margin-left:3px"></i>
	<div class="searchType" style="z-index:99;position: absolute;width: 97px;left: -70px;top: 25px;display: none;color:#000;background-color: #fff;border: 1px solid #eee">
    	<table class="layui-table" style="margin:0px">
    		<c:choose>
				<c:when test="${not empty moduleTypeList}">
					<c:forEach items="${moduleTypeList}" var="moduleType" varStatus="vs">
						<tr onclick="updateModuleList('${moduleType.CODE_VALUE}')"><td style="text-align: center;">${moduleType.CODE_NAME}</td></tr>
					</c:forEach>
				</c:when>
			</c:choose>
		</table>
	</div>
</button>
```
---

## JS代码

```js
$(function(){
	$("#searchTypeBtn").hover(
		function(){
			$(".searchType").slideDown(400);
		},
		function(){
			$(".searchType").slideUp(400);
		}
	);
});
```

