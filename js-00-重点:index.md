###设置鼠标样式

	cursor ： pointer
	
	
###数学函数 求平方

	Math.pow(a,b) 求a 的 b 次方,并返回结果
	
###轮播图中涉及知识点汇总

>**1、获取所有的点击事件及对象**
>**将外部js 引入**

	<script src="js/tween.js" type="text/javascript" ></script>
	<script type="text/javascript">
	
	var left = document.getElementById("left");
	var right = document.getElementById("right");
	var contentDiv = document.getElementById("content");
	var imgs = contentDiv.getElementsByTagName("img");
	var lis = document.getElementsByTagName("li");
	var index = 0 ;//记录图片下标
	contentDiv.style.width = imgs.length*imgs[0].offsetWidth+'px';//获取所有图片宽度
	</script>
	
	
>**2、上一张按钮的点击事件**	

	left.onclick = function () {
	//判断是第一张的时候，就赋值给最后一张
		if(index == 0){
			index=6;
			contentDiv.style.left = -imgs[0].offsetWidth*index + 'px';
		}
		index--；
		//开启定时器、轮播等操作
		scrollImg();
		changePoint();
	}


>**3、下一张按钮的点击事件**

	right.onclick = function () {
		if(index == 6){
			index=0;
			contentDiv.style.left = -imgs[0].offsetWidth*index + 'px';
		}
		index++;
		//开启定时和轮播操作
		scrollImg();
		changePoint();
	}
	
>**3、滚动动画的设置**


	引入第三方，tween 并对去参数进行设置
	
	function scrollImg(){
		var t=0;
		var start = contentDiv.offsetLeft;
		var change = -imgs[0].offsetWidth;
		var change = -imgs[0].offsetWidth*index-start;
		var d = 20;
		function move (){
			t++;
			contentDiv.style.left = Tween.Linear(t,start,change,d)+'px';
			if (t==d){
				clearInterval(timer);
			}
		}
		clearInterval(timer);
		timer = setInterval(move,50);	
	}	
	
	
>**4、设置小球位置及设置对应事件**

	//判断是哪个小球，然后对其余小球设置背景颜色恢复
	function changePoint () {
		for (var i = 0;i<lis.length;i++){
			lis[i].style.backgroundColor = "red";
		}else{
			lis[i].style.backgroundColor = "whitesmoke";
		}
		if(index == 6){
			lis[0].style.backgroundColor = "red";
		}
	}	
	
	//点击小球的时候，查找是哪个，并对其设置
	for(var i=0;i<lis.length;i++){
		lis[i].onmouseenter = function(){
			for(var j=0;j<lis.length;j++){
				if(this == lis[j]){
					index=j;
				}
			}
			//将改变图片函数和轮播函数调用
			scrollImg();
			changePoint();
		}
	}

	
>**5、实现自动切换**
	
	function autoChange (){
		if(index ==6){
			index =0;
			contentDiv.style.left = -imgs[0].offsetWidth * index + 'px'; 
		}
		index++;
		scrollImg();
		changePoint();
	}
	
	
>**6、对全局设置定时器**

	var timer;
	var timer2 = setInterval(autoChange,1000);
	var wrap = document.getElementById("wrap");
	//鼠标移出 ，开始新的定时器

	wrap.onmouseout = function(){
		timer2 = setInterval(autoChange,1000);
	}	
	//鼠标移入，关闭定时器
	wrap.onmouseover = function(){
		clearInterval(timer2);
	}
	
	
	
>**html部分**

	<div id="wrap">
			<div id="content">
				<img src="img/1.jpg"/>
				<img src="img/2.jpg"/>
				<img src="img/3.jpg"/>
				<img src="img/4.jpg"/>
				<img src="img/5.jpg"/>
				<img src="img/6.jpg"/>
				<img src="img/1.jpg"/>
			</div>
			<ul>
				<li class="li1">1</li>
				<li>2</li>
				<li>3</li>
				<li>4</li>
				<li>5</li>
				<li>6</li>
			</ul>
				<div id="left"><<</div>
				<div id="right">>></div>
		</div>
		
		
>**css 部分**

				*{
				margin: 0;
				padding: 0;
			}
			#wrap{
				width: 400px;
				height: 500px;
				border: 6px dashed bisque;
				margin: 0 auto;
				margin-top: 30px;
				position: relative;
				overflow: hidden;
			}
			#content{
				height: 500px;
				/*width: 99999px;*/
				position: absolute;
			}
			#content img{
				width: 400px;
				height: 500px;
				float: left;
			}
			ul{
				list-style-type: none;
				position: absolute;
				left: 30%;
				bottom: 10px;
			}
			ul>li{
				width: 20px;
				height: 20px;
				margin: 0 5px;
				background-color: whitesmoke;
				border-radius: 10px;
				float: left;
				text-align: center;
				line-height: 20px;
				font-size: 18px;				
			}
			#left,#right{
				position: absolute;
				top: 50%;
				color: black;
				width: 30px;
				height: 30px;
				background-color: #FFE4C4;
				line-height: 30px;
				text-align: center;
			}
			#right{
				right: 0;
			}
			.li1{
				background-color: red;
			}
			
			
###为所有的 li 对象添加点击事件

	var lis = document.getElementsByIagName('li');//获得所有 li，是个数组
	
	for (var i=0;i<lis.length;i++){
		lis[i].onclick = function(){
			for(var j=0;j<lis.length;j++){
				
			}
		}
	}
	

###对点击按钮设置

	for (var i=0; i<inputs.length;i++){
		inputs[i].index = i ;//记录按钮对应的值
		inputs[i].onclick = function (){
			
		}
	}
	
	
###记录点击事件

>**记录上一次点击事件，和本次点击事件**
>**思路：设置一个变量，用来存储上次点击按键的值**
	

	var previous = 1;//记录点击之前的上一个 a 的下标
	for (var i = 0;i<as.length;i++){
		as[i].onclick = function (){
			for (var j = 0; j<as.length;j++){
					if(this == as[j]){
					index = j;//记录下标
				}
			}
			previous = index ;
		}
	}
	
###洗牌算法

	function randomArray (arr){
		//遍历数组，依次洗牌
		for (var i=0; i<arr.length;i++){
		var num = randomNumber(0,arr.length-1){
				//如果随机的位置和当前位置不一致，进行交换位置，对应的值
				if(i !=num){
					var temp = arr[i];
					arr[i] = arr[num];
					arr[num] = temp;
				}
			}
		}
	}
	
	
	
**pointer-events 属性**

	none：元素不再是鼠标事件的目标，鼠标不再监听下面层中的元素，但是如果他的子元素设置了auto
	，那么鼠标还是会监听这个子元素的
	
	auto 鼠标不会穿透当前层
	
***

**到达文本最大框时，跳至下一个文本框**

	function checkLen(x,y){
		if (y.length==x.maxlength){
		var next = x.tabIndex
		if (next<document.getElementById("myForm").length){
		document.getElementById ("myForm").elements[next].focus()
		  }
		}	
	}	


*html部分*
	
	<form id="myForm">
		<input size="3" tabindex="1" maxlength="3" onkeyup="checkLen(this,this.value)">
		<input size="2" tabindex="2" maxlength="2" onkeyup="checkLen(this,this.value)">
		<input size="3" tabindex="3" maxlength="3" onkeyup="checkLen(this,this.value)">
	</form>

**带停止计时的计时器**
	
	var c=0
	var t
	function timedCount()
	{
	document.getElementById('txt').value=c
	c=c+1
	t=setTimeout("timedCount()",1000)
	}
	
	function stopCount()
	{
	clearTimeout(t)
	}

**时间**
	
	function startTime()
	{
	var today=new Date()
	var h=today.getHours()
	var m=today.getMinutes()
	var s=today.getSeconds()
	// add a zero in front of numbers<10
	m=checkTime(m)
	s=checkTime(s)
	document.getElementById('txt').innerHTML=h+":"+m+":"+s
	t=setTimeout('startTime()',500)
	}
	
	function checkTime(i)
	{
	if (i<10) 
	  {i="0" + i}
	  return i
	}


























<!---->