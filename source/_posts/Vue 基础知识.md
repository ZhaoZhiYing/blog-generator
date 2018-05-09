---
title: Vue 基础知识
date: 2018-03-13 14:10:31
categories:
tags:
---

#### `Vue` 实例

每个 `Vue` 应用都是通过用 `Vue` 函数创建一个新的 `Vue` 实例开始的。

	var vm = new Vue({...})

##### 数据与方法

当一个 `Vue` 实例被创建时，它向 `Vue` 的响应式系统中加入了其 `data` 对象中能找到的所有的属性。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

	var vm = new Vue({
	  data: data
	})

如果晚些时候需要一个属性，但是一开始它为空或不存在，那么需要设置一些初始值。

	data: {
	  newTodoText: '',
	  visitCount: 0,
	  hideCompletedTodos: false,
	  todos: [],
	  error: null
	}

##### 实例生命周期钩子

每个 `Vue` 实例在被创建时都要经过一系列的初始化过程。在这个过程中也会运行一些叫做生命周期钩子的函数。

**作用：**给用户在不同阶段添加自己的代码的机会。

比如 `created` 钩子可以用来在一个实例被创建之后执行代码：

```
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` 指向 vm 实例
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1"
```

---

#### 模板语法

##### 插值

数据绑定最常见的形式就是使用插值语法 (双大括号) 的文本插值。

	<span>Message: {{ msg }}</span>

插值语法同时支持 `JavaScript` 表达式。每个绑定都只能包含单个表达式。

	{{number + 1}}
	{{ ok ? 'YES' : 'NO' }}

插值语法不能作用在 `HTML` 特性上，遇到这种情况应该使用 `v-bind` 指令。

	<div v-bind:id="dynamicId"></div>

##### 指令

指令带有前缀 `v-`，以表示它们是 `Vue` 提供的特殊特性。

```
<a v-on:click="doSomething">...</a>
<div v-bind:class="{ active: isActive }"></div>
```

##### 修饰符

修饰符是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。

	<form v-on:submit.prevent="onSubmit">...</form>		
---

#### 计算属性

##### 模板内表达式

	<div id="example">
	  {{ message.split('').reverse().join('') }}
	</div>
	
##### 计算属性

模板内的表达式非常便利，但是在模板中放入太多的逻辑会让模板过重且难以维护。对于任何复杂逻辑，应当使用计算属性。

	<div id="example">
	  <p>{{ message }}</p>
	  <p>{{ reversedMessage }}</p>
	</div>
	
	<script>
		var vm = new Vue({
		  el: '#example',
		  data: {
		    message: 'Hello'
		  },
		  computed: {
		    // 计算属性的 getter
		    reversedMessage: function () {
		      // this 指向 vm 实例
		      return this.message.split('').reverse().join('')
		    }
		  }
		})
	</script>

##### 方法

计算属性是基于它们的依赖进行缓存的。如果不希望有缓存，可以用方法来替代。

	<p>Reversed message: "{{ reversedMessage() }}"</p>
	
	<script>
		methods: {
		  reversedMessage: function () {
		    return this.message.split('').reverse().join('')
		  }
		}
	</script>	

##### 侦听属性

`Vue` 提供了一种更通用的方式来观察和响应 `Vue` 实例上的数据变动：侦听属性。

	<div id="demo">{{ fullName }}</div>
	
	<script>
		var vm = new Vue({
		  el: '#demo',
		  data: {
		    firstName: 'Foo',
		    lastName: 'Bar',
		    fullName: 'Foo Bar'
		  },
		  watch: {
		    firstName: function (val) {
		      this.fullName = val + ' ' + this.lastName
		    },
		    lastName: function (val) {
		      this.fullName = this.firstName + ' ' + val
		    }
		  }
		})
	</script>
	
---	