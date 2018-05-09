---
title: jQuery 常用API
date: 2018-03-16 22:42:57
categories: jQuery
tags:
---

#### `jQuery` 选择器

	* $(this) //当前的 HTML 元素。
	* $("p") //所有 <p> 元素。
	* $(".test") //所有 class="test" 的元素。
	* $("#test") // id="test" 的元素。
	* $(":button") //所有 button 元素和类型为 button 的元素。
		//等价于$("button, input[type='button']")

---

#### `jQuery` 事件

	* click(function) //单击元素事件。为 "click" 事件绑定一个函数，每次事件触发时会执行。
	* click() //触发元素上的 "click" 事件。
	* dbclick(function); dbclick()  //双击元素事件。
		//click 事件只能监听鼠标左键。
	
	* mouseenter(function); mouseenter(); //鼠标进入元素事件。
	* mouseleave(function); mouseleave() //鼠标离开元素事件。
	
	* mousedown(function); mousedown() //鼠标进入元素并按下鼠标左键时（按下不松开的过程）触发事件。
	* mouseup(function); mouseup() //当鼠标松开鼠标左键时触发事件。
	
	* hover() //hover()是一个复合方法，相当于 mouseenter + mouseleave 一起使用的情况。

	* focus(function); focus() //当元素获得焦点时触发事件。
	* blur(function); blur() //当元素失去焦点时触发事件。

	* on(event,childSelector,data,function) //在被选元素及子元素上添加一个或多个事件处理程序。
		event //由空格分隔多个事件值，也可以是数组。
		childSelector //规定只能添加到指定的子元素上的事件处理程序
		data //规定传递到函数的额外数据。
		function //规定当事件发生时运行的函数。
	* one() //同 on()，但只触发一次。
	
	//举例 on()
	<script>
		$(document).ready(function(){
		  $("div").on("click","p",function(){
		    $(this).slideToggle();
		  });
		  $("button").click(function(){
		    $("<p>This is a new paragraph.</p>").insertAfter("button");
		  });
		});
	</script>

	
---

#### `jQuery` 隐藏/显示	

	* hide() //隐藏匹配的元素。
	* show() //显示匹配的元素。
		//show() 适用于通过 jQuery 方法和 CSS 中 display:none 隐藏的元素（不适用于通过 visibility:hidden 隐藏的元素）。
		//hide() 和 show() 的执行速度会比直接改变 css 慢。
	* toggle() //添加两个或多个函数，以响应被选元素的 click 事件之间的切换。

---
	
#### `jQuery` 淡入淡出

	 * fadeIn() //逐渐改变被选元素的不透明度，从隐藏到可见（褪色效果）。
	 * fadeOut() //逐渐改变被选元素的不透明度，从可见到隐藏（褪色效果）。
	 * fadeToggle() //在 fadeIn() 和 fadeOut() 方法之间切换。
	 * fadeTo(duration, opacity [, easing ] [, function ]) //调整透明度。
	 	duration //一个字符串或者数字决定动画将运行多久。
	 	opacity //0和1之间的数字表示目标元素的不透明度。
	 	easing //表示动画过渡方式，有 "linear" 和 "swing"。
	 	function //在动画完成时执行的函数。

---

#### `jQuery` 滑动 

	* slideDown() //以滑动方式显示被选元素。
	* slideUp() //以滑动方式隐藏被选元素。
	* slideToggle() //在 slideUp() 和 slideDown() 方法之间切换。

---

#### `jQuery` 动画	
	
	* animate() //通过 CSS 样式将元素从一个状态改变为另一个状态。
	
	//举例
	<script> 
		$("button").click(function(){
			$("#box").animate({height:"300px"});
		});
	</script> 
	//通过改变元素的高度，对元素应用动画。
---

#### `jQuery` 停止动画

	* stop() //停止动画
	
	<script> 
		$(document).ready(function(){
		  $("#flip").click(function(){
		    $("#panel").slideDown(5000);
		  });
		  $("#stop").click(function(){
		    $("#panel").stop();
		  });
		});
	</script>
	

---

#### `jQuery HTML` 获取/设置内容和属性 

	* text() //设置或返回被选元素的文本内容。返回一个字符串。
	* html() //设置或返回被选元素的内容（innerHTML）。
	* val() //返回或设置 value 属性的值。
	* attr() //设置或返回被选元素的属性和值。

	//举例 val()
	<script>
		$(document).ready(function(){
			$("button").click(function(){
				$("input:text").val(function(n,c){
					return c + " Griffin";
				});
			});
		});
	</script>
	
	//举例 attr()
	$("button").click(function(){
		$("img").attr("width","500");
	});
	
---

#### `jQuery HTML` 添加元素/内容
	
	* append() //在被选元素的末尾(添加到元素内部)添加内容。
	* prepend() //在被选元素的开头添加内容。
	
	* after() //在被选元素之后(添加到元素外部)添加内容。
	* before() //在被选元素之前添加内容。


---

#### `jQuery HTML` 移除元素/内容

	* remove() //移除被选元素，包括所有的文本和子节点。
	* empty() //移除被选元素所有子节点和内容。不会移除元素本身，或它的属性。

---

#### `jQuery Get Set CSS`类

	* addClass() //向被选元素添加一个或多个类名。
		//添加多个类，用空格分隔。
	* removeClass() //从被选元素移除一个或多个类。
		//如果该参数为空，将移除所有类名称。
	* toggleClass() //检查每个元素中指定的类。如果不存在则添加类，如果已设置则删除之。

---

#### `jQuery css()` 方法

	* css() //为被选元素设置或返回一个或多个样式属性。
	
	<script>
		$("button").click(function(){
			$("p").css({
				"color":"white",
				"background-color":"#98bf21",
				"font-family":"Arial",
				"font-size":"20px",
				"padding":"5px"
			});
		});
	</script>

---

#### `jQuery` 尺寸 

	* width() //设置或返回被选元素的宽度。
	* height() //设置或返回被选元素的高度。
		//返回宽度时， 则返回第一个匹配元素的宽度。
		//设置宽度时，则设置所有匹配元素的宽度。

	* innerHeight(); innerWidth() //返回第一个匹配元素的内部高度/宽度。包含 padding，但不包含 border 和 margin。
	
	* outerHeight(includeMargin); outerWidth(includeMargin) //返回第一个匹配元素的外部高度/宽度。包含 padding 和 border。
		includeMargin //布尔值，规定是否包含 margin。默认 false。
	
---

#### `jQuery` 遍历 

祖先
	
	* closest(filter,context) //返回被选元素的第一个祖先元素。直到找到与所提供的选择器匹配的为止。
	* parent(filter) //返回被选元素的直接父元素。该方法只沿着 DOM 树向上遍历单一层级。
	* parents(filter) //返回被选元素的所有祖先元素。
	* parentsUntil(stop,filter) //返回介于 selector 与 stop 之间的所有祖先元素。
	
	//举例
	<script>
		$(document).ready(function(){
			$("span").parentsUntil("body","p,li,div")
				.css({"color":"red","border":"2px solid red"});
		});
	</script>
	//缩小范围在 span 和 body 之间寻找祖先 p,li 和 div。

后代

	* children(filter) //返回被选元素的所有直接子元素。
	* find(filter) //返回被选元素的后代元素。	
	//举例
	<ul class="level-1">
	  <li class="item-i">II
	        <ul class="level-3">
	          <li class="item-1">1</li>
	          <li class="item-2">2</li>
	          <li class="item-3">3</li>
	        </ul>
	  </li>
	</ul>
	<script>
		$('li.item-i').find('li').css('background-color', 'red');
	</script>
	//匹配的 li.item-i 的后代中的 1，2，3，将背景变为红色。

同胞 `siblings`

	* siblings(filter) //返回被选元素的所有同级元素。
	* next(filter) //返回被选元素的后一个同级元素。
	* nextAll(filter) //返回被选元素之后的所有同级元素。
	* nextUntil(stop,filter) //返回 selector 与 stop 之间的每个元素之后的所有同级元素。

---

#### `jQuery AJAX load()` 方法

	* load() //从服务器加载数据，并把返回的数据放置到指定的元素中。

---

#### `jQuery AJAX get() post()` 方法

	* get() //使用 AJAX 的 HTTP GET 请求从服务器加载数据。	* post() //使用 AJAX 的 HTTP POST 请求从服务器加载数据。

---
	
	