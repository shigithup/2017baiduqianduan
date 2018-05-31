

## 由js tastkfour 引起的

## 1.[未输入时属性value的默认值](https://www.cnblogs.com/mingjiezhang/p/5371224.html)

在`<input type="text"/>`中未规定value的初始值同时用户未输入时，value的默认值是什么？

是个空字串：`""`||`''`。 

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>example</title>
  </head>
<body>
  <label for="weather_input">请输入北京今天空气质量：<input id="weather_input" type="text"/></label>
  <button id="confirm_button">确认</button>
  <p>你输入的值是：<span id="value_show">尚未输入</span></p>
<script type="text/javascript">
window.onload=function(){
  var button=document.getElementById("confirm_button");
  var span=document.getElementById("value_show");
  var input=document.getElementById("weather_input").value;
  button.onclick=function(){
  span.innerHTML=input;
}
}
</script>
</body>
</html>
```

这段代码语法上是正确的，不过逻辑上是有问题的：`var input=document.getElementById("weather_input").value`；该语句中input获取了input输入框的默认值，之后再触发button.onclick时，input的值无法即时更新，也就无法达到程序即时显示效果。 

## 2.规定输入内容仅为数字

把上面js部分的代码修改为，即触发事件后再获取`input`，并规定输入内容仅为数字。

**用`isNaN(input)`或者`/^[0-9]*$/.test(input)`**

```js
var button=document.getElementById("confirm_button");
  button.onclick=function(){
  var span=document.getElementById("value_show");
  var input=document.getElementById("weather_input").value;
  if (input==""||isNaN(input)) {
    alert("请输入一个有效值");
  } else {
    span.innerHTML=input;
  }
```



## 3.用原生实现点击删除点击的li

如何获得动态的`li`,事件代理或闭包。

原`taskfour.html`中用的是事件代理。

闭包如下：

```js
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>ife-js基础-4</title>
    <style>
      #left-out{margin-left: 20px;}
      .number{
        float: left;
        background: red;
        color: #fff;
        margin-right: 5px;
        font-size: 30px;
        padding: 0 10px;
        cursor: pointer;
      }
    </style>
  </head>
  <body>
    <div id="div-input">
      <input type="text" id="input" value="" />
      <input type="button" id="left-in" value="左侧入" />
      <input type="button" id="right-in" value="右侧入" />
      <input type="button" id="left-out" value="左侧出" />
      <input type="button" id="right-out" value="右侧出" />
    </div>
    <!--<div class="number">4</div><div class="number">5</div>
    -->
    <script type="text/javascript">
      (function(){
        var val = document.getElementById('input');
        //getElementsByClassName 返回一个数组
        //左侧入
        document.getElementById('left-in').onclick = function(){
          if(/^[0-9]*$/.test(val.value)){
            var create_div = document.createElement('div');
            var div_text = document.createTextNode(val.value);
            create_div.setAttribute('class', 'number');
            create_div.appendChild(div_text);
            document.body.insertBefore(create_div, document.querySelector('.number'));
            val.value = '';
          }
          else{
            alert("sdfds");
          }
        }

        //右侧入
        document.getElementById('right-in').onclick = function(){
          if(val.value !== ''){
            var create_div = document.createElement('div');
            var div_text = document.createTextNode(val.value);
            create_div.setAttribute('class', 'number');
            create_div.appendChild(div_text);
            var num1 = document.getElementsByClassName('number');
            var num2 = num1[num1.length];//插在最后一个
            document.body.insertBefore(create_div, num2);
            val.value = '';
          }
        }

        //左侧出
        document.getElementById('left-out').onclick = function(){
          var div_text = document.querySelector('.number');
          if(div_text !== null){
            alert(div_text.innerText);
            document.body.removeChild(div_text);
          }
        };

        //右侧出
        document.getElementById('right-out').onclick = function(){
          var div_text = document.getElementsByClassName('number');
          var class_number = div_text[div_text.length - 1];
          if(document.querySelector('.number') !== null){
            alert(class_number.innerText);
            document.body.removeChild(class_number);
          }
        };
        //点击元素 删除本身
        document.body.onclick = function(){
            var num = document.querySelectorAll('.number');
            //此处两种方法 使得动态添加的div点击函数生效 一种是注释了，一种是用闭包。最重要是找到不变的父元素，这样每次点击获取新的num
            //var ev = ev || window.event, target = ev.target || ev.srcElement;
            for(var i = 0; i < num.length; i++){
              //if(num[i] === target){
                //alert()
              //}
              (function (cur) {
                num[cur].onclick = function () {
                  document.body.removeChild(num[cur]);
                };
              })(i);
            }
          
        };
      })();
    </script>
  </body>
</html>
```

其他方法参考：[用原生实现点击删除点击的l](https://www.jianshu.com/p/09e94f89af9a)

[用原生实现点击删除点击的li]: https://www.jianshu.com/p/09e94f89af9a



































