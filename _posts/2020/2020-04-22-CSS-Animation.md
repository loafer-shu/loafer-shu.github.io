---
layout: post
title: CSS Animation
category: CSS
tags: [css]
---

关于CSS动画的快速说明。

## CSS Animation

CSS3动画使元素逐渐从一种样式变为另一种样式。

两步：

1. 使用 `@keyframes` 定义动画.
2. 在具有动画属性的元素上设置此动画

我们可以单独地设置属性，或者用下面的速记法:

{% highlight css %}
animation: [animation-name] [animation-duration] [animation-timing-function] [animation-delay] [animation-iteration-count] [animation-direction] [animation-fill-mode] [animation-play-state];
{% endhighlight %}

## @keyframes

它定义了动画时间轴每个阶段的动画外观。它由以下组成：

* 动画名称。例如，changeColor。 
* 阶段：从0％到100％代表动画的整个过程
* CSS属性：为动画时间轴的每个阶段定义的CSS属性。

下面的示例创建一个名为`changeColor`的动画并将其分配给`div:hover`：
{% highlight css %}
@keyframes changeColor {
  0% {
    background: red;
  }
  60% {
    background: blue;
  }
  100%{
    background: green;
  }
}

div:hover{
  animation: changeColor 5s ease .1s;
}
{% endhighlight %}

> 在上面的示例中, 我们还可以使用 `from` 表示 `0%` ， `to` 表示 `100%`

## Animation 属性

它具有以下属性：

1. animation-name
2. animation-duration
3. animation-timing-function
4. animation-delay
5. animation-iteration-count
6. animation-direction
7. animation-fill-mode
8. animation-play-state

### animation-name

动画的名称，在@keyframes中定义。

### animation-duration

动画的持续时间，以秒（例如5s）或毫秒（例如200ms）为单位.

### animation-timing-function

动画的速度曲线或速度:

| Timing Function | 说明 |
|---|---|
| linear | 从头到尾，动画的速度相同d |
| ease | **默认值**. 动画在开始缓慢结束之前先缓慢后快速。 |
| ease-in | 慢慢开始，快速结束.  |
| ease-out | 比线性的开始更快，而缓慢的结束。缓解的反面. |
| ease-in-out | 缓慢的开始和缓慢的结束 |
| initial | 将此属性设置为其默认值。所以 `ease`. |
| inherit | 从其父元素继承此属性. |


### animation-delay 

它指定动画何时开始。该值以秒（s）或毫秒（mil）为单位定义。

### animation-iteration-count

它指定动画将播放的次数。可能的值为：

* 特定的迭代次数（默认为1）
* `infinite` - 永远重复
* `initial`
* `inherit`

### animation-direction

它指定动画是应前进，后退还是交替播放。 
* `normal`-默认。在每个循环中，动画将重置为开始状态（0％），然后再次播放（至100％）。 
* `reverse`-在每个循环中，动画重置为结束状态（100％），然后向后播放（为0％）。 
* `alternate`-在每个奇数周期，动画会向前播放（0％至100％）。在每个偶数周期，动画将向后播放（100％至0％）。 
* `alternate-reverse`-在每个奇数周期，动画以相反的顺序播放（100％到0％）。在每个偶数周期中，动画都会向前播放（0％或100％）。
### animation-fill-mode

它指定动画样式在动画播放之前或之后是否可见。
* `normal` - 默认。在动画之前或之后，动画不会对元素应用任何样式。
* `forwards` - 动画结束后，元素将保留最终关键帧（100％）中定义的样式。
* `backwards` - 在动画之前（动画延迟期间），会将初始关键帧的样式（0％）应用于元素。
* `both` - `forwards` 与 `backwards`.

### animation-play-state

Two values: `running` and `paused`.

它指定动画是“正在播放”还是“已暂停”。 **恢复暂停的动画会在不播放动画的地方开始播放。但是，如果暂停动画，则元素样式将返回其原点。**

举个🌰:

{% highlight css %}
div:hover {
  animation-play-state: paused;
}
{% endhighlight %}

## 多种动画

用逗号将多个动画添加到选择器：

{% highlight css %}
div {
  animation: animationA 2s, animationB 2s;
}
{% endhighlight %}

## Refs

* [Imooc 十天精通CSS3](http://www.imooc.com/learn/33)
* [CSS Animation for Beginners](https://robots.thoughtbot.com/css-animation-for-beginners#animation-iteration-count)
* [CSS3 animation-timing-function Property](http://www.w3schools.com/cssref/css3_pr_animation-timing-function.asp)
