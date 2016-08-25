###ajax 

**ajax 的优势**
 
  1、异步加载数据无需切换页面
 
  2、更好的用户体验：局部刷新、即时验证 
 
  3、操作步骤简单化

**ajax使用步骤**

>1、new XMLHttpRequest() 创建ajax 对象
>
>2、open 创建请求
>
>3、send 发送请求
>
>4、onreadyStateChange 获取请求状态
>
>5、responseText 获取返回状态


**流程**

>1、创建XMLTttpRequest 对象
	
	if(window.XMLHttpRequest){
	//现代浏览器
		var http = new XMLHttpRequest();
	}else{
	//ie 低版本浏览器
		var http = new ActiveXObject("Microsoft.XMLHTTP");
	}
>2.open 创建一个请求，向服务器发送数据
	
	参数1：请求的方式
	参数2: 请求的地址
	参数3：是否异步请求，默认为 true	
	
	var url = "test.txt";
	http.open("GET",url,true);
	
>3.发送请求 send
	
	http.send(null);
	
>4、捕获请求状态 onreadystateChange
	
	http.onreadystatechange = function(){
		console.log(http.readyState);
	}		

>5、获取返回结果 responseText
	
	if(http.readyState ==4 && http.status >= 200 && http.status <300 || http.status == 304){
		console.log(http.responseText);
	}	

**原生js版本 ajax**

>1、var http = new XMLHttpRequest();//创建对象
>
>2、var url = "php.php"; http.open("get",url,true);
>
>3、http.send(null);//发送请求
>
>4、获取请求状态

	http.onreadystatechange = function(){
		if(http.readyState == 4 && http.status >= 200 && http.status < 300 || http.status == 304){
			//获取返回的信息
		}
	}
	
**JQ版本 ajax**	
	
	$.ajax({
		type:"get",
		url:"php.php",
		async:true,
		data:"user=wang&pass=22",
		data:{
			user:'什么',
			pass:12345
		},
		dataType:"json",//设置接收数据格式
		//success 设置接收数据后回调函数
		success:function(data){
			//请求成功后执行回调函数，并且将后台反馈数据以参数形式传递过来
		},
		error:function(){
			//请求失败也有回调函数
		}
	})
	
**简写ajax**

	$.get(参数1、参数2，参数3，参数4)
		参数1、url 即请求的地址
		参数2、用于向后台传输的数据
		参数3、function 一个回调函数，请求成功后执行
		参数4、设置数据类型
		
	var url = "php.php";
	$.get(url,{user:"aaa",pass:123},function(){
		//获取 的 data 数据
	})	
		


























	
	
<!---->	