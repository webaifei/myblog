---
title: xml获取html, js ,css
date: 2017-11-09 19:28:24
tags: [异步, javascript]
---

问题源于一个面试题：
> 通过xhr获取一html片段，其中包含html，css，js ，请问三种是否都能正常的解析执行？

代码：
```
var xhr = new XMLHttpRequest();
  xhr.open('get', './hasjsHtml.html', true);
  xhr.onreadystatechange = function(){
    if(xhr.status == 200 && xhr.readyState ==4){
      console.log(xhr.responseText)
      document.getElementById('test').innerHTML = xhr.responseText;
    }
  }
  xhr.send(null)

//请求的html片段
<style>

#sdf{
  width: 100px;
  height: 100px;
  border: 1px solid #ccc;
}
</style>
<div id="sdf">
  nice
</div>
<script type="text/javascript">
  alert(1)
</script>
```

结论：
1. html，css样式都能够正常的解析和执行
2. js不能被执行



