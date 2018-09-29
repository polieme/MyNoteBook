> ### 1. 业务页面JSP(goods_detail_edit.jsp)
```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
<%
	String path = request.getContextPath();
    String basePath = request.getScheme() + "://" + request.getServerName() + ":" + request.getServerPort() + path + "/";
%>
<!DOCTYPE html>
<html lang="en">
<head>
<base href="<%=basePath%>">
<meta charset="utf-8" />
<title></title>
<meta name="description" content="overview & stats" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<link href="static/css/bootstrap.min.css" rel="stylesheet" />
<link href="static/css/bootstrap-responsive.min.css" rel="stylesheet" />
<link rel="stylesheet" href="static/css/font-awesome.min.css" />
<!-- 下拉框 -->
<link rel="stylesheet" href="static/css/chosen.css" />
<link rel="stylesheet" href="static/css/ace.min.css" />
<link rel="stylesheet" href="static/css/ace-responsive.min.css" />
<link rel="stylesheet" href="static/css/ace-skins.min.css" />
<script type="text/javascript" src="static/js/jquery-1.7.2.js"></script>
<!--提示框-->
<script type="text/javascript" src="static/js/jquery.tips.js"></script>
<!-- 上传图片 -->
<link rel="stylesheet" type="text/css" href="plugins/webuploader/webuploader.css" />
<link rel="stylesheet" type="text/css" href="plugins/webuploader/style.css" />
<style type="text/css">
td input {
	width: 97%;
}

tr th {
	font-size: 13px;
	font-weight: bold;
	vertical-align: middle;
}

#wrapper {
	margin: 0;
}

#uploader .placeholder {
	background: url(plugins/webuploader/image.png) center 23px no-repeat;
	padding-top: 88px;
	min-height: 110px;
}
</style>
</head>
<body>
	<form action="goodsDetail/${msg }.do" name="goodsForm" id="goodsForm" method="post">
		<div id="zhongxin">
			<table id="table_report" class="table table-striped table-bordered table-hover">
				<tr>
					<th style="vertical-align: middle">商品编码:</th>
					<td><input type="hidden" id="checkGoodsCode" value="${pd.goods_code}" /> <input type="text" name="GOODS_CODE" id="GOODS_CODE" value="${pd.goods_code}" maxlength="6" placeholder="请输入商品编码"
						title="商品编码" onblur="checkHasCode()" />
					</td>
					<th style="vertical-align: middle">商品类型:</th>
					<td><select class="chzn-select" name="GOODS_TYPE" id="GOODS_TYPE" data-placeholder="请选择商品类型" style="vertical-align:top;width: 42%">
							<option value=""></option>
							<c:forEach items="${cateGoryList}" var="cateGory">
								<option value="${cateGory.GOODS_TYPE}"
									<c:if test="${pd.goods_type==cateGory.GOODS_TYPE}">selected</c:if>>${cateGory.DESCRIPTION }
								</option>
							</c:forEach>
					</select>
					</td>
				</tr>
				<tr>
					<th style="vertical-align: middle">商品名称:</th>
					<td><input type="text" name="GOODS_NAME" id="GOODS_NAME" value="${pd.goods_name }" maxlength="6" placeholder="请输入商品名称" title="商品名称" />
					</td>
					<th style="vertical-align: middle">商品别名:</th>
					<td><input type="text" name="GOODS_ABBR_NAME" id="GOODS_ABBR_NAME" value="${pd.goods_abbr_name }" maxlength="64" placeholder="请输入商品别名" title="商品别名" />
					</td>
				</tr>
				<tr>
					<th style="vertical-align: middle">特殊商品:</th>
					<td style="vertical-align:top;"><select class="chzn-select" name="IS_SPECIAL" id="IS_SPECIAL" data-placeholder="是否特殊商品" style="vertical-align:top;width: 42%">
							<option value=""></option>
							<option value="Y" <c:if test="${pd.is_special=='Y'}">selected</c:if>>特殊商品</option>
							<option value="N" <c:if test="${pd.is_special=='N'}">selected</c:if>>非特殊商品</option>
					</select>
					</td>
					<th style="vertical-align: middle">是否有效:</th>
					<td style="vertical-align:top;"><select class="chzn-select" name="IS_VALID" id="IS_VALID" data-placeholder="是否有效" style="width: 42%">
							<option value=""></option>
							<option value="Y" <c:if test="${pd.is_valid=='Y'}">selected</c:if>>有效</option>
							<option value="N" <c:if test="${pd.is_valid=='N'}">selected</c:if>>无效</option>
					</select>
					</td>
				</tr>
				<tr>
					<th style="vertical-align: middle">菜单编码:</th>
					<td><input type="text" name="MENU_CODE" id="MENU_CODE" value="${pd.menu_code }" maxlength="6" placeholder="请输入菜单编码" title="菜单编码" />
					</td>
				</tr>
				<tr>
					<td colspan="4"><textarea name="GOODS_DESC" id="GOODS_DESC" rows="5" cols="50" style="width:99%;" placeholder="请选输入商品描述" title="请选输入商品描述">${pd.goods_desc}</textarea>
					</td>
				</tr>
				<tr>
					<td colspan="4"><input type="hidden" name="FILE_PATH" id="FILE_PATH" value="${pd.FILE_PATH}" />
						<div id="wrapper">
							<div id="container"  class="uploadFile">
								<!--头部，相册选择和格式选择-->
									<div id="uploader">
										<div class="queueList">
											<div id="dndArea" class="placeholder">
												<div id="filePicker"></div>
												<p>或将照片拖到这里，单次最多可选5张</p>
											</div>
										</div>
										<div class="statusBar" style="display:none;">
											<div class="progress">
												<span class="text">0%</span> <span class="percentage"></span>
											</div>
											<div class="info"></div>
											<div class="btns">
												<div id="filePicker2"></div>
												<div class="uploadBtn">开始上传</div>
											</div>
										</div>
									</div>
							</div>
						</div>
					</td>
				</tr>
				<tr>
					<td colspan="4"><input type="hidden" name="detail_image_url" id="detail_image_url" value="${pd.detail_image_url}" />
						<div id="wrapper">
							<div id="container" class="uploadFile">
								<!--头部，相册选择和格式选择-->
									<div id="uploader">
										<div class="queueList">
											<div id="dndArea" class="placeholder">
												<div id="filePickerDetail"></div>
												<p>或将照片拖到这里，单次最多可选5张</p>
											</div>
										</div>
										<div class="statusBar" style="display:none;">
											<div class="progress">
												<span class="text">0%</span> <span class="percentage"></span>
											</div>
											<div class="info"></div>
											<div class="btns">
												<div id="filePicker2"></div>
												<div class="uploadBtn">开始上传</div>
											</div>
										</div>
									</div>
							</div>
						</div>
					</td>
				</tr>
				<tr>
					<td style="text-align: center;" colspan="4">
						<a class="btn btn-mini btn-primary" onclick="save();">保存</a> <a class="btn btn-mini btn-danger" onclick="top.Dialog.close();">取消</a>
					</td>
				</tr>
			</table>

		</div>
		<div id="zhongxin2" class="center" style="display:none">
			<br /> <br /> <br /> <br /> <img src="static/images/jiazai.gif" /><br />
			<h4 class="lighter block green"></h4>
		</div>

	</form>

	<!-- 引入 -->
	<script type="text/javascript">window.jQuery || document.write("<script src='static/js/jquery-1.9.1.min.js'>\x3C/script>");</script>
	<script src="static/js/bootstrap.min.js"></script>
	<script src="static/js/ace-elements.min.js"></script>
	<script src="static/js/ace.min.js"></script>
	<script type="text/javascript" src="static/js/chosen.jquery.min.js"></script>
	<!-- 下拉框 -->

	<script type="text/javascript" src="plugins/webuploader/webuploader.js"></script>
	<script src="static/js/goods/goods_detail_edit.js"></script>

	<script type="text/javascript">
		
		$(function() {
			//单选框
			$(".chzn-select").chosen(); 
			$(".chzn-select-deselect").chosen({allow_single_deselect:true}); 
		});
		
	$(top.hangge());
	$(document).ready(function(){
		if($("#user_id").val()!=""){
			$("#loginname").attr("readonly","readonly");
			$("#loginname").css("color","gray");
		}
	});
	
	//保存
	function save(){
		//验证商品编码是否为空
		if($("#GOODS_CODE").val()==""){
			$("#GOODS_CODE").tips({
				side:3,
	            msg:'请输入商品编码',
	            bg:'#AE81FF',
	            time:2
	        });
			
			$("#GOODS_CODE").focus();
			return false;
		}
		if($("#GOODS_NAME").val()==""){
			$("#GOODS_NAME").tips({
				side:3,
	            msg:'请输入商品名称',
	            bg:'#AE81FF',
	            time:2
	        });
			
			$("#GOODS_NAME").focus();
			return false;
		}
		if($("#GOODS_ABBR_NAME").val()==""){
			$("#GOODS_ABBR_NAME").tips({
				side:3,
	            msg:'请输入商品别名',
	            bg:'#AE81FF',
	            time:2
	        });
			
			$("#GOODS_ABBR_NAME").focus();
			return false;
		}
		//保存之前处理图片数据
		var lbfiles = uploader[0].getFiles("complete");//轮播图
		var lbFilesUrl="";
		$(lbfiles).each(function(index,item){
			lbFilesUrl = lbFilesUrl+";"+item.url; 
		});
		$("#FILE_PATH")[0].value = lbFilesUrl;
		//保存之前处理图片数据
		var detailfiles = uploader[1].getFiles("complete");//商品详情图
		var detailFilesUrl="";
		$(detailfiles).each(function(index,item){
			detailFilesUrl = detailFilesUrl+";"+item.url; 
		});
		$("#detail_image_url")[0].value = detailFilesUrl;
		
		$("#goodsForm").submit();
		$("#zhongxin").hide();
		$("#zhongxin2").show();
	}
	
	//校验编码是否存在
	function checkHasCode(){
		var goodsCode = $("#GOODS_CODE")[0].value;
		var checkGoodsCode = $("#checkGoodsCode")[0].value;
		
		if(goodsCode == checkGoodsCode)return;
		
		$.ajax({
			type: "GET",
			url: '<%=basePath%>goodsDetail/hasCode.do?tm='+new Date().getTime() + '&GOODS_CODE=' + goodsCode,
				data : '',
				dataType : 'json',
				cache : false,
				success : function(data) {
					if (data.result == "error") {
						alert("编码重复，请重新输入");
						$("#GOODS_CODE")[0].value = checkGoodsCode;
					};
				}
			});
		};
	</script>
</body>
</html>
```
> #### 1.1 对应上传的js(goods_detail_edit.js)
```js
(function($){
	
    // 当domReady的时候开始初始化
    $(function() {
    	uploader = new Array();//创建 uploader数组
    	// 判断浏览器是否支持图片的base64
        var isSupportBase64 = ( function() {
            var data = new Image();
            var support = true;
            data.onload = data.onerror = function() {
                if( this.width != 1 || this.height != 1 ) {
                    support = false;
                }
            };
            data.src = "data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///ywAAAAAAQABAAACAUwAOw==";
            return support;
        } )(),

        // 检测是否已经安装flash，检测flash的版本
        flashVersion = ( function() {
            var version;

            try {
                version = navigator.plugins[ 'Shockwave Flash' ];
                version = version.description;
            } catch ( ex ) {
                try {
                    version = new ActiveXObject('ShockwaveFlash.ShockwaveFlash')
                            .GetVariable('$version');
                } catch ( ex2 ) {
                    version = '0.0';
                }
            }
            version = version.match( /\d+/g );
            return parseFloat( version[ 0 ] + '.' + version[ 1 ], 10 );
        } )(),

        supportTransition = (function(){
            var s = document.createElement('p').style,
                r = 'transition' in s ||
                        'WebkitTransition' in s ||
                        'MozTransition' in s ||
                        'msTransition' in s ||
                        'OTransition' in s;
            s = null;
            return r;
        })();
        if ( !WebUploader.Uploader.support('flash') && WebUploader.browser.ie ) {

            // flash 安装了但是版本过低。
            if (flashVersion) {
                (function(container) {
                    window['expressinstallcallback'] = function( state ) {
                        switch(state) {
                            case 'Download.Cancelled':
                                alert('您取消了更新！');
                                break;

                            case 'Download.Failed':
                                alert('安装失败');
                                break;

                            default:
                                alert('安装已成功，请刷新！');
                                break;
                        }
                        delete window['expressinstallcallback'];
                    };

                    var swf = './expressInstall.swf';
                    // insert flash object
                    var html = '<object type="application/' +
                            'x-shockwave-flash" data="' +  swf + '" ';

                    if (WebUploader.browser.ie) {
                        html += 'classid="clsid:d27cdb6e-ae6d-11cf-96b8-444553540000" ';
                    }

                    html += 'width="100%" height="100%" style="outline:0">'  +
                        '<param name="movie" value="' + swf + '" />' +
                        '<param name="wmode" value="transparent" />' +
                        '<param name="allowscriptaccess" value="always" />' +
                    '</object>';

                    container.html(html);

                })($wrap);

            // 压根就没有安转。
            } else {
                $wrap.html('<a href="http://www.adobe.com/go/getflashplayer" target="_blank" border="0"><img alt="get flash player" src="http://www.adobe.com/macromedia/style_guide/images/160x41_Get_Flash_Player.jpg" /></a>');
            }

            return;
        } else if (!WebUploader.Uploader.support()) {
            alert( 'Web Uploader 不支持您的浏览器！');
            return;
        }
        
        
        
        
        
        
    	$('.uploadFile').each(function(index){
    		var $wrap = $('#uploader')[index],
            // 图片容器
            $queue = $( '<ul class="filelist"></ul>' ).appendTo( $(this).find( '.queueList' ) ),
            // 状态栏，包括进度和控制按钮
            $statusBar = $(this).find( '.statusBar' ),
            // 文件总体选择信息。
            $info = $statusBar.find( '.info' ),
            // 上传按钮
            $upload =  $(this).find( '.uploadBtn' ),
            // 没选择文件之前的内容。
            $placeHolder =  $(this).find( '.placeholder' ),
            $progress = $statusBar.find( '.progress' ).hide(),
            // 添加的文件数量
            fileCount = 0,
            // 添加的文件总大小
            fileSize = 0,
            // 优化retina, 在retina下这个值是2
            ratio = window.devicePixelRatio || 1,
            // 缩略图大小
            thumbnailWidth = 110 * ratio,
            thumbnailHeight = 110 * ratio,

            // 可能有pedding, ready, uploading, confirm, done.
            state = 'pedding',

            // 所有文件的进度信息，key为file id
            percentages = {};

        

        
        var locat = (window.location+'').split('/'); 
    	if('pictures'== locat[3]){locat =  locat[0]+'//'+locat[2];}else{locat =  locat[0]+'//'+locat[2]+'/'+locat[3];};
    	uploader[index] = WebUploader.create({
            pick: {
                id: index==0?'#filePicker':'#filePickerDetail',
                label: '点击选择图片'
            },
            dnd: '#dndArea',
            swf: './Uploader.swf',
            chunked: false,
            chunkSize: 512 * 1024,
            //server: 'http://127.0.0.1:8080/pictures/save.do',
            server: 'goodsDetail/uploadImg.do?',
            //runtimeOrder: 'flash',

            accept: {
                 title: 'Images',
                 extensions: 'gif,jpg,jpeg,bmp,png',
                 mimeTypes: 'image/*'
             },

            // 禁掉全局的拖拽功能。这样不会出现图片拖进页面的时候，把图片打开。
            disableGlobalDnd: true,
            fileNumLimit: index==0?5:1,
            fileSizeLimit: 200 * 1024 * 1024,    // 200 M
            fileSingleSizeLimit: 50 * 1024 * 1024    // 50 M
        });

        // 拖拽时不接受 js, txt 文件。
        uploader[index].on( 'dndAccept', function( items ) {
            var denied = false,
                len = items.length,
                i = 0,
                // 修改js类型
                unAllowed = 'text/plain;application/javascript ';

            for ( ; i < len; i++ ) {
                // 如果在列表里面
                if ( ~unAllowed.indexOf( items[ i ].type ) ) {
                    denied = true;
                    break;
                }
            }

            return !denied;
        });

        // uploader.on('filesQueued', function() {
        //     uploader.sort(function( a, b ) {
        //         if ( a.name < b.name )
        //           return -1;
        //         if ( a.name > b.name )
        //           return 1;
        //         return 0;
        //     });
        // });

        // 添加“添加文件”的按钮，
        if(index==0){
        	uploader[index].addButton({
        		id: '#filePicker2',
        		label: '继续添加'
        	});
        }

		 var getFileBlob = function(url, cb) {
			var xhr = new XMLHttpRequest();
			xhr.open("GET", url);
			xhr.responseType = "blob";
			xhr.addEventListener('load', function() {
				cb(xhr.response);
			});
			xhr.send();
		};

		var blobToFile = function(blob, name) {
			blob.lastModifiedDate = new Date();
			blob.name = name;
			return blob;
		};

		var getFileObject = function(filePathOrUrl, cb) {
			getFileBlob(filePathOrUrl, function(blob) {
				cb(blobToFile(blob, 'test.jpg'));
			});
		};

		//回显图片
        uploader[index].on('ready', function() {
            window.uploader = uploader;
            var filePathArg = index==0?$("#FILE_PATH")[0].value.split(';'):$("#detail_image_url")[0].value.split(';'); 
            var files=new Array();
            var i=0;
            if(filePathArg.length>0){
			$.each(filePathArg, function(tempindex,item) {
				//如果图片是空值，就直接返回
				if(item==''||item=="undefined"||item==undefined){
					return true;
				}
				getFileObject(item, function(fileObject) {
					var wuFile = new WebUploader.Lib.File(WebUploader.guid('rt_'), fileObject);
					var tempfile = new WebUploader.File(wuFile);
					tempfile.url=item;
					tempfile.setStatus('complete');
					uploader[index].addFiles(tempfile);
				});
			});
            };
        });

        
        uploader[index].on( 'uploadSuccess', function( file,response ) {
        	file.url=response.path;
        	if(index==0){
        		$("#FILE_PATH")[0].value = $("#FILE_PATH")[0].value+";"+response.path;
        	}else{
        		$("#detail_image_url")[0].value = $("#detail_image_url")[0].value+";"+response.path;
        	}
        });
        
        
        
        // 当有文件添加进来时执行，负责view的创建
        function addFile( file ) {
            var $li = $( '<li id="' + file.id + '">' +
                    '<p class="title">' + file.name + '</p>' +
                    '<p class="imgWrap"></p>'+
                    '<p class="progress"><span></span></p>' +
                    '</li>' ),

                $btns = $('<div class="file-panel">' +
                    '<span class="cancel">删除</span>' +
                    '<span class="rotateRight">向右旋转</span>' +
                    '<span class="rotateLeft">向左旋转</span></div>').appendTo( $li ),
                $prgress = $li.find('p.progress span'),
                $wrap = $li.find( 'p.imgWrap' ),
                $info = $('<p class="error"></p>'),

                showError = function( code ) {
                    switch( code ) {
                        case 'exceed_size':
                            text = '文件大小超出';
                            break;

                        case 'interrupt':
                            text = '上传暂停';
                            break;

                        default:
                            text = '上传失败，请重试';
                            break;
                    }

                    $info.text( text ).appendTo( $li );
                };

            if ( file.getStatus() === 'invalid' ) {
                showError( file.statusText );
            } else {
                // @todo lazyload
                $wrap.text( '预览中' );
                uploader[index].makeThumb( file, function( error, src ) {
                    var img;

                    if ( error ) {
                        $wrap.text( '不能预览' );
                        return;
                    }

                    if( isSupportBase64 ) {
                        img = $('<img src="'+src+'">');
                        $wrap.empty().append( img );
                    } else {
                        $.ajax('../../server/preview.php', {
                            method: 'POST',
                            data: src,
                            dataType:'json'
                        }).done(function( response ) {
                            if (response.result) {
                                img = $('<img src="'+response.result+'">');
                                $wrap.empty().append( img );
                            } else {
                                $wrap.text("预览出错");
                            }
                        });
                    }
                }, thumbnailWidth, thumbnailHeight );

                percentages[ file.id ] = [ file.size, 0 ];
                file.rotation = 0;
            }

            file.on('statuschange', function( cur, prev ) {
                if ( prev === 'progress' ) {
                    $prgress.hide().width(0);
                } else if ( prev === 'queued' ) {
                    $li.off( 'mouseenter mouseleave' );
                    $btns.remove();
                }

                // 成功
                if ( cur === 'error' || cur === 'invalid' ) {
                    console.log( file.statusText );
                    showError( file.statusText );
                    percentages[ file.id ][ 1 ] = 1;
                } else if ( cur === 'interrupt' ) {
                    showError( 'interrupt' );
                } else if ( cur === 'queued' ) {
                    percentages[ file.id ][ 1 ] = 0;
                } else if ( cur === 'progress' ) {
                    $info.remove();
                    $prgress.css('display', 'block');
                } else if ( cur === 'complete' ) {
                    $li.append( '<span class="success"></span>' );
                }

                $li.removeClass( 'state-' + prev ).addClass( 'state-' + cur );
            });

            $li.on( 'mouseenter', function() {
                $btns.stop().animate({height: 30});
            });

            $li.on( 'mouseleave', function() {
                $btns.stop().animate({height: 0});
            });

            $btns.on( 'click', 'span', function() {
                var tempIndex = $(this).index(),
                    deg;

                switch ( tempIndex ) {
                    case 0:
                        uploader[index].removeFile( file );
                        return;

                    case 1:
                        file.rotation += 90;
                        break;

                    case 2:
                        file.rotation -= 90;
                        break;
                }

                if ( supportTransition ) {
                    deg = 'rotate(' + file.rotation + 'deg)';
                    $wrap.css({
                        '-webkit-transform': deg,
                        '-mos-transform': deg,
                        '-o-transform': deg,
                        'transform': deg
                    });
                } else {
                    $wrap.css( 'filter', 'progid:DXImageTransform.Microsoft.BasicImage(rotation='+ (~~((file.rotation/90)%4 + 4)%4) +')');
                    // use jquery animate to rotation
                    // $({
                    //     rotation: rotation
                    // }).animate({
                    //     rotation: file.rotation
                    // }, {
                    //     easing: 'linear',
                    //     step: function( now ) {
                    //         now = now * Math.PI / 180;

                    //         var cos = Math.cos( now ),
                    //             sin = Math.sin( now );

                    //         $wrap.css( 'filter', "progid:DXImageTransform.Microsoft.Matrix(M11=" + cos + ",M12=" + (-sin) + ",M21=" + sin + ",M22=" + cos + ",SizingMethod='auto expand')");
                    //     }
                    // });
                }


            });

            $li.appendTo( $queue );
        }

        // 负责view的销毁
        function removeFile( file ) {
            var $li = $('#'+file.id);

            delete percentages[ file.id ];
            updateTotalProgress();
            $li.off().find('.file-panel').off().end().remove();
        }

        function updateTotalProgress() {
            var loaded = 0,
                total = 0,
                spans = $progress.children(),
                percent;

            $.each( percentages, function( k, v ) {
                total += v[ 0 ];
                loaded += v[ 0 ] * v[ 1 ];
            } );

            percent = total ? loaded / total : 0;


            spans.eq( 0 ).text( Math.round( percent * 100 ) + '%' );
            spans.eq( 1 ).css( 'width', Math.round( percent * 100 ) + '%' );
            updateStatus();
        }

        function updateStatus() {
            var text = '', stats;

            if ( state === 'ready' ) {
                text = '选中' + fileCount + '张图片，共' +
                        WebUploader.formatSize( fileSize ) + '。';
            } else if ( state === 'confirm' ) {
                stats = uploader[index].getStats();
                if ( stats.uploadFailNum ) {
                    text = '已成功上传' + stats.successNum+ '张照片至XX相册，'+
                        stats.uploadFailNum + '张照片上传失败，<a class="retry" href="#">重新上传</a>失败图片或<a class="ignore" href="#">忽略</a>';
                }

            } else {
                stats = uploader[index].getStats();
                text = '共' + fileCount + '张（' +
                        WebUploader.formatSize( fileSize )  +
                        '），已上传' + stats.successNum + '张';

                if ( stats.uploadFailNum ) {
                    text += '，失败' + stats.uploadFailNum + '张';
                }
            }

            $info.html( text );
        }

        function setState( val ) {
            var file, stats;

            if ( val === state ) {
                return;
            }

            $upload.removeClass( 'state-' + state );
            $upload.addClass( 'state-' + val );
            state = val;

            switch ( state ) {
                case 'pedding':
                    $placeHolder.removeClass( 'element-invisible' );
                    $queue.hide();
                    $statusBar.addClass( 'element-invisible' );
                    uploader[index].refresh();
                    break;

                case 'ready':
                    $placeHolder.addClass( 'element-invisible' );
                    $( '#filePicker2' ).removeClass( 'element-invisible');
                    $queue.show();
                    $statusBar.removeClass('element-invisible');
                    uploader[index].refresh();
                    break;

                case 'uploading':
                    $( '#filePicker2' ).addClass( 'element-invisible' );
                    $progress.show();
                    $upload.text( '暂停上传' );
                    break;

                case 'paused':
                    $progress.show();
                    $upload.text( '继续上传' );
                    break;

                case 'confirm':
                    $progress.hide();
                    $( '#filePicker2' ).removeClass( 'element-invisible' );
                    $upload.text( '开始上传' );

                    stats = uploader[index].getStats();
                    if ( stats.successNum && !stats.uploadFailNum ) {
                        setState( 'finish' );
                        return;
                    }
                    break;
                case 'finish':
                    stats = uploader[index].getStats();
                    if ( stats.successNum ) {
                        //alert( '上传成功' );
                    } else {
                        // 没有成功的图片，重设
                        state = 'done';
                        location.reload();
                    }
                    break;
            }

            updateStatus();
        }

        uploader[index].onUploadProgress = function( file, percentage ) {
            var $li = $('#'+file.id),
                $percent = $li.find('.progress span');

            $percent.css( 'width', percentage * 100 + '%' );
            percentages[ file.id ][ 1 ] = percentage;
            updateTotalProgress();
        };

        uploader[index].onFileQueued = function( file ) {
            fileCount++;
            fileSize += file.size;

            if ( fileCount === 1 ) {
                $placeHolder.addClass( 'element-invisible' );
                $statusBar.show();
            }

            addFile( file );
            setState( 'ready' );
            updateTotalProgress();
        };

        uploader[index].onFileDequeued = function( file ) {
            fileCount--;
            fileSize -= file.size;
            debugger;
            if ( !fileCount ) {
                setState( 'pedding' );
            }
            removeFile(file);
            updateTotalProgress();
        };

        uploader[index].on( 'all', function( type ) {
            var stats;
            switch( type ) {
                case 'uploadFinished':
                    setState( 'confirm' );
                    break;

                case 'startUpload':
                    setState( 'uploading' );
                    break;

                case 'stopUpload':
                    setState( 'paused' );
                    break;

            }
        });

        uploader[index].onError = function( code ) {
        	if(code == 'F_DUPLICATE'){
        		alert( '图片重复' );
            }else{
            	alert( 'Eroor: ' + code );
            }
        };

        $upload.on('click', function() {
            if ( $(this).hasClass( 'disabled' ) ) {
                return false;
            }

            if ( state === 'ready' ) {
                uploader[index].upload();
            } else if ( state === 'paused' ) {
                uploader[index].upload();
            } else if ( state === 'uploading' ) {
                uploader[index].stop();
            }
        });

        $info.on( 'click', '.retry', function() {
            uploader[index].retry();
        } );

        $info.on( 'click', '.ignore', function() {
            alert( 'todo' );
        } );

        $upload.addClass( 'state-' + state );
        updateTotalProgress();
    	});
    });
})( jQuery );
```

