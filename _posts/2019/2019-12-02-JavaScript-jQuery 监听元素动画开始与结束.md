---
layout: post
title: jQuery 监听元素动画开始与结束
date: 2019-12-02 16:07:35 +0800
categories: [JavaScript]
---

## jQuery 监听元素动画开始与结束

```javascript
// 监听动画执行开始事件
$('#OBJ').bind('animationstart webkitAnimationStart mozAnimationStart MSAnimationStart oanimationstart', function(){
   // ...
});

// 监听动画执行结束事件
$('#OBJ').bind('animationend webkitAnimationEnd mozAnimationEnd MSAnimationEnd oanimationend', function(){
	// ...
});
```

