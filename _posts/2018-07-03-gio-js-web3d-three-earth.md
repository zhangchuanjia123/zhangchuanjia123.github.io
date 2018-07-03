---
layout: post
title: 开源Gio.js：一个基于 Three.js 的 Web3D 地球数据可视化库
date: 2018-07-03 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: diqiu.gif # Add image post (optional)
tags: [Gio.js/Three.js] # add tag
---

晚上浏览掘金社区的时候偶然发现一个web3D可视化库，炫酷的动态数据让我眼前一亮，所以在这里给大家分享一下：Gio.js 是一个基于 Three.js 的 web 3D 地球数据可视化的开源组件库。使用 Gio.js 的网页应用开发者，可以快速地以申明的方式创建自定义的 Web3D 数据可视化模型，添加数据，并且将其作为一个组件整合到自己的应用中。

Github 地址： [https://github.com/syt123450/giojs](https://github.com/syt123450/giojs)

中文官网: [http://giojs.org/index_zh.html](http://giojs.org/index_zh.html)

Codepen 在线例子: [https://codepen.io/collection/DkBobG/](https://codepen.io/collection/DkBobG/)

![](http://giojs.org/assets/images/Gio.png)    

## 为什么要开发、使用 Gio.js?
这个库的开发是受到 Google 2012 Info 大会上的项目[世界武器贩卖](https://github.com/dataarts/armsglobe)可视化的启发，该项目开发者是 Google 员工 Michael Chang。使用 Gio.js 就可以快速构建这种炫酷的 3D 模型，并以此为基础进行深入地开发。Gio.js 具有以下的特点：
##### 1、易用性 -- 仅使用 4 行 Javascript 即可创建 3D 地球数据可视化模型；
##### 2、定制化 -- 使用 Gio.js 提供的丰富的 API 来创建自定义样式的 3D 地球；
##### 3、现代化 -- 基于 Gio.js 构建高交互、跨平台、自适应的现代化 3D 前端应用；

## 基本使用的了解：

通过 NPM 或者 YARN 安装 giojs
---
    npm install giojs --save
---

``
---
    yarn add giojs
---

在 HTML 页面中添加了 Threejs 和 Giojs 依赖之后，您就可以基于 Giojs 开发您的应用了。我们将展示如何创建一个具有基础样式的 Gio 地球。

---
{% highlight ruby %}
<!DOCTYPE HTML>
<html>
<head>

  <!-- 引入 three.js -->
  <script src="three.min.js"></script>

  <!-- 引入 Gio.js -->
  <script src="gio.min.js"></script>

</head>
<body>

  <!-- 创建一个 div 作为 Gio 的绘制容器 -->
  <div id="globalArea"></div>

</body>
</html>
{% endhighlight %}
---

在页面中添加以下 Javascript 代码来初始化 Gio 地球：

---
{% highlight ruby %}
<script>

    // 获得用来承载 Gio 地球的容器
    var container = document.getElementById( "globalArea" );

    // 创建 Gio 控制器
    var controller = new GIO.Controller( container );

    // 添加数据
    controller.addData( data );

    // 初始化并渲染地球
    controller.init();

</script>
{% endhighlight %}
---

## 文档
中文 [README](https://github.com/syt123450/giojs/blob/master/README_zh.md)

快速了解如何使用 Giojs [开始使用文档](https://github.com/syt123450/giojs/blob/master/docs/zh/Getting_Started_zh.md)

有关 Gio.js 的 [3D基础组件介绍文档](https://github.com/syt123450/giojs/blob/master/docs/zh/Basic_Elements_zh.md)

详细介绍 [API 文档](https://github.com/syt123450/giojs/blob/master/docs/zh/APIs_zh.md)

参与 Gio.js 项目开发的 [开发者文档](https://github.com/syt123450/giojs/blob/master/docs/zh/Developer_Guide_zh.md)


