---
title: 格式化银行号码
date: 2017-11-09 19:42:42
tags: [javascript]
---

需求：
> 用户输入银行卡号的时候 将银行卡号每四个数字之间加上一个空格 ， 并且保证光标位置正确（比如用户可能从中间位置插件数字）

功能点：
1. 格式化
2. 中间位置输入 光标位置定位问题



### 格式化

```
    //正则：
    var formatReg = /(\d{4})(?=\d)/g;

    var val = this.value;

    var newVal = val.replace(/\s/g, '').replace(formatReg, ' ');


```

### 光标位置定位问题

```
    如果我们直接给input赋值的话 ， 它的光标默认会调到最后，这样，当我们想在之间位置插入数字的时候，光标总会跑到最后，需要我们重新定位光标


    w3c =>this.selectionStart = selectionEnd = pos;

    //如何计算pos呢？
    我们的输入值长度变换主要是因为空格引起的， 只需要计算出我们光标之前空格的变化+原来的光标位置就行了

    var startPos = this.selectionStart;
    //原始值得空格数量
    var originalSp = (this.value.slice(0, startPos).match(/\s/)||[]).length;
    //格式化
    var newVal = this.value.replace(/\s/g, '').replace(formatReg, ' ');
    //格式化后的空格
    var curSp = (newVal.slice(0, startPos).match(/\s/)||[]).length;

    //新的位置
    var pos = startPos + curSp - originalSp;
    this.selectionStart = selectionEnd = pos;
```

## 完整的示例

```
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width">
        <title>使用正则格式化</title>
    </head>
    <body>
        <p>银行卡号</p>
        <input type="tel" name="" style="width: 400px;">
    </body>
    <script type="text/javascript">
        var input = document.querySelector('input');
        //输入的时候 获取当前的值 怎么回填
        var length = 0;
        var lastAdd = false;
        input.oninput = function(e){
            var val = e.target.value;
            var posStart = this.selectionStart;
            //原始值的光标之前的空格数
            var originalSp = (val.slice(0, posStart).match(/\s/g)||[]).length;

            var newVal = val.replace(/(\d{4})(?=\d)/g, '$1 ');
            //替换完成之后的空格
            var curSp = (newVal.slice(0,posStart).match(/\s/g)||[]).length;

            e.target.value = newVal;
            //this.setSelectionRange(posStart, res.length)
            this.selectionStart = this.selectionEnd = posStart +curSp -originalSp;
            //console.log(res)
        }
    </script>
    </html>
```