> ### 2.后台代码
> 上传图片
```java
	/**
	 * 上传图片
	 */
	@RequestMapping(value="/uploadImg")
	@ResponseBody
	public Object save(@RequestParam(required=false) MultipartFile file,String goodsCode) throws Exception{
		logBefore(logger, "GoodsDetail上传图片");
		Map<String,String> map = new HashMap<String,String>();
//		String  ffile = DateUtil.getDays(), fileName = "";
		PageData pd = new PageData();
		String imageUrls = "";
		if(Jurisdiction.buttonJurisdiction(menuUrl, "add")){
			if (null != file && !file.isEmpty()) {
				//上传图片到FastDFS
				MultipartFile[] files = new MultipartFile[1];
				files[0] = file;
				imageUrls = fastDFSService.upload(files);
//				String filePath = PathUtil.getClasspath() + Const.FILEPATHIMG + ffile;		//文件上传路径
//				fileName = FileUpload.fileUp(file, filePath, this.get32UUID());				//执行上传
			}else{
				System.out.println("上传失败");
			}
		}
		map.put("result", "ok");
//		map.put("path", ffile + "/" + fileName);
		map.put("path", imageUrls);
		return AppUtil.returnObject(pd, map);
	}
```
保存图片路径
```java
/**
	 * 保存商品基础信息
	 */
	@RequestMapping(value="/save")
	public ModelAndView save() throws Exception{
		ModelAndView mv = this.getModelAndView();
		PageData pd = new PageData();
		pd = this.getPageData();
		DateFormat df = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		//首先判断是否有主键goods_code
		String goodsCode = pd.getString("GOODS_CODE");
		if(goodsCode!=null && !"".equals(goodsCode)){//如果不为空，走update语句
			String filePath = pd.getString("FILE_PATH")==null?"":pd.getString("FILE_PATH").toString();//图片路径
			String[] filePathArg = filePath.split(";");
			String imageUrl1 = filePathArg!=null&&filePathArg.length>1?filePathArg[1]:"";
			String imageUrl2 = filePathArg!=null&&filePathArg.length>2?filePathArg[2]:"";
			String imageUrl3 = filePathArg!=null&&filePathArg.length>3?filePathArg[3]:"";
			String imageUrl4 = filePathArg!=null&&filePathArg.length>4?filePathArg[4]:"";
			String imageUrl5 = filePathArg!=null&&filePathArg.length>5?filePathArg[5]:"";
			String updatedTime = df.format(new Date());
			pd.put("imageUrl1", imageUrl1);
			pd.put("imageUrl2", imageUrl2);
			pd.put("imageUrl3", imageUrl3);
			pd.put("imageUrl4", imageUrl4);
			pd.put("imageUrl5", imageUrl5);
			pd.put("updatedTime", updatedTime);
			
			String detailImageUrl = pd.getString("detail_image_url")==null?"":pd.getString("detail_image_url").toString();//商品详情
			String[] detailImageUrlArg = detailImageUrl.split(";");
			String detailImage = detailImageUrlArg!=null&&detailImageUrlArg.length>1?detailImageUrlArg[1]:"";
			pd.put("detail_image_url", detailImage);
		}else{//如果为空，那就是新增数据

		}
		
		
		if(Jurisdiction.buttonJurisdiction(menuUrl, "edit")){goodsDetailService.save(pd);}
		mv.addObject("msg","success");
		mv.setViewName("save_result");
		return mv;
	}
```