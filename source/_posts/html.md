---
title: 一些知识点
date: 2017-11-09 19:26:55
tags: [html, css]
---


## 写在前面

总结了一些有用的面试知识点，没有什么规律

1. 解决chrome不允许设置<12px的字体问题

  ```
  //网上有好多这样的说法 然后我傻傻的去试了下 ： 我擦 骗我！
  // 继续百度 发现这个是在低版本的chrome（27）中可以使用 高版本已经禁用了
  html{
    -webkit-text-size-ajust:none;
  }
  // css3 使用transform:scale()来实现

  .f10{
    font-size: 12px;
    transform:scale(0.875);
    transform-origin: left bottom;
  }
  ```


2. 网页布局之圣杯布局和双飞翼布局
  > 首先明白一点，这两种布局概念的提出都是为了解决网页左中右三栏布局的问题
  1. 要求左右两栏固定宽度， 中间的内容宽度自适应
  2. 一般中间的内容很重要，需要优先解析展示

  正常情况下，我们直接使用浮动就能够解决问题1
  ```
  /*css*/
  .container{

  }
  .left{
    float:left;
    width: 200px;
    background:#f00;
  }
  .right{
    float: right;
    width: 150px;
    background:#ff0;
  }
  .center{
    padding: 0 150px 0 200px;
    background: blue;
  }

  /*html 结构*/
  .container>.left+.right+.center
  ```

  ### 上面的布局结构 能够解决问题1， 但是问题2却无法解决，改进方案(圣杯布局)：
  ```
  /*html structure*/
  <div class="container">
    <div class="center">中间内容</div>
    <div class="left">导航</div>
    <div class="right">右侧内容</div>
  </div>

  /*css*/
  div{
    min-height: 100px;
  }
  .container{
    padding: 0 150px 0 200px;
  }
  .left{
    float:left;
    width: 200px;
    background:#f00;
    margin-left: -100%;
    z-index: 10;
    position: relative;
    left: -200px;
  }
  .right{
    float: left;
    width: 150px;
    background:#ff0;
    margin-left: -150px;
    position: relative;
    right: -150px;
  }
  .center{
    width: 100%;
    float: left;

    background: blue;
  }
  ```
  实现的主要原理：
  1. 通过margin-left 负值把left 和 right 部分拉到和center同列中 给外层的container设置padding 通过定位把left 和 right 定位到正确的位置上。

  ps： 太诡异了

  ### 国内淘宝ued团队的双飞翼布局
  ```
    /*html structure*/

    <div class="container">
      <div class="center">
        <div class="inner">我是中间</div>
      </div>
      <div class="left"></div>
      <div class="right"></div>

    </div>

    /*css*/
    div{
      min-height: 100px;
    }
    .container{

    }
    .left{
      float:left;
      width: 200px;
      background:#f00;
      margin-left: -100%;
    }
    .right{
      float: left;
      width: 150px;
      background:#ff0;
      margin-left: -150px;
    }
    .center{
      width: 100%;
      float: left;
      background: blue;

    }
    .inner{
        padding: 0 150px 0 200px;
    }

  ```
  > 主要解决思路 把中间的部分放到一个单独的div中 通过这个容器来设置padding
  1. 免去了设置定位
  2. 结构样式控制更加合理
