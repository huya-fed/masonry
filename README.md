masonry
=========

> 瀑布流

> 该插件是v2.1.08的，兼容IE7的版本，下面的官网是兼容IE8+以上的，所以没有用到

> http://masonry.desandro.com/
> 
> http://www.css88.com/archives/3321


----------

##html结构

	<div class="grid">
	  <div class="grid-item">...</div>
	  <div class="grid-item grid-item--width2">...</div>
	  <div class="grid-item">...</div>
	  ...
	</div>


##CSS

	.grid-item { width: 200px; }
	.grid-item--width2 { width: 400px; }



##基于jq的初始化

	require('masonry');
	$('.grid').masonry({
	  // 元素
	  itemSelector: '.grid-item',
	  //间距
	  gutterWidth: 4
	});


##基于原生的javascript
		
	<script type="text/javascript">	
		var flag = true;
		$(function(){			
			var $container = $('#listing');    
			$container.masonry({
				singleMode: true,
				animate: true,
				itemSelector: '.post'
			});		
			//滚动条滚动到离底部距离50的时候触发
			$(window).scroll(function(){
				// 当滚动到最底部以上100像素时， 加载新内容
				if ($(document).height() - $(this).scrollTop() - $(this).height()<50){	
					if (flag){
						var $boxes = $(getList());	 
						$container.append($boxes).masonry('appended',$boxes);
					}
				}
			});	
		});	
		//测试获取列表
		function getList() {	
			var boxes = [],count = parseInt(Math.random()*10); 
			for (var i=0; i < count; i++ ) {
				boxes.push('<div class="post"><a href="#"><img src="images/'+(i+1)+'.jpg" width="280" alt="" /></a><a href="#" target="_blank">图片'+(i+1)+'</a></div>');
			}
			//把数组转成字符串
			return boxes.join("");
		};
	</script>

##注意点，图片没有加载成功，获取不到宽和高，会导致布局乱，得引用imagesLoaded插件

	
	require('imagesLoaded');
	$grid.imagesLoaded(function() {
		$grid.masonry({
			// options
			itemSelector: '.grid-item',
			gutterWidth : 4
		});
	});
