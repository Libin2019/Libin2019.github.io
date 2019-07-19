---
title: 原生js实现轮播图(一)-js定时器实现动画效果
date: 2019-07-20 00:12:28
tags:
    -JavaScript
---

想尝试用原生js做一下轮播图的效果 ，在此之前，要先去实现一个轮播图中动画的过渡效果，实际上我们很容易的通过vue，或者jq实现一个轮播图，甚至css3也可以做到，但是本着原生大法好的原则，加深对基础js的理解及运用，话不多说 ，先看一下这个动画的Demo吧！

![](原生js实现轮播图-一-js定时器实现动画效果/jsAninmation_demo.gif)

可能是由于录制的原因，看上去过渡效果不是太流畅，实际上是没有这些问题的。贴一下代码，顺便记录一下思路
~~~
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>定时器运动</title>
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			.box1{
				width: 200px;
				height: 200px;
				background-color: yellow;
				position: relative;
			}
			.line{
				height: 800px;
				border-right: black 1px solid ;
				position: absolute;
				left: 800px;
			}
		</style>
	</head>
	<body>
		<div class="box1">
			
		</div>
		<div class="line">
			
		</div>
		
		<button type="button" class="btn">向右运动</button>
		<button type="button" class="btn5">向左运动</button>
		<button type="button" class="btn2">点击停止运动</button>
		<button type="button" class="btn3">点我到800px处自动停下</button>
		<script type="text/javascript">
			var box = document.querySelector(".box1");
			var box2 = document.querySelector(".box2");
			var btn = document.querySelector(".btn");
			var btn2 = document.querySelector(".btn2");
			var btn3 = document.querySelector(".btn3");
			var btn5 = document.querySelector(".btn5");
			var timer ;
			var timer2 ;
			btn.onclick = function(){
				clearInterval(timer);
				timer = setInterval(function(){
					var currentVal = getComputedStyle(box,null).left;
					box.style.left = parseInt(currentVal)+1+"px";
				},5)	
			}
			btn2.onclick = function(){
				clearInterval(timer)
			}
			btn5.onclick = function(){
				clearInterval(timer);
				timer = setInterval(function(){
					var currentVal = getComputedStyle(box,null).left;
					box.style.left = parseInt(currentVal)-1+"px";
				},5)
			}
			btn3.onclick = function(){
				clearInterval(timer);
				 timer = setInterval(function(){
					var currentVal = getComputedStyle(box,null).left;
					if(parseInt(currentVal) < 800){
						box.style.left = parseInt(currentVal)+1+"px";
					}else if(parseInt(currentVal) > 800){
						box.style.left = parseInt(currentVal)-1+"px";
					}else if( parseInt(currentVal) == 800){
						clearInterval(timer)
					}
					
				},5)	
			
			}
			
		</script>
	</body>
</html>
~~~

代码中没有什么特别需要注意的地方，基本上的逻辑就是 在运动前开启定时器，并通过`getComputedStyle()`属性去获取当前盒子移动的距离，left,这个属性获取到的是一个带px的字符串，所以咱们通过parseInt去转换为数字，通过该数字加或者减去每毫秒运动的直线距离，绑定按钮点击事件，从而达到使得盒子运动的过渡动画效果
Tip:在点击按钮事件是，我们第一件事是要去关闭上一次的定时器，如果不关闭，会出现 ：一直点击向左的按钮，那么这个盒子运动的速度会越来越快，关闭之后，再怎么点击，都不会出现盒子加速的后果。
