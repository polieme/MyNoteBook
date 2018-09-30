> layui是非模块化引入的
```html
<link rel="stylesheet" href="plugins/layuiv-2.3.0/css/layui.css">
**********************
页面代码
*********************
<script type="text/javascript" src="plugins/layuiv-2.3.0/layui.all.js"></script>
```

## html代码
```html
<div class="layui-inline">
	<label class="layui-form-label">审批意见</label>
	<div class="layui-input-inline">
		<select name="APPVTYPE" lay-filter="appvtype" lay-verify="required" lay-search="">
			<option value=""></option>
			<c:choose>
				<c:when test="${not empty appvTypeList}">
					<c:forEach items="${appvTypeList}" var="appvType" varStatus="vs">
						<option value="${appvType.APPR_CODE}">${appvType.APPR_NAME}</option>
					</c:forEach>
				</c:when>
			</c:choose>
		</select>
	</div>
</div>
<div class="layui-inline">
	<label class="layui-form-label">拒件理由</label>
	<div class="layui-input-inline">
		<select name="REFUSALREG" lay-verify="required" lay-search="" disabled="">
			<option value=""></option>
			<c:choose>
				<c:when test="${not empty refusalRegList}">
					<c:forEach items="${refusalRegList}" var="refusalReg" varStatus="vs">
						<option value="${refusalReg.CODE_VALUE}">${refusalReg.CODE_NAME}</option>
					</c:forEach>
				</c:when>
			</c:choose>
		</select>
	</div>
</div>
<div class="layui-inline">
	<div class="layui-input-block">
		<input type="checkbox" name="like1[write]" lay-skin="primary" title="加入黑名单" disabled="" id="BLACKLIST">
	</div>
</div>
```

## js代码（一定要注意下面的重新渲染）
```js
var form = layui.form;//初始化form
form.on('select(appvtype)', function(data){//监听下拉框onchange
	if(data.value=="02"){
		$("select[name^='REFUSALREG']").removeAttr("disabled");//设置下拉框为非只读
		$("#BLACKLIST").removeAttr("disabled");//设置复选框为非只读
		form.render();//重新渲染所有元素（必须得进行重新渲染，要不没法正常显示）
	}else{
		$("select[name^='REFUSALREG']").attr("disabled","disabled");//设置下拉框为只读
		$("#BLACKLIST").attr("disabled","disabled");//设置复选框为只读
		$("select[name^='REFUSALREG']").val("");//清空下拉框选中的值
		$("#BLACKLIST").prop("checked",false);//清空复选框选中的值
		form.render();//重新渲染所有元素（必须得重新渲染，要不没法正常显示）
	}
});
```