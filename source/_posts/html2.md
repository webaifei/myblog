---
title: 居中布局
date: 2017-11-09 19:27:39
tags: [html, css]
---

## 居中布局

> 不论是面试还是工作中 我们经常遇到的问题就是居中（水平 垂直居中）

### 外部容器固定高度 需要居中的元素也固定高度
```
因为都是固定值 所以能够通过设置固定值来定位， 不论是通过margin还是position等
```
### 外部容器高度不固定 内部元素的高度固定

```
/*(无兼容问题)*/
.center{
  width: 200px;
  height: 220px;
  background: #acb;
  position: relative;
  top: 50%;//把元素的左上角放到中心点
  margin:0 auto;//水平居中
  margin-top: -110px;//向上移动容器自身的一半

}
```

### 外部容器高度固定 内部容器高度不固定

```
  /*(兼容问题) IE67不支持display:table-cell;*/
  .wraper{
    display:table;
    /*需要设置宽高*/
    width:xxx;
    height:xxx;
  }
  .cell{
    display: table-cell;
    vertical-align: middle;
    text-align: center;
  }
```

```
  /*使用css3 */
  .center4{
    width: 50%;
    position: relative;
    /*拉倒中心*/
    left: 50%;
    top: 50%;
    /*移动本身宽高的负1/2*/
    transform: translate3d(-50%, -50%, 0)
  }
```

### 使用vertical-align middle来实现图文垂直居中（类似flex的效果）

```
  .list-item{
    padding: 10px;
    /*如果设置了固定的高度  需要设置line-height来让vertical-align起作用 相应的内部元素都需要重新设置line-height*/
  }
  .img{
    vertical-align:middle;
  }
  .desc{
    display:inline-block;
    vertical-align: middle;
  }
```

### 强大的flex布局
```
.flex{
  display: flex;
  display: -webkit-flex;
  display: flex-box;

  justify-content: center;//水平居中
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
}
.flex-item{
  flex: 1;
  -webkit-box-flex: 1;
  display: block;//兼容uc的bug
}
```

