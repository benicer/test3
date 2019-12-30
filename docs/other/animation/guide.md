# 动画研究

## 动画简介

经过测试，ec6108v9的盒子可以使用css3的动画特性

## transform

```
-webkit-transform: rotateY(0deg)

div[i].style.webkitTransform = 'translateX(' + tempLeft + ')';
```

## keyframe

```
        @-webkit-keyframes mymove /* Safari and Chrome */
            {
                from {left:1280px;}
                to {left:0px;}
            }
        div
            {
                width:1280px;
                height:720px;
                position:relative;
                -webkit-animation:mymove 5s infinite; /* Safari and Chrome */
            }


```

## transition

```
-webkit-transition: -webkit-transform 2s;

-webkit-transition: width 2s;
```

## 通过js触发伪类

```
#border-radius:hover,
#border-radius.hover {
    -webkit-animation: border-radius 1s infinite alternate;
    -webkit-transform: perspective(400px) rotateY(0deg)
}

divo.className = 'hover';
```

## requestAnimationFrame兼容写法

```
window.requestAnimFrame = (function(){
		return  window.requestAnimationFrame || 
		window.webkitRequestAnimationFrame   || 
		window.mozRequestAnimationFrame      || 
		window.oRequestAnimationFrame        || 
		window.msRequestAnimationFrame       || 
		function( run ){
			window.setTimeout(run, 16);
		};
})();
```