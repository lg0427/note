###点击事件监听
	
**isPointInPath() 来判断是否点击到图形**
	
	if(context.isPointInPath(x,y)){
		//添加需要的函数
	}
	
	
**调用自己，清理掉计时器**
	
	function move(){
	n++;//调用自己
	time = window.requestAnimationFrame(move);
	}	
	
	window.cancelAnimationFrame(time);
	
###图片的循环播放

**重复绘制、获取当前空白内容用新的图片填充**
	
	var img = new Image();
	img.src = "img/background.png";//将需要的图片引入
	
	bgimg = {
		x:0,
		y:0,
		w:canvas.width,
		h:canvas.height,
		//创建绘制的方法
		draw:function(){
			//不断改变 y 的值实现滚动效果
			this.y++;
			if(this.y>=canvas.height){
				this.y = 0;
			}
			context.drawImage(img,this.x,this.y,this.w,this.h);
			context.drawImage(img,this.x,this.y-canvas.height,this.w,this.h);
		}
	}
	//设置计时器
	setInterval(function(){
		context.clearRect(0,0,canvas.width,canvas.height);
		bgImg.draw();
	},30);

**规则性运动-圆周运动**

>1、计算圆心的运动轨迹函数

	function circle(x,y,r,angle){
	
	var arcx = x + r* Math.cos(angle);
	var arcy = y + r* Math.sin(angle);
	
		return [arcx,arcy];//返回x y 坐标值放入数组
	}

>2、运动函数
	
	var n = 0;//定义一个变量来实现角度的变化
	function move(){
		n++;
		var ang = n/180*Math.PI;
		//清理画布
		context.cleatRect(0,0,canvas.width,canvas.height);
		var x = circle(250,250,200,ang)[0];//将函数返回值的第一个赋给x
		var y = circle(250,250,200,ang)[1];
		//开始绘制小球
		context.beginPath();
		context.arc(x,y,10,0,Math.PI*2,false);
		context.fillStyle = "red";
		context.fill();
	}

>3、用一个定时器：调用函数

	setInterval(move,30);
	
	
###图形的移动等问题

**模拟重力效果**
	
>1、创建小球对象
	
	var ball = {
		x:200,
		y:50,
		r:50,
		speedy:0,
		draw:function(){
			context.beginPath();
			context.arc(this.x,this.y,this.r,0,Math.PI*2,false);
			context.fillStyle = "red";
			context.fill();
		}
	}

>2、先画出小球
	
	var time = null;
	ball.draw();
	
	canvas.onclick = function(){
	//开始计时器
	time = setInterval(function(){
	ball.speedy += 2;
	context.clearRect(0,0,canvas,width,canvas.height);
	ball.y += ball.speedy;
	
	//判断临界值
	if(ball.y>=canvas.height - ball.r){
	ball.y = canvas.height - ball.r;
	//改变速度方向实现反弹
	ball.speedy *= -0.8
	}
	if(Math.abs(ball.speedy)<1&&ball.y>=canvas.height-ball.r){
		ball.speedy = 0;//速度归零
	//清除计时器
	clearInterval(time);
	}
	ball.draw();
	},30)
	}



















	
<!---->		