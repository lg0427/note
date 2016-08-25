###做游戏需要的简单地图
	
>1、打开绘图软件 tiled
>
>2、将想要绘制的原图放入
>
>3、生成新图形后，保存为js 文件
>
>4、将js文件中的 地图地址复制下来

	
	简单示例：
		<!--1、将上下文元素和地图坐标获取-->
		var canvas = document.getElementById('myCanvas');
		var context = canvas.getContext('2d');
		var mapIndex = [0, 0, 0, 0, 0, 0, 0, 0,
		0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 
		0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0,
		0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 0,
		0, 0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 
		0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1,
		0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0,
		0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0];
		
		<!--将用于绘制地图的图像引入-->
		var img = new Image();
		img.src = "img/map.jpg";
		
		function Maps(x,y){
			this.x = x;
			this.y = y;
			this.w = 50;
			this.h = 50;
			this.draw = function(){
			context.drawImage(img,0,0,50,50,this.x,this.y,50,50);
			
			}
		}
		var mapArr = [];
		<!--遍历设置画板上的位置进行绘制
			*10 是之前将画布设置为10等分-->
			
			
		for (var i=0;i<10;i++){
			for(var mapIndex[i*10+j]!=0){
				var map = new Maps(j*50,i*50);
				mapArr.push(map);
			}
		}
		<!--绘制地图-->
		
		img.onload = function(){
			for(var i=0;i<mapArr.length;i++)
			mapArr[i].draw();
		}
		
		
###**圆形碰撞**

	
>1、获取画布及上下文
	
	var canvas = document.getElementById("mycanvas");
	var context = canvas.getContext("2d");
	
	
>2、创建两个对象
	
	var rec1 = {
		x:100,
		y:100,
		r:50,
		color:"red"
	}		
	var rec2 = {
		x:300,
		y:250,
		r:100,
		color:"blue"
	}
	var arr = [rec1,rec2];
	function draw(obj){
		context.beginPath();
		context.arc(obj.x,obj.y,obj.r,0,Math.PI*2,false);
		context.fillStyle = obj.color;
		context.fill();
	}	
	<!--遍历数组来绘制图形-->
		
	for(var i =0;i<arr.length;i++){
		draw(arr[i]);
	}		
	
>鼠标移入进行判断
		
	<!--鼠标事件-->
	
	var n;
	canvas.onmousedown = function(e){
	<!--获取鼠标坐标-->
		var e = e||window.event;
		var clicx = e.clientx - canvas.offsetLeft;
		var clicy = e.clienty - canvas.offsetTop;
		
		for(var i=0;i<arr.length;i++){
		<!--鼠标移动监听-->
			if (context.isPointInPath(clicx,clicy)) {
			n=i;
			var disx = clicx - arr[n].x;
			var disy = clicy - arr[n].y;
			canvas.onmousemove = function(e){
				context.clearRect(0,0,canvas.width,canvas.height);
				var e= e||window.event;
				var x = e.clientX - canvas.offsetLeft - disx;
				var y = e.clientY - canvas.offsetTop - disy;
				arr[n].x = x;
				arr[n].y = y;
				for(var i=0;i<arr.length;i++){
					draw(arr[i]);
				<!--判断另外一个对象-->
					if(i!=n){
						if(crash(arr[i],arr[n])){
							console.log("撞上");
						}
					}
				}
			}
		}
	}	
}		
>鼠标移出，解除 move事件
	
	document.onmouseup = function(){
		canvas.onmousemove = null;
	}		
	
>设置碰撞函数判断
	
	function crash(obj1,obj2){
		var disx = Math.abs(obj1.x - obj2.x);//取绝对值
		var disy = Maht.abs(obj1.y - obj2.y);
		
		var sum = obj1.r+obj2.r;
		if (Math.sqrt(disx*disx + disy*disy) <=sum){
			return true;
		}else{
			return false;
		}
	}		
		
		
###**矩形碰撞**
	
	//	设置碰撞函数
	function crash(obj1,obj2){
		var l1 = obj1.x;
		var r1 = l1 + obj1.w;
		var t1 = obj1.y;
		var b1 = t1 + obj1.h;
		
		var l2 = obj2.x;
		var r2 = l2 + obj2.w;
		var t2 = obj2.y;
		var b2 = t2 + obj2.h;
		
		if(l1<r2 && r1>l2 && t1<b2 && b1>t2){
			return true;
		}else{
			return false;
		}
	}		
		
###**拖拽与仿重力**

>将上一次鼠标事件记录	

	<!--存储上一次鼠标的位置-->
	var lastx = 0;
	var lasty = 0;
	
	var ball = {
		x:100,
		y:100,
		r:50,
		color:"red",
		speedx:0,
		speedy:0,
		<!--绘制方法设置-->
		draw:function(){
			context.beginPath();
			context.arc(this.x,this.y,this.r,0,Math.PI*2,false);
			context.fillStyle = this.color;
			context.fill();
		}
	}		
		
	ball.draw();
	
>鼠标移动事件监听
	
	canvas.onmousedown = function(e){
		var e = e||window.event;
		var clicx = e.clientX - canvas.offsetLeft;
		var clicy = e.clientY - canvas.offsetTop;
		<!--鼠标移动，就重新绘制-->
		<!--isPointInPath监听事件-->
		if(context.isPointInPath(clicx,clicy)){
			canvas.onmousemove = function(e){
				context.clearRect(0,0,canvas.width,canvas.height);
				var e = e||window.event;
				var x = e.clientX - canvas.offsetLeft;
				var y = e.clientY - canvas.offsetTop;
				
				ball.speedx = x - lastx;
				ball.speedy = y - lasty;
				
				lastx = x;
				lasty = y;
				
				ball.x = x;
				ball.y = y;
				ball.draw();
			}
		}
	}	
		
>鼠标移开就清理
	
	document.onmouseup = function(){
		canvas.onmousemove = null;
		move();
	}		
		

>用计时器来定时，改变碰撞后反弹及减速
	
	var time = null ;
	function move (){
		clearInterval(time);
		time = setInterval(function(){
			context.clearRect(0,0,canvas.width,canvas.height);
			ball.speedy += 2;
			ball.y += ball.speedy;
			ball.x += ball.speedx;
			if(ball.x >= canvas.width - ball.r){
				ball.x = canvas.width - ball.r;
				ball.speedx *= -0.8;
				ball.speedy *= 0.8;
			}
			if(ball.x <= ball.r){
				ball.x = ball.r;
				ball.speedx *= -0.8;
				ball.speedy *= 0.8;
			}
			if(ball.y >= canvas.height - ball.r){
				ball.y = canvas.height - ball.r;
				ball.speedy *= -0.8;
				ball.speedx *= 0.8;
			}
			if(ball.y <= ball.r){
				ball.y = ball.r;
				ball.speedy *= -0.8;
				ball.speedx *= 0.8;
			}
			if(Math.abs(ball.speedx)<1){
				ball.speedx = 0;
			}
			if(Math.abs(ball.speedy)<1 && ball.y>=canvas.height-ball.r && ball.speedx==0){
				ball.speedy = 0;
			}
			ball.draw();			
		},30)
	}		
		
		
###贪吃蛇
	
			
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
	<!---->	