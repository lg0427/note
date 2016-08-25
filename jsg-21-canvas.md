###canvas

**基础知识**
	
1、有两种填充方法
	
	context.fill()//填充
	context.stroke()//绘制边框
		
2、style 在进行图形绘制前设置好绘图的样式

	context.fillStyle //填充样式
	
	context.strokeStyle //边框样式
	
	context.lineWidth  // 图形边框宽度

3、路径设置
	
	context.beginPath();//开始绘图
	
	context.closePath();//结束绘图
	
>*系统会默认第一个路径为开始点，如果画完前面路径没有重新指定 beginPath,
>那么画其他路径的时候会将前面最近指定的beginPath 后的路径全部重新绘制*	
	
**基础参数设置**

|名称|作用|
|:--|:--|
|beginPath（）|开始绘制|
moveTo	| 设置绘制起点
lineTo	| 设置下一个点
closePath()	|结束绘制，闭合之前当前点到起点
strokeStyle	| 设置绘制的样式
stroke()	| 绘制点之间的路线
fillStyle | 设置填充样式
fill() |	填充当前绘图
lineWidth	|	线宽

**绘制直线**

	//获取canvas
	var canvas = document.getElementById("canvas1");
	//获取绘制环境
	var context = canvas.getContext("2d");
	
	context.beginPath();//开始绘制	
	context.moveTo(0,0);//设置起点
	context.lineTo(400,200);//设置下一个点
	context.closePath();//闭合
	
	context.strokeStyle = "red";//设置绘制样式
	context.stroke();//绘制
	
**填充内容**
	
	context.fillStyle = "red";
	context.fill();
	
**绘制矩形**
	
>1、strokeRect(x,y,w,h) 矩形的起始坐标，矩形的宽 、 高
>
>2、fillRect(x,y,w,h) 填充矩形边框
	
	context.strokeStyle = "red";
	context.lineWidth = 10;
	context.strokeRect(10,10,200,200);	
	
	//填充内容
	context.fillStyle = "red";
	context.fillRect(15,15,190,190);
	
**绘制圆形**

>context.arc(x,y,radius,starAngle,endAngle,anriclockwise)	
>
>x,y 圆心位置 、 radius 半径 、 起始和结束位置角度 、 
>anticlockwise 是否逆时针
	
	context.arc(100,100,200,0,Math.PI*2,true);
	

**绘制文字**

|标签|参数|
|:--|:--|
|strokeText()|绘制文字|
|fillText()|填充文字|
|createLineatGradient(x,y,x1,y1)|x,y:渐变开始点<br>x1,y1 渐变结束点|
|createRadialGradient(x,y,r,x1,y1,r1)|x,y,r:开始圆心坐标及半径<br>x1,y1,r1:结束圆心的坐标及半径|
|addColorStop(offset,color)|offset为设定的颜色设定渐变距离（0-1）|
|font|字体样式|

**设置阴影的属性和方法**

|名称|解释|
|:--|:--|
|shadowColor|阴影颜色|
|shadowOffsetX|x 方向偏移量|
|shadowOffsetY|y 方向偏移量|
|closePath()|结束绘制，连接当前点到起点，形成闭合图形|
|shadowBlue|设置阴影的模糊级别|

**二次贝瑟尔曲线**

>quadraticCurveTo(x,y,dx,dy);
>x,y 代表控制点，决定曲线的形状
>dx,dy 代表锚点，绘制的曲线会将最后一个点与锚点连接

**三次贝瑟尔曲线**

>bezierCurveTo(x,y,cx,cy,dx,dy)  创建一条表示三次贝瑟尔曲线的路径
>
>(x,y),(cx,cy)代表控制点，决定曲线的形状
>
>（dx,dy）代表锚点，将曲线最后的点与锚点连接
>


####图形变换

**平移translate()**

>添加到水平和垂直坐标上的值

	context.translate(100,100);
	
**rotate()**

>旋转角度以弧度计，如 5度 ：5*Math.PI/180
>
	context.rotate(Math.PI/4);
	
**scale()**
	
>两个参数是当前绘图的宽 高比
	
	context.scale(2,2);
	
####清理矩形区域
	
	clearRect(x,y,w,h);
	
	x,y 分别表示清除的起始点的坐标，w ,h 分别表示清理的矩形区域的宽和高
	
####存档与提档
	
	context.save();
	context.restore();
	
	context.save() 用来保存当前坐标系的状态
	context.restore() 用来提取之前的坐标系存档	
####图形的组合

>图形的组合方式参考图片显示
>
>source 汉语解释是：来源 ,理解为第一个图，方便记忆
>
>destination 汉语解释是：最终的，最后的 ，理解为后添加的图方便记忆

![图形的组合](/Users/lanouhn/Desktop/biji/imgs-for-md/combination.png)
	
	