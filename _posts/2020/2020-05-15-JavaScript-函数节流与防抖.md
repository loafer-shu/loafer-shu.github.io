---
layout: post
title:  "节流与防抖"
date:   2020-05-15 11:04:35 +0800
categories: JavaScript
---

## 函数节流与防抖

- 函数节流: 指定时间间隔内只会执行一次任务；
- 函数防抖: 任务频繁触发的情况下，只有任务触发的间隔超过指定间隔的时候，任务才会执行。

### 函数节流(throttle)

```javascript
//实现节流
function throttle(fn, interval = 300) {
    let canRun = true;
    return function () {
        if (!canRun) return;
        canRun = false;
        setTimeout(() => {
            fn.apply(this, arguments);
            canRun = true;
        }, interval);
    };
}

function onScroll() {
    // 判断是否滚动到底部的逻辑
    const pageHeight = $('body').height();
    const scrollTop = $(window).scrollTop();
    const winHeight = $(window).height();
    const thresold = pageHeight - scrollTop - winHeight;

    if (thresold > -100 && thresold <= 20) {
        console.log('end');
    }
}
//使用
$(window).on('scroll', throttle(onScroll));
```

### 函数防抖(debounce)

```javascript
//防抖实现
function debounce(fn, interval = 300) {
    let timeout = null;
    return function () {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
            fn.apply(this, arguments);
        }, interval);
    };
}
//使用
$('input.user-name').on('input', debounce(function () {
    $.ajax({
        url: `https://just.com/check`,
        method: 'post',
        data: {
            username: $(this).val(),
        },
        success(data) {
            if (data.isRegistered) {
                $('.tips').text('该用户名已被注册！');
            } else {
                $('.tips').text('恭喜！该用户名还未被注册！');
            }
        },
        error(error) {
            console.log(error);
        },
    });
}));
```

