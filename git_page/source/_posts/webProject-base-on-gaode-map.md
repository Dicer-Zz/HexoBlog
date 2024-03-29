---
title: 基于高德地图 API 的 Web 课程设计
cover: /gallery/thumbnails/gate-wall.jpg
date: 2019-12-28 13:34:14
tags: 
    - Web
categories: 
---

## Web课程设计

说好的考试突然就变成了课程设计，竟然还要写一个多达20页的论文，实在是不知如何是好。

Web 考试本来应该是最简单的了，想着随便看看就过了，现在可倒好，就算是把我肚子里的东西都倒出来也凑不够20页的论文。

话虽然这样说，不过还是认真的做了一个网页的。主要基于高德地图的开放API，此处给阿里点个赞，高德地图应该是有口皆碑，用过的都知道很好。

页面随便搞了搞，做了一个大色块撞色的设计，感觉还挺好看的。排版就是简单的几个 div 布局。

然后提供了三个小功能，包括经纬度查询，地点联想查询和点击获得经纬度。都是通过 js 和提供的 API 实现的。

[项目演示](http://47.101.66.37:8888/map)

<!--more-->

## HTML 部分

在 head 标签里面引入高德地图的 API 和自己写好的 js 以及 css 文件。

body 里面有一个项目的名称和简介，然后就是三个显眼的功能方块，对应着三个小功能。下面就是地图本身了，直接调用 API 给出一个默认地址就可以加载了。

第一个功能方块提供了经纬度地图查询，默认为我校的地址。通过输入经纬度，然后点击确认按钮，通过按钮的 onclick 事件连接到一个 js 函数，实现地图查询。

第二个功能方块是最复杂的一个，使用了关键字补全 API，通过检测选择事件来实现地图的重新加载。

第三个功能方块分为两个部分，一个是通过监听 click 事件来实现获取点击处的经纬度，并将其填入 input 标签的内容中。然后复制按钮使用了 DOM 的 execCommand 函数进行复制。

## CSS 部分

地图主题用 container id 标记，通过百分比布局实现多设备自适应。

三个功能方块通过简单的媒体查询实现移动端，PC端的适应布局，个人感觉效果还是挺好的，就是在 iPad 上看有点歪，没有居中，实在是不知道是什么原因。

颜色是在网上找的一套颜色，看着也还行，也可能还有更好看的配色，不过实在是懒得调了，没有太大的意义。

## JAVASCRIPT 部分

三个功能方块都是 js 实现的，效果还是挺好的。工作的挺正常，有一个小 bug 是第二个功能方块在你操作过地图之后可能会失灵，我也不清楚是什么原因。

还有可以提升用户体验的方法，页面刷新前应该保存地图当前的位置，防止刷新之后地图更改，可能会造成用户不必要的麻烦。

## 总结

最后说一说总结吧。整个东西做下来还是挺有意思的，好多功能不知道怎么实现就一直在 google ，看 API 的文档和样例。基本功能实现了之后就是不断的调样式，怎么才能更好看一点。虽然是一个很简单的项目，自己一个人做下来感觉还是很有成就感的。