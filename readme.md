# canvas notes
```
  <canvas id="tutorial" width="150" height="150">这是替代内容，在浏览器不支持canvas的情况下，显示的内容</canvas>
```
## canvas的用法， 和普通的标签使用一样， 下面是一段完整地例子：
```
<html>
 <head>
  <script type="application/javascript">
    function draw() {
      var canvas = document.getElementById("canvas");
      if (canvas.getContext) { //这里是判断， 当前是否支持canvas
        var ctx = canvas.getContext("2d"); // 获取canvas 元素的上下文

        ctx.fillStyle = "rgb(200,0,0)";
        ctx.fillRect (10, 10, 55, 50);

        ctx.fillStyle = "rgba(0, 0, 200, 0.5)";
        ctx.fillRect (30, 30, 55, 50);
      }
    }
  </script>
 </head>
 <body onload="draw();">
   <canvas id="canvas" width="150" height="150"></canvas>
 </body>
</html>
```
# canvas只支持两种形式的图形：矩形和路径。所有类型的图形都是通过一条路径或者多条路径的组合形成的。
```
fillRect(x, y, width, height) // 绘制一个填充的矩形
strokeRect(x, y, width, height) // 绘制一个矩形的边框
clearRect(x, y, width, height) // 清楚一个指定区矩形区域，让清楚区域完全透明
```
## 下面是一个完整地代码实例：
```
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext) {
    var ctx = canvas.getContext('2d');

    ctx.fillRect(25, 25, 100, 100);
    ctx.clearRect(45, 45, 60, 60);
    ctx.strokeRect(50, 50, 50, 50);
  }
}
```
![矩形])(image\react.jpg)