---
title: 'css-vw,vh'
date: 2019-11-06 21:21:21
tags:
    - Html+Css基础
---
# <center>基础为重！！！关于vw和vm的响应式应用<center>
面试题，分享一波，主要是关于对响应式的css属性**vh-vw**的考察，以及对布局的整体考察。
![](css-vw-vh/test.jpg)
~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>demo</title>
  <style>
    body{
      padding: 0;
      margin: 0;
    }
    .container{
      width: 100vw;
    }
    .nav{
      height: 19vh;
      background-color: blue;
    }
    .aside{
      height: 81vh;
      width: 16vw;
      float: left;
      background-color: green;
    }
    .main{
      float: left;
    }
    .top div{
      float: left;
      width: 21vw;
      height: 27vh;
    }
    .middle div{
      float: left;
      width: 28vw;
      height: 27vh;
    }
    .box{
      background-color: aqua;
    }
    .box2{
      background-color: blueviolet;
    }
    .box3{
      background-color: brown;
    }
    .box4{
      background-color: chartreuse;
    }
    .box5{
      background-color: deeppink;
    }
    .box6{
      background-color: pink;
    }
    .box7{
      background-color: hotpink;
    }
    .footer div{
      float: left;
      width: 42vw;
      height: 27vh;
    }
    .box8{
      background-color: darkorange;
    }
    .box9{
      background-color: firebrick;
    }
    .clearfix:after{
      display: inline-block;
      content: '';
      clear: both;
    }

  </style>
</head>
<body>
<div class="container">
  <div class="nav"></div>
  <div style="width:100vw">
    <div class="aside"></div>
    <div class="main ">
      <div class="top">
        <div class="box"></div>
        <div class="box2"></div>
        <div class="box3"></div>
        <div class="box4"></div>
      </div>
      <div class="middle">
        <div class="box5"></div>
        <div class="box6"></div>
        <div class="box7"></div>
      </div>
      <div class="footer">
        <div class="box8"></div>
        <div class="box9"></div>
      </div>
    </div>
  </div>
</div>
</body>
</html>

~~~ 
###效果：
![](css-vw-vh/test.gif)
