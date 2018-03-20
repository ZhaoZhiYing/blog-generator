---
title: JS 常用条件判断语句
date: 2018-03-20 16:42:38
categories:
tags:
---

### `for` 

循环代码块一定的次数。

语法

	for ([initialization]; [condition]; [final-expression]){
	    被执行的代码块
	}
	
	initialization //开始前执行
	condition //定义运行循环的条件
	final-expression //在循环已被执行之后

举例

	for (var i=0; i<5; i++){ 
	    document.write(i);
	}
	
	//0 1 2 3 4
	
	
结合 `onclick`，下面例子中，点击不同的按钮，打印都是 5。

	<button>0</button>
	<button>1</button>
	<button>2</button>
	<button>3</button>
	<button>4</button>
	
```	
<script> 
	var btn = document.getElementsByTagName('button');
	for(var i=0; i<btn.length; i++){ 
	    btn[i].onclick=function(){ 
	        console.log(i);
	    }
	}
</script>
```	
	
现在换一种写法，下面例子中，依次点击按钮，会打印 0 1 2 3 4 。

    <script> 
        var btn=document.getElementsByTagName('button');
        for(var i=0; i<btn.length; i++){ 
            (function(j){ 
                btn[j].onclick=function(){ 
                    console.log(j);
                }
            }(i)) //循环中的 i，被作为参数传入。
        }
    </script>

---
   
### `for in`

用于遍历数组或者对象的属性（对数组或者对象的属性进行循环操作）。

语法

	for (value in object) {...}
	
举例	

	var obj = {a:1, b:2, c:3};
	    
	for (var j in obj) {
	  document.write("obj." + j + " = " + obj[j] + '<br>');
	}
	
	//obj.a = 1
	//obj.b = 2
	//obj.c = 3

---

### `if...else`

用于基于不同的条件来执行不同的动作。
	
语法

	if (condition1){
	    当条件 1 为 true 时执行的代码
	}
	else if (condition2){
	    当条件 2 为 true 时执行的代码
	}
	else{
	  当条件 1 和 条件 2 都不为 true 时执行的代码
	}	
	
举例：实现上面 `if...else` 的例子。

	var mydate = new Date();
	var mytime = mydate.getHours();
	
	if (mytime < 8 && mytime > 5){
	    console.log("早上好");
	}else{
		console.log("哈哈哈");
	}	
	
---

#### 三元运算符
	
语法

	condition ? expr1 : expr2 

```
* condition 计算结果为true或false的表达式。
* 如果条件值为真值（true），运算符就会返回 expr1 的值。
* 否则，就会返回 expr2 的值。	
* expr1, expr2 值可以是任何类型的表达式。
```	

举例

	var mydate = new Date();
	var mytime = mydate.getHours();
	
	mytime < 8 && mytime > 5 ? console.log("早上好") : console.log("哈哈哈")	    

---