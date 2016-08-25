###debugger 用于逐步调试

###swiper使用

>1、swiper.js 框架

>2、Swiper常用于移动端网站的内容触摸滑动

>3、Swiper是纯javascript打造的滑动特效插件，面向手机、平板电脑等移动终端。

>4、Swiper能实现触屏焦点图、触屏Tab切换、触屏多图切换等常用效果。

>5、Swiper开源、免费、稳定、使用简单、功能强大，是架构移动终端网站的重要选择！


####使用流程

>1、下载框架文件

>2、将压缩文件放在对应目录下

>3、将基础模板添加进来

>4、对应需要的格式，改变属性名称

**代码解析**

    var mySwiper = new Swiper ('.swiper-container', {
		  	effect : 'cube',
		  
	//设置滚轮点位置
	//	 direction: 'vertical',
		    loop: true,
		    
	// 设置分页器
	//	 pagination: '.swiper-pagination',
		    
	// 设置前进后退按钮
	    nextButton: '.swiper-button-next',
	    prevButton: '.swiper-button-prev',
		    
	// 设置滚动条
	//		 scrollbar: '.swiper-scrollbar',
		  })
	
***
	
###Touch.js

>1、下载Touch.js （或者使用百度CDN在线touch.js）
>
>2、Touch.js 函数中三个参数的使用
	
	参数1、执行该触摸事件的元素对象（对象或者选择器）
	
	参数2、手势事件类型 （添加多个事件，用空格隔开）
	
	参数3、函数（执行事件时触发的函数）
	
>3、将函数中对应的名称修改为自己需要的即可


**Touch 了解**

1、Touch.js是移动设备上的手势识别与事件库,由百度云Clouda团队维护，也是在百

度内部广泛使用的开发工具.
	
2、Touch.js的代码已托管于github并开源，希望能帮助国内更多的开发者学习和开发出优秀的App产品.
	
3、Touch.js手势库专为移动设备设计, 请在Webkit内核浏览器中使用.
	
	
	//touch.on(img1, 'touchstart', function(ev){
	
	//单指触发滚动事件
  	ev.startRotate();
  	
  	//关闭系统的滚动效果
  	ev.preventDefault();
  	});
	
	touch.on(img1, 'rotate', function(ev){
	
	  var totalAngle = angle + ev.rotation;
	  
	  if(ev.fingerStatus === 'end'){
	      angle = angle + ev.rotation;
	  }
	  
	 this.style.webkitTransform = 'rotate(' + totalAngle + 'deg)';
	});
	
**多个事件**

*swipe*

1、swipeleft 左轻扫

2、swiperight 右轻扫

3、swipeup   上轻扫

4、swipedown 下轻扫
	
***

###本地存储

**localStorage**

>HTML 5 版本新产生的一个技术点	
>
>注意：存储没有时间的限制

*存储数据*

>通过键值对的方式存储
	
	localStorage.sex = '男';
	等价于
	localStorage['sex'] = '男';
	
>添加键值对的另一种方式
>	setItem(key,value);

*获取值*

>localStorage.getItem('score');

*删除本地数据*

>通过key 值删除对应的键值对

	localStorage.removeItem('name');
	
>删除本地所有数据
	
	localStorage.clear();
	
*获取所有本地数据*

	for(var temp in localStorage){
		<!--遍历对象，得到的是key值，通过key值，获取key值对应的value值-->
		
		localStorage.getItem(temp);
	}

***

###Cookie

*cookie作用*

1、HTTP 协议是一个无状态协议，一旦传递完成，客户端和服务端就会断开，再次连接，需要再次请求

2、连接服务器后，为确认客户端身份，使用 cookie

	1、一个网站下的多个界面，共用一个cookie
	
	2、不同的浏览器使用不同的cookie
	
	3、不识别中文

*使用场景*

1、用户名和密码（保存用户的登录状态）

2、记录用户信息

3、购物车记录

*缺点*

1、容量小，只有 4k。

2、cookie 有条数限制： 最多20条

3、cookie可以被修改和删除

4、一般必须设置失效期

*添加cookie*

1、通过添加键值对来进行添加 (key 值此前不存在，添加，存在，覆盖)
	
	document.cookie = "userName=long";
	
	document.cookie = "sex=man";
	
*删除cookie*

	将key值赋值为空

1、设置失效日期，必须小于当前日期

2、对应的键值对失效
	

*失效的两种方式*

1、expires ： 失效日期，默认为当前日期

2、max-age ： 存活的时间（秒数），默认为-1.

3、同时设置expires 和 max-age ，以max-age 为主


###二维数组

*获取二维数组中元素*

	arr[m][n];
	
>外循环用数组总长度
>
>内循环用该下标对应长度

	for(var i=0;i<arr.length;i++){
		for(var j=0;j<arr[i].length;j++){
			
		}
	}

  
