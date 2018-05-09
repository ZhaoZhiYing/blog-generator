---
title: HTML 标签(二)
date: 2018-04-01 21:00:06
categories: HTML
tags:
---

#### `HTML` 表单标签

	* <form> //定义供用户输入的表单
	
	//<form> 元素包含一个或多个如下的表单元素
	* <input> //定义输入域
	* <textarea> //定义文本域 (一个多行的输入控件)
	* <label> //定义了 <input> 元素的标签，一般为输入标题
	* <fieldset> //定义了一组相关的表单元素，并使用外框包含起来
	* <legend> //定义了 <fieldset> 元素的标题
	* <select> //定义了下拉选项列表
	* <optgroup> //定义选项组
	* <option>v定义下拉列表中的选项
	* <button> //定义一个点击按钮
	
	//HTML5 新标签
	* <datalist> //指定一个预先定义的输入控件选项列表
	* <keygen> //定义了表单的密钥对生成器字段
	* <output> //定义一个计算结果

##### `<form>`

一个简单的 `HTML` 表单，包含两个文本输入框和一个提交按钮。

举例 

	<form action="demo_form.asp">
	  First name: <input type="text" name="fname"><br>
	  Last name: <input type="text" name="lname"><br>
	  <input type="submit" value="提交">
	</form>
	

注意事项：

	1.target 属性基本同 a 标签
	2.如果 form 表单里没有提交按钮，就无法提交
	3.form 标签主要用来发起 post 请求
	4.name 属性值显示在 HTTP 请求 第四部分
	 	//主要使用 POST 请求，参数放到第四部分 from datas 。
	 	//使用 GET 请求时，参数默认放到查询参数。
	
	// a 标签和 form 标签都是用来发请求，a 标签使用 get，form 标签主要使用 post。

#### `<input>`

`input` 没有子元素，`button` 有子元素

属性

	* accept //规定通过文件上传来提交的文件的类型。 (只针对type="file")
		audio/* //声音文件。
		video/* //视频文件。
		image/* //图像文件。
		MIME_type //一个有效的 MIME 类型
	* checked //规定在页面加载时应该被预先选定的 <input> 元素。 (只针对 type="checkbox" 和 type="radio")
		//checked 属性也可以在页面加载后，通过 JavaScript 代码进行设置。
	* disabled //规定禁用的 <input> 元素。
	* name //规定 <input> 元素的名称。
		//name 属性用于在 JavaScript 中引用元素，或者在表单提交后引用表单数据。
	* maxlength //规定 <input> 元素中允许的最大字符数。
	* size //规定以字符数计的 <input> 元素的可见宽度。
	* readonly //规定输入字段是只读的。
	* alt //定义图像输入的替代文本。 (只针对type="image")
	* src //规定显示为提交按钮的图像的 URL。 (只针对 type="image")
	* value //指定 <input> 元素初始（默认）值。
		//value 属性对于 <input type="checkbox"> 和 <input type="radio"> 是必需的。
		//value 属性不适用于 <input type="file">
		

	// HTML5 中的新属性
	* autocomplete //规定 <input> 元素输入字段是否应该启用自动完成功能。
	* autofocus //属性规定当页面加载时 <input> 元素应该自动获得焦点。
	* form //规定 <input> 元素所属的一个或多个表单。
	* required //规定必需在提交表单之前填写输入字段。
	* placeholder //规定可描述输入 <input> 字段预期值的简短的提示信息 。
	* multiple //规定允许用户输入到 <input> 元素的多个值。
	* min //规定 <input> 元素的最小值。
	* max //规定 <input> 元素的最大值。
	* width //width 属性规定 <input> 元素的宽度。 (只针对type="image")
	* height //规定 <input>元素的高度(只针对type="image")。
	* step //规定 <input> 元素的合法数字间隔。
	...

`type`属性值

	* button //定义可点击的按钮。
	* checkbox //定义复选框。
	* file //定义文件选择字段和 "浏览..." 按钮，供文件上传。 
	* hidden //定义隐藏输入字段。 
	* image //定义图像作为提交按钮。 
	* password //定义密码字段（字段中的字符会被遮蔽）。 
	* radio //定义单选按钮。 
	* reset //定义重置按钮（重置所有的表单值为默认值）。 
	* submit //定义提交按钮。 
	* text //默认。定义一个单行的文本字段（默认宽度为 20 个字符）。 
	
	// HTML5 中的新属性值
	* color //定义拾色器。 
	* date //定义 date 控件（包括年、月、日，不包括时间）。 
	* datetime //定义 date 和 time 控件（包括年、月、日、时、分、秒、几分之一秒，基于 UTC 时区）。 
	* datetime-local //定义 date 和 time 控件（包括年、月、日、时、分、秒、几分之一秒，不带时区）。 
	* email //定义用于 e-mail 地址的字段。
	* month //定义 month 和 year 控件（不带时区）。 
	* number //定义用于输入数字的字段。  
	* range //定义用于精确值不重要的输入数字的控件（比如 slider 控件）。 
	* search //定义用于输入搜索字符串的文本字段。
	* tel //定义用于输入电话号码的字段。 
	* time //定义用于输入时间的控件（不带时区）。
	* url //定义用于输入 URL 的字段。 
	* week //定义 week 和 year 控件（不带时区）。
	
	//如果一个 form 只有一个按钮 button，没写 type，自动升级为 submit。submit 是唯一能确定 type 能不能提交的按钮，button 只是一个普通按钮。

#### `<label>`

`<label>` 标签为 `input` 元素定义标注（标记）。

属性

	* for //规定 label 与哪个表单元素绑定。值为元素的 id。
	
	// HTML5 新属性
	* form //规定 label 字段所属的一个或多个表单。值为 form 的 id。

举例`for`

	<form action="demo_form.html">
	  <label for="male">Male</label>
	  <input type="radio" name="sex" id="male">
	  <label for="female">Female</label>
	  <input type="radio" name="sex" id="female">
	  <input type="submit" value="提交">
	</form>

举例`form` 

	<form action="demo_form.php" id="form1">
	  <input type="radio" name="sex" id="male">
	  <label for="female">Female</label>
	  <input type="radio" name="sex" id="female">
	  <input type="submit" value="提交">
	</form>
	
	<label for="male" form="form1">Male</label>		
更聪明的写法：用`<label>` 标签包裹`<input>`标签，不需要`for`和`name`。 

	<form action="demo_form.html">
	  	<label>Male
		  <input type="radio" name="sex">
    	</label>
	    <label>Female
	  	  <input type="radio" name="sex">
	    </label>
	    <input type="submit" value="提交">
	</form>

#### `<select>` `<option>` `<optgroup> `

属性

	*disabled //规定禁用该选项组。
	*label //为选项组规定描述。

举例：实现两个带有 `label` 的选项组。 

	<select>
	  <optgroup label="Swedish Cars">
	    <option value="volvo">Volvo</option>
	    <option value="saab">Saab</option>
	  </optgroup>
	  <optgroup label="German Cars">
	    <option value="mercedes">Mercedes</option>
	    <option value="audi">Audi</option>
	  </optgroup>
	</select>

#### `<textarea>`标签

输入多行文本.通过 `cols` 和 `rows` 属性来规定 `textarea` 的尺寸，更好的办法是使用 `CSS` 的 `height` 和 `width` 属性。

	<textarea rows="10" cols="30">
	我是一个文本框。 
	</textarea>

---

### `HTML` 表格标签

#### `<table>`

一个简单的 HTML 表格，包含两列两行：

	tr(table row)元素定义表格行
	th(table head)元素定义表头
	td(table data)元素定义表格单元(数据)

属性

	在 HTML5 中，仅支持 "border" 属性，并且只允许使用值 "1" 或 ""。


举例

	<table border="1">
		<tr>
			<th>Month</th>
			<th>Savings</th>
		</tr>
		<tr>
			<td>January</td>
			<td>$100</td>
		</tr>
	</table>


#### `<caption> `

`<caption> `标签定义表格的标题。必须直接放置到 `<table>` 标签之后。


#### `<colgroup>` `<col>` 

	* 只能在 <table> 元素之内，在任何一个 <caption> 元素之后，在任何一个  <thead> <tbody> <tfoot> <tr> 元素之前使用 <colgroup> 标签。
	* <col> 标签规定了 <colgroup> 元素内部的每一列的列属性。

属性

	* span //在 <colgroup> 中，规定列组应该横跨的列数。
		//在 <col> 中，指规定 <col> 元素应该横跨的列数。
		
	//若在 <colgroup> 中嵌套了 <col> 元素则应该避免在 <colgroup> 中使用 <col> 标签属性。
	//这是因为属于嵌套的 <col> 元素的 span 标签属性将覆盖 <colgroup> 元素中的标签属性。	

举例

<img src="https://i.loli.net/2017/12/10/5a2d416f2959f.png">

---
