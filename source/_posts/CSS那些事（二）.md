---
title: CSS那些事（二）
date: 2022-09-30 18:28:51
categories: 知识梳理
---
# CSS
CSS在html的基础上为网页“增色”，有了CSS，我们才做出如今灵动多彩的网页。

本文为大家带来CSS的一些技巧，满足实际开发中的大部分场景。

## css实现动画
### 过渡动画
过渡：`transition:属性（all） 花费时间 运动曲线 何时开始。`搭配‘hover’使用。谁要发生动画效果就给谁加。

转换：`transform:`与过渡一起使用，达到动画效果。

- translate:移动效果
- rotate:旋转效果
- scale:缩放

### css 关键帧动画
animation:相比于过渡，动画可以实现更多的动态效果。
```
//定义动画
@keyframs 动画名{
    0%{//开始状态
        转换操作
    },
    ....//可以在中间添加任意多的关键帧没实现复杂的动画
    100%{//结束状态
        转换操作
    }
}
//使用动画
.类{
    animation:动画名 持续时间 运动曲线 何时开始 步长  播放次数 是否逆向。。。。
}
```

## 网页元素的显示与隐藏

通常有几种控制元素隐藏的方式
1. ` display:none;`：会使元素从渲染树上消失，元素不再占有原来的位置，更不能触发绑定的事件。
2. `visibility:hidden;`：这种方法与` display:none;` 不同的是，这种方式隐藏的元素不会空出原来位置，会继续占有位置。但不会触发绑定的事件。 
3. `opacity=0;`，该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如 click 事件，那么点击该区域，也能触发点击事件。 
4. `left:-1000px`哈哈1000px有点夸张，意思就是让元素离开页面的可视区域。这种方法不建议使用，笔者唯一一次使用是为了避开浏览器的表单自动填充功能，将一个输入框放到可视区域外。
5. `height:0`也可以使元素隐藏。

## 溢出文字省略号效果：
常见的手写题：
```
write-space:nowarp;
overflow:hidden;
text-overflow:ellipsis;
```

## css 三角
1. 当我们把 box 的宽高置为 0，再设置边框时就会形成四个三角形，为他们设置不同颜色可以看到四个三角形。

![css三角](https://qiaolj-tuchuang.oss-cn-beijing.aliyuncs.com/img/CSS三角.jpg)

设置其中一个有颜色，另外三个透明就可以得到 css 三角

代码如下：

```
   div {
            height: 0;
            width: 0;
            border: 100px solid transparent;
            border-left-color: blue;
            /* border-top: 10px solid black;
            border-bottom: 10px solid green;
            border-right: 10px solid red; */
        }
```
2. 在工作中，我又遇到了一种制作三角形的方法：利用线性渐变。

——方向左上角到右下角，颜色从透明到想要的颜色，位置在 50%就可以了。

利用这种方式，我们可以制作出颜色渐变的三角形。

## 响应式布局

### 1.媒体查询+rem

`rem`是基于根节点字体大小的单位，可以随根节点字体的大小而改变。

如 html 的 `font-size` 为 `100px`那么`1rem=100px`

那么，我们又是怎么获取所在屏幕的大小尺寸的呢？

我们用了一种媒体查询的方式，`media-query` 可以帮助我们获取到当前所在屏幕的大小。

```
@media screen and (max-width:800px){
    html{
        font-size:80px; !important
    }
}
```

这段代码的意思是，屏幕小于 800px 时，根节点字体大小为 80px。

利用媒体查询+rem 的方式的确可以实现响应式布局。

可与之相关的问题就是，响应式布局只能在一个区间段内定义根字体的大小，具有阶梯式的变化特点，并不是时时改变的。

## vw 和 vh 代替 rem

由于 rem 阶梯性的弊端，vw 和 vh 带来了解决方案
vh 是 window.innerHeight 视口高度的 1/100。
vw 是 window.innerWeight 视口高度的 1/100。