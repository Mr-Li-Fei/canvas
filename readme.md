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
## 绘制矩形
```
fillRect(x, y, width, height) // 绘制一个填充的矩形
strokeRect(x, y, width, height) // 绘制一个矩形的边框
clearRect(x, y, width, height) // 清楚一个指定区矩形区域，让清楚区域完全透明
rect(x, y, width, height) // 绘制一个左上角坐标为（x,y），宽高为width以及height的矩形
```
### 下面是一个完整地代码实例：
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
![矩形])(./image/react.jpg)
## 绘制路径
1. 首先，你需要创建路径起始点。
2. 然后你使用[画图命令](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D#paths)去画出路径。
3. 之后你把路径封闭。
4. 一旦路径生成，你就能通过描边或填充路径区域来渲染图形。
### 以下是对常用且简单的语法记录
```
beginPath() //新建一条路径，就是重新开始画一条路径, 图形绘制命令被指向到路径上生成路径
closePath() // 闭合路径， 就是当前的路径被关闭，图形绘制命令又重新回到了上下文中，不是必须使用来关闭路径，fill()也可以实现自动闭合路径
fill() //填充路径的内容区域生成实心的图形
stroke() // 通过线条绘制图形轮廓
moveTo(x,y) // 就是结束上一条路径， 从另一个(x,y)点开始一段路径绘制
lineTo(x,y) // 语义化，就是连接到(x,y)坐标点;
```
## 画圆
### arc(x, y, radius, startAngle, endAngle, anticlockwise) //画圆或者圆弧，画一个以(x,y)为圆心，半径为redius, 从开始弧度startAngle 到结束弧度 endAngle（弧度=(Math.PI/180)*角度。）, 以anticlockwise的值来实现顺时针或者是逆时针画圆。
```
function draw() {
  var canvas = document.getElementById('canvas');
  if (canvas.getContext){
    var ctx = canvas.getContext('2d');

    for(var i = 0; i < 4; i++){
      for(var j = 0; j < 3; j++){
        ctx.beginPath();
        var x = 25 + j * 50; // x 坐标值
        var y = 25 + i * 50; // y 坐标值
        var radius = 20; // 圆弧半径
        var startAngle = 0; // 开始点
        var endAngle = Math.PI + (Math.PI * j) / 2; // 结束点
        var anticlockwise = i % 2 == 0 ? false : true; // 顺时针或逆时针

        ctx.arc(x, y, radius, startAngle, endAngle, anticlockwise);

        if (i>1){
          ctx.fill();
        } else {
          ctx.stroke();
        }
      }
    }
  }
}
```
## 贝塞尔曲线 (一般用来绘制复杂有规律的图形)
### quadraticCurveTo(cp1x, cp1y, x, y) // 绘制二次贝塞尔曲线，cp1x,cp1y为一个控制点，x,y为结束点。
### bezierCurveTo(cp1x, cp1y, cp2x, cp2y, x, y) // 绘制三次贝塞尔曲线，cp1x,cp1y为控制点一，cp2x,cp2y为控制点二，x,y为结束点。

