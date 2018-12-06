# cookielist

大家都知道cookie的特性， cookie生效在同一个域名下，cookie储存量有限，cookie主要用于记录用户的一些信息，例如记录用户的登录信息使用户一段时间内不用登录，它有服务器创建，并放在客户端。

跨页面传值定义：统指WEB页面之间的传值，包括简单的页面表单传值和页面程序中的变量传值

以下仿写cookie的跨页面传值问题仿购物车案例，把```list```界面选定的数值跳转带到```shopCar```界面。

list界面：
```
<!doctype html>
<html lang="en">

	<head>
		<meta charset="UTF-8">
		<title>Document</title>
		<style>
			* {
				margin: 0 auto;
			}
			
			.content {
				width: 800px;
				height: 100px;
				background: #f9f9f9;
				border-radius: 5px;
				box-shadow: 0 3px 10px #666;
				margin: 50px auto;
			}
			
			.picwarp {
				width: 120px;
				height: 98px;
				border: 1px solid #fff;
				float: left;
			}
			
			.picwarp img {
				width: 100%;
				height: 100%;
			}
			
			.warp:after {
				content: '';
				display: block;
				clear: both;
			}
			
			.warp input {
				display: block;
				float: right;
				background: none;
				border: 2px solid #fff;
				border-radius: 2px;
				width: 80px;
				height: 30px;
				margin-top: 30px;
				margin-right: 30px;
			}
			
			.car {
				float: right;
				position: relative;
				width: 80px;
				height: 40px;
				color: red;
				font-size: 30px;
				font-weight: bold;
				right: -100px;
				top: -40px;
				background-image: url(images/1.png);
				background-size: 100% 90%;
				background-repeat: no-repeat;
			}
			
			.text {
				float: left;
			}
			
			.text h4 {
				padding-left: 40px;
				padding-top: 20px;
			}
			
			.text h3 {
				padding-top: 15px;
				padding-left: 40px;
				color: red;
			}
		</style>
		<script src='cookie.js'></script>
		<script>
			window.onload = function() {
				var add = document.getElementById('add');
				var redu = document.getElementById('reduce');
				var num = 0;
				var res = document.getElementById('num');
				var buy = document.getElementById('buy');
				add.onclick = function() {
					num++
					res.innerHTML = num;
				}

				redu.onclick = function() {
					if(num > 0) {
						num--
						res.innerHTML = num;
					}
				}
				buy.onclick = function() {
					var resNum = res.innerHTML;
					cookie.setCookie('num', resNum);
					window.location.href = 'shopCar.html'

				}
			}
		</script>
	</head>

	<body>
		<div class="content">
			<div class="warp">
				<div class="picwarp">
					<img src="images/2.png" alt="">
				</div>
				<div class="text">
					<h4>ins小清新玫瑰感化客厅装饰花瓶</h4>
					<h3>售价：18</h3>
				</div>
				<input type="button" id="buy" value='立即购买'>
				<input type="button" id='add' value='增加'>
				<input type="button" id='reduce' value='减少'>
			</div>

			<div class="car">
				<span class='num' id='num'>0</span>
			</div>

		</div>
	</body>
</html>
```

shopCar界面：


```
<!doctype html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	
	<style>
	#div1{
		width: 859px;
		height: 100px;
		line-height: 100px;
		border: 2px solid #b6b6b6;
		color: blueviolet;
		margin: 80px auto;
	
		font-size: 18px;
		text-align: center;
		
	}

	body{
		background:#f9f9f9;
	}
	
	</style>
</head>
<body>
	<div id='div1'></div>
</body>
<script src='cookie.js'></script>
	<script>
	window.onload=function(){
		var num=cookie.getCookie('num')
		var oDiv=document.getElementById('div1');
		if(num=='0'){
			oDiv.innerHTML='你没有选中任何商品';
			setTimeout(function(){
				window.location.href='list.html'

			},1000)

		}else{

			oDiv.innerHTML='我知道我要买'+num+'束漂亮的花朵！！心情美美哒！！！'+'<img src="images/2.png">';

		}
	}
	</script>
</html>
```

封装的cookie.js
```
var cookie={
    setCookie:function(name,value,date){
        var d=new Date();
        d.setTime(d.getTime()+date);
        document.cookie=name+'='+value+';expires='+d;
    },
    getCookie:function(name){
        var arr=document.cookie.split('; ');
        for(var i = 0 ; i < arr.length; i ++){
            var arr2=arr[i].split('=');
            if(arr2[0]==name){
                return arr2[1];
            }
        }

        return '';
    },
    removeCookie:function(name){
        cookie.setCookie(name,'',-1)
    }

}

```
效果：

![](https://upload-images.jianshu.io/upload_images/5640239-7b84e9c0bec8543f.gif?imageMogr2/auto-orient/strip)


*   [热门推荐：前端，Java，产品经理，微信小程序，Python等资源合集大放送](https://www.jianshu.com/p/e8197d4d9880)

> 原文作者：祈澈姑娘；技术博客：https://www.jianshu.com/u/05f416aefbe1
> 90后前端妹子，爱编程，爱运营，爱折腾。 坚持总结工作中遇到的技术问题，坚持记录工作中所所思所见，欢迎大家一起探讨交流。
