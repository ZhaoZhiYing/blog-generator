---
title: target 与 currentTarget
date: 2018-02-03 18:56:13
categories: JavaScript
tags:
---

* `currentTarget`：指绑定事件的对象。恒等于`this`。
* `targt`：指触发事件的某个具体对象。

举例1

```
 <div id="grand">
    爷爷
     <div id="parent">
      爸爸
       <div id="child">
        儿子
       </div>
     </div>
  </div>

grand.addEventListener('click',function(e){
    console.log(e.target)
    console.log(e.currentTarget)
},false)
//当点击 child 是，打印结果是：child  grand 
//这时的 this 指向 grand
```
举例2

```
 <div id="grand">
    爷爷
     <div id="parent">
      爸爸
       <div id="child">
        儿子
       </div>
     </div>
  </div>

child.addEventListener('click',function(e){
    console.log(e.target)
    console.log(e.currentTarget)
},false)
//当点击 child 是，打印结果是：child  child
//这时的 this 指向 child
```

---