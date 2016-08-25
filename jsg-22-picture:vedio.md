###canvas绘制
	
**绘制图片**

>1、创建图片 var img = new Image();img.src = "img/2.jpg";
>
>2、img.onload = function(){

	方法一:直接绘制，引入图片，确定起始坐标
	
		context.drawImage(img,100,100);
		
	方法二：绘制，引入图片，绘制起始坐标、确定宽高	
		context.drawImage(img,100,100,200,230);
		
	方法三：绘制，引入图片，图片上的截取坐标、截取宽高、画布上绘制点坐标、宽高	
		context.drawImage(img,100,100,200,230,200,200,200,300)
		
	}

*ps-给图片添加文字*

		var canvas = document.getElementById('myCanvas');
		var context = canvas.getContext('2d');
	
		var img = new Image();
		img.src = "img/zheng.jpg";//引入图片
	
		img.onload = function(){//当图片加载完成执行函数
		context.drawImage(img,0,0);//绘制图片到画布上
		var str = "飞呀";
		context.font = "10px 宋体";
		context.strokeStyle = "gray";
		context.strokeText(str,204,120);
	
		var url = canvas.toDataURL();//转换成图片地址
		
		}

*ps-像素处理*
	
>将彩色图片改变为黑白色
	
		var canvas = document.getElementById('myCanvas');
		var context = canvas.getContext('2d');
	
		var img = new Image();//创建一张图片
		img.src = "img/2.jpg";
		
		//当图片加载完毕执行该函数
		img.onload = function(){
			//将图片绘制到画布上
			context.drawImage(img,0,0);
			//获取整个画布上的所有像素点
			var imgData = context.getImageData(0,0,canvas.width,canvas.height);
			var imgPx = imgData.data;
			//遍历像素数组
			for(var i=0; i<imgPx.length; i+=4){
				var r = imgPx[i];
				var g = imgPx[i+1];
				var b = imgPx[i+2];
				//取灰色
				var gray = parseInt((r+g+b)/3);
				imgPx[i] = gray;
				imgPx[i+1] = gray;
				imgPx[i+2] = gray;
			}
			context.putImageData(imgData,0,0);
		}		

*刮刮乐-图层绘制*

		var canvas = document.getElementById('myCanvas');
		var context = canvas.getContext('2d');
		
		//绘制蒙层
		context.fillStyle = "gray";
		context.fillRect(0,0,canvas.width,canvas.height);
		
		//开刮
		canvas.onmousedown = function(){
		//鼠标点下并且移动才会有刮的效果
			canvas.onmousemove = function(e){
				var ev = e||window.event;
		//获取鼠标位置
				var x = ev.clientX - canvas.offsetLeft;
				var y = ev.clientY - canvas.offsetTop;
		//设置图形组合方案
				context.globalCompositeOperation = "destination-out";
		//设置橡皮擦的形状
				context.beginPath();
				context.arc(x,y,25,0,Math.PI*2,false);
				context.fillStyle = "red";
				context.fill();
				
		//获取画布上所有的像素点
				var imgData = context.getImageData(0,0,canvas.width,canvas.height);
		//获取像素数组
				var imgPx = imgData.data;
		//定义一个变量用来计数
				var num = 0;
				for(var i=3; i<imgPx.length; i+=4){
		//判断a的值是否为0
					if(imgPx[i] == 0){
						num++;
					}
				}
		//判断num是否达到总像素点数量的一半
		//计算出画布上总的像素点个数
				var all = imgPx.length/4;
				if(num/all>=0.5){
		//context.clearRect(0,0,canvas.width,canvas.height);
					canvas.style.opacity = "0";
					canvas.style.transition = "all 3s";
				}
				
			}
		}
		//当鼠标松开的时候停止清除
		document.onmouseup = function(){
			canvas.onmousemove = null;
		}
		
	

**绘制视频**

>1、获取

	var canvas = document.getElementById('myCanvas');
	var context = canvas.getContext('2d');
	var myvideo = document.getElementById('myVideo');
	
>2、视频准备完毕执行函数
	
	myvideo.oncanplay = function(){
		
		myvideo.play();//开始播放
		animate();
	}

>3、设置函数来绘制当前画面

	function animate(){
		if(!myvideo.ended){
			
			context.drawImage(myvideo,0,0,canvas.width,canvas.height);
			window.requestAnimationFrame(animate);
		
		}
	}	