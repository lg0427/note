##前端

>1、nodejs 不是一个框架，是js运行环境，类似与java中的jvm
>"全站程序员"
>2、js mvc框架 比较有名的是：expressjs 
	
	基于 nodejs：
			1、Sails.js Total.js Partial.js Koa.js
			2、locomotive.js Express.js Flatiron.js
>3、reactjs fackbook 出的http://facebook.github.io/react/
>4、reactjs 最大的作用用来开发ui组件，特点是 可以封装大量代码
>5、coolie 先入手
>
##可以到

>1、慕课网
>
>2.网易云课堂
>
>3、菜鸟
>
##高级

setAttribute() 方法添加指定的属性，并且为其赋指定值

原生js 获取index 以及 获取indexof

小括号总是计算出他内部的运算结果并返回给上下文

**repl (交互式解释器)**
	
	read / eval / print / loop 
	
##链接mongo数据库
	终端输入：mongod --dbpath文件直接拖入
	
	成功后mongo
	
	成功后 db
		
	
##node

**http**	

*链接http*
	
	//创建一个node服务，需要引入一个 http 模块
	var http = require("http");
	
	//创建服务
	var server = http.createServer(function (req,res){
		//req request 传入的参数
		//res response 返回的数据
		res.setHeader("content-type","text/html;charset=utf-8");
		res.write("可以写入");	
		
		//end 方法里面必须传字符串
		res.end("字符串才能执行");
	})
	
	//监听的端口
		server.listen(8080);
		
	//连接成功
		console.log("连接成功");	
		

**分析链接**

	var http = require("http");
	var server = http.creatServer(function(req,res){
		res.setHeader("content-type","text/html;charset=utf-8");
		
		/*
			url:"/" //路径
			method:'get' //传入方式
			shift+ctrl+/ 多层注释
		*/
		
		var str = "";
		if(req.url == "/"){
			str = "您访问的是首页"；
		}else if (req.url=='index.html){
			str = "小桥流水";
		}else {
			str = "触发错误";
		}
		
		res.end(str);
	});		
		
		//监听端口
		server.listen(8080);
		
		//连接成功
		console.log("连接成功");
		
		
###引入块
	
	var http = require("http");//引入一个http 模块
	var url = require("url")；
	var server = http.creatServer(function (req,res){
		res.setHeader("content-type","text/html;charset=utf-8");
		var urlObj = url.parse(req.urlm,true);//添加true 将query 转为对象格式
		var querys = urlObj.query;
		console.log(querys.name);
		res.end("结束");//用于告诉客户端传输已经完成，必须调用一次，不然会让客户端一直处于等待状态
	});	
	server.listen(8080);
	console.log("连接成功");
	
	
**引入自己写的**
	
		自己建的块 文件名必须为： node_modules 下面的home 文件夹下
	包含 package.json 文件，用来决定文件指向
	指向的js 文件是在package.js 中用 “main”:"js文件名" 来指定

*自己创建模块注意*
	
	一定使用var 声明变量
	如果不使用 var ，那么就是全局变量，这样会导致污染整个项目
	
	//设置函数
	var which = function(m){
		if(m>90){
			console.log("大数据");
		}else{
			console.log("有点小");
		}
	} 
	var randoms = function (m,n){
		console.log(Math.floor(Math.random()*(n-m+1)+m))；
	}；
	//建立模块
	module.exports = {
		"which":m,
		"randoms":randoms
	};
	
	package.json 中添加： "main":"home.js"	
	
*引用自建模儿*
	var col = require("home.js");
	col.which(99);
	col.randoms(29,40);
	
**引入工具模块-util 三个功能**
	
	1、继承
	2、输出对象
	3、查看类型	
	
	var  util = require ("util");//引入 util 模块儿
	
	//设置构造函数
	function Parent(name){
		this.name = "刘备"；
		this.act = function (){
			console.log("卖草鞋");
		}
	};
	Parent.prototype.dream = function(){
		console.log("三锅");
	};
	
	//继承只能继承原型的方法
	function Son(name){
		Parent.call(this,name);
	};	
	//继承
	util.inherits(Son,Parent);
	
	var  liubei = new Parent("刘备");
	var liushan = new Son("刘禅");	
	
	liushan.dream();
	liushan.act();
	
*引入对象以及判断数据类型*
	
	var util = require("util");
	var arr = [1,2,3];
	
	//输出对象
	console.log(util.inspect(arr));
	
	//查看数据类型
	console.log(util.isArray(arr))；	
	
###Ctrl+c 退出	

###fs相关
	
**读取文件**

	var fs = require("fs");		
	//读取文件 异步操作
	fs.readFile('a.txt','utf-8',function(err,data){
		if(err){
			return console.error(err);
		}
		console.log(data);
	});
	//读取文件 同步 阻塞
		var data = fs.readFileSync("a.txt","utf-8");
		console.log(data);
		
**添加文件**
	
	var fs = require("fs");
	//flag 有两个参数： a 代表追加内容 w代表覆盖
	fs.writeFile("a.txt","花落人亡两不知"，{flag:"a"}，function (){
		console.log("一支红杏出墙来");
		fs.readFile("a.txt","utf-8",function(err,data){
			if(err){
				return console.error(err);
			}
			console.log(data);
		});
	});
	
**查询文件**

	var fs = require("fs");		
	fs.readdir("test1",function(err,file){
		if(err){
			return console.error(err);
		}else{
			console.log(file);
		}
	});	
	//文件详情
	fs.stat("test1",function(err,stat){
		if(err){
			return console.error(err);
		}else{
			console.log(stat);
		}
	});
	//修改文件名
	fs.rename("test","test2",function(err){
		console.log("恭喜你")；
	})；

**复制文件**	
	
	var fs = require("fs");
	var data = fs.readFileSync("a.txt","utf-8");
	console.log(data);
	fs.appendFile("a.txt",data,"utf-8",function(){
		fs.readFile("a.txt","utf-8",function(err,data){
			if(err){
				return console.log(err);
			}
			console.log(data);
		})
	});
	
*封装 拷贝函数*
	
	function copy(a,b){
		fs.readFile(a,function(err,data){
			fs.writeFile(b,data,function(){
				console.log("复制成功");
			})
		})
	}
	copy ("a.jpg","b.jpg")；
	
**创建目录**
	
	var fs = require("fs");
	fs.mkdir("test",0777,function(err){
		if(err){
			return console.error(err);
		}
		console.log("创建成功");
	});	

**权限问题**

>0777 含义
>
>0 不用操作
>
>第一个位置代表	本用户
>
>第二个位置代表	组用户
>
>第三个位置代表	所有用户
>
>1：执行权限
>
>2：写入权限
>
>3：读取权限	
		
###文件操作

>文件操作解决速度问题
>
>流 专门操作大数据

	var fs = require("fs");
	
	//创建可读流
		var rs = fs.creatReadStream("b.jpg")；
	//创建一个可写流
	var ws = fs.createWriteStream("c.jpg");
	rs.pipr(ws)；	//流操作 简单粗暴版
	
**路径规范化**
	
	//引入路径模块儿
	var path = require("path")；
	console.log(path.normalize("a/d/s///d//d../"));//规范化字符路径 normalize
	console.log(path.join("wwwroot",'dd/ss.dd///sd','ddd/img/a.jpg'));//合并路径的方法:合并字符串让其变为有效路径 join
	
	console.log(path.join(__dirname));//两个下划线 获取根目录
	
##获取传入的用户名和密码，以及获取图片

	var http = require("http");
	var url = require("url");
	var fs = require("fs");
	var formidable = require("formidable");	
	var server = http.createServer(function(req,res){
		res.setHeader("content-type","text/html;charset=utf-8");
		
		var murl = req.url;
		var mmethod = req.method;
		var urlObj = url.parse(murl,true);
		if(urlObj.pathname == "/"||urlObj.pathname=="/post.html"){
			var rs = fs.creatReadStream("post.html");
			rs.pipe(res);
		}else if(urlObj.pathname = "/post"){
			var forms = new formidable.IncomingForm();
			forms.parse(req,function(err,fields,files){
				var rs = fs.creatReadStream(files.file.path);
				var ws = fs.creatWriteSteam('../images/'+files.file.name);
				rs.pipr(ws);
				res.end(JSON.stringify(fields));
			});
			console.log(urlObj);
		}else{
			res.statusCode = "404";
			res.end("没有找到文件");
		}
	}) 	;
		server.listen(8080);
		console.log("成功")；

**html代码**
	
*enctype 传文件的时候用*
	
	<form action="/post" method="post" enctype="multipart/form-data">
	        用户名: <input type="text" value="" name="name" /><br/>
	        密码:<input type="password" value="" name="pass" /><br/>
	        <input type="file" name="file" >
	        <input type="submit" value="提交">
    </form>	
			
##angular

**即时获取特性**
*引入js后直接写格式框架*
	
	<script type="text/javascript" src="../js/angulat.min.js"></script>
	<div ng-app="" ng-init="a=2;b=3">
		<input type = "text" ng-model="a">X		<input type = "text" ng-model="b">={{a*b}}	</div>	

**ng 指令**				
>
>ng-app 使用angular 必须引用该指令，是指angular 的工作区域
>
>ng-init 理解为：angular 的数据源
>
>ng-model 理解为：他是先找到 最外层的 ng-app 然后在作用域内查找他自己
>view 位置给予显示
>
>ng-bind 绑定
>
>ng-selected 没有选择时候的值
>
>ng-click 点击绑定的元素 点击触发
>
>ng-show 当他的值为true 时候，显示元素 实质是 display：block
>
>ng-hide 当他的值为false 时候，隐藏元素，实质是 display：none
>
>双大括号 里面绑定数据

**点击显示demo**
	
	<div ng-app="" ng-init="isBool=true;ks=false">
		<span class="btn" ng-click= "isBool=!isBool">问君能有几多愁</div>		<input class= "div" ng-show= "isBool">点击切换的</div>	</div>	

**switch**
	
>点击将依次对应的值显示，如果没有对应的就默认为0
	
	<div ng-app="" ng-init= "n=0" ng-switch= "" on="n">
		   <p ng-switch-default= "0">0</p>		   <p ng-switch-when="1">1</p>
	        <p ng-switch-when="2">2</p>
	        <p ng-switch-when="3">3</p>
	        <p ng-switch-when="4">4</p>
	        <p ng-switch-when="5">5</p>
	  </div>
	  <input type="button" class = "btn"  ng-click =  "n=n+1">
	
**遍历操作**
	
>angular 使用 input 必须添加一个 ng-model
>
	<div ng-app="" ng-controller= "myCtrl" >		<ul>
			<li ng-repeat = "i in data">{{i.name}}{{i.age}}</li>		</ul>	
		<input type= "button" value = "点击" ng-click = "myClick()" class = "btn" ng-model = "a">
	</div>	
				
>创建一个module 两个参数：参数一：app 名称 参数二：引入依赖，也就是 angular 模块儿，是一个数组形式，可以同时引用 多个模块
>	
>
>创建controller 两个参数1：controller 第二个是：执行函数 
>
>$scope 链接 module 和 view 的数据传递桥梁
	
	<script type="text/javascript" src="../js/angular.min.js"></script>
	<script type = "text/javascript">
		var app = angular.module("myApp",[]);
		app.controller("myCtrl",function($scope){
			$scope.data = [
				  {name:"康熙",age:16},
				  {name:"王宗智",age:18},
	                {name:"王献之",age:18},
	                {name:"王羲之",age:18},
	                {name:"成吉思汗",age:18}
			];
			//创建点击事件
			$scope.myClick = function(){
				alert("弹出");
			}
			//声明一个 booler 值
			$scope.isBool = true;
			$scope.myClickBool = function(){
				$scope.isBool = !$scope.isBool;
			};
		});
	</script>
	
**绑定**
	
	<div ng-app="" ng-coltroller = "myCtrl">		<select name="" >	
				<option ng-repeat="item in data">{{item.name}}</option>
		</select>		
	<p>您选择了{{myselcet.name}},他是{{myselcet.age}}岁
	</div>
	<script type="text/javascript" src="../js/angular.min.js"></script>
	<script type="text/javascript">
	    var app = angular.module("myApp",[]);
	    app.controller("myCtrl",function($scope){
	        $scope.asd = "错错错";
	        $scope.data=[
	            {name:"康熙",age:18},
	            {name:"王宗智",age:18},
	            {name:"王献之",age:18},
	            {name:"王羲之",age:18},
	            {name:"成吉思汗",age:18}
	        ];
	    });
	</script>

**jsonp处理**
	
>引入 angular.min.js 以及 angular-sanitize.min.js 文件
>
>module 引入 sanitize 将名字改为 ngSanitize 理解为 首字母大写前加 ng
>
>创建指令关键字： directive  参数一：指令名 参数二：回调函数
>
>restrict 规定指令的引用方式：有 A C E 三种，默认 A 的属性
>
>A : 属性方式引用 	C ：class 方式引用   E ：标签方式引用
	
	var app = angular.module("myApp",['ngSanitize']);
	app.controller("myCtrl",myFun);
	function myFun($scope){
		$scope.myHtml = "<div class='ht'>随意</div>"
	}
	app.directive('myNumber',function(){
		return {
                restrict:"C",
                templateUrl:'7.template.html'
            }
            //7.template.html 中内容为 <a href="www.baidu.com">百度</a>
            //即为将需要的内容引入
	});
	
**简单调用html**		
	
	<body ng-app="myApp" ng-controller="myCtrl">
		<ul>
			<li>{{scct}}</li>
			<li>{{ba}}</li>
		</ul>
	</body>
	<script type="text/javascript" src="../js/angular.min.js"></script>
	<script type = "text/javascript">
    var app = angular.module("myApp",[]);
	//  设置定时器 和 延时器
	    app.controller("myCtrl",function($scope,$interval,$timeout,myService){
	        $scope.scct=0;
	        $scope.txt = "李煜";
	        $interval(function(){
	           $scope.scct++;
	       },1000);
	        $timeout(function(){
	            $scope.scct+=1000;
	            $scope.ba = myService.addText($scope.txt);
	        },5000);
	    });
	    /*
	    * 创建自己的服务 也就是 js 方法
	    * service 参数一: 创建的服务名 参数二:服务的执行方法
	    * */
	    app.service("myService",function(){
	        this.addText = function(str) {
	            return "一行白鹭上青天"+str;
	        };
	    });
	</script>	
	
**jsonp完整 html 及 js**	

*js文件*
	
	var express=require("express");	
	var app = express();
	
	app.get("/jsonp",function(req,res){
		var query = req.query;
		var name = query.name;
		var age = query.age;
		var cb=query.cb;
		
		var obj={
			name:"名字："+name,
			age:"年龄："+age
		};
		var strJson = JSON.stringify(obj);
		res.send(cb+ '(' + strJson+ ')')
	});
	
	app.listen(8080);
	
*html文件*
	
	var app = angular.module("myApp",[]);	app.controller("myCtrl",function($scope,$http){
		$http.jsonp("/jsonp?name=tom&age=18&cb=JSON_CALLBACK").success(function(response){
			console.log(response);
		})
	})
	
**过滤器**
*文件自带*
	
>需要的内容加 竖杠 加过滤条件
	
	{{678|currency}}<br/>	
	
	举例：获取json中 内容
	<ul ng-app="myApp" ng-controller="myCtrl">
		<li ng-repeat="item in jsonData2|orderBy:'age'">{{item.name}}{{item.age}}</li>
	</ul>
	
	<script type="text/javascript" src="../js/angular.min.js"></script>
	<script type="text/javascript">
		var app=angular.module("myApp",[]);
		app.controller("myCtrl",function($scope){
			$scope.jsonData={
				name:"流域",
				age:80
			}
			$scope.jsonData2=[
				 {
                name:"刘秀",
                age:50
            },
            {
                name:"刘邦",
                age:30
            },
            {
                name:"始皇",
                age:35
            },
            {
                name:"可汗",
                age:45
            }
			];
		});
	</script>
	
<hr>

###完整创建交互页面
**引用 angular.js 等部分**		
	
	//创建后台数据
	var datas={
		{firstName:"王",lastName:"昭君"},
	    {firstName:"西",lastName:"施"},
	    {firstName:"貂",lastName:"蝉"},
	    {firstName:"杨",lastName:"玉环"}
	};
	//设置app module
	var app = angular.module("myApp",[]);
	//创建 controller
	app.controller("myCtrl",function($scope,$http){
		$scope.users = datas;//引用模拟数据
		$scope.disa = true;//设置全局disabled 默认为true
		var Index = 0 ;
		$scope.editBool = true;//设置编辑布尔值
		//设置默认方法
		function setReset(){
			$scope.disa = true;
			$scope.editBool = true;
			$scope.firstName = '';
			$scope.lastName = '';
			$scope.pass1 = '';
			$scope.pass2 = '';
		}
		setReset();
	//编辑方法
	$scope.editFun = function(index){
		Index = index;
		$scope.editBool = false;//重置editBool
		$scope.disa = false;
		$scope.firstName = $scope.users[index].firstName;
		$scope.firstName = $scope.users[index].lastName;
	};
	//创建用户
	$scope.createUser = function(){
		$scope.editBool = true;
		setReset();
	};
	//总体监听保存事件
	$scope.changeFun = function(){
		if($scope.editBool){
			$scope.disa = $scope.firstName!= ''&& $scope.lastName!= ''&& $scope.pass1!= ''&&$scope.pass2!= ''&&$scope.pass1==$scope.pass2?false:true;
		}else{
			$scope.disa = ($scope.firstName!= ''&&$scope.lastName!= ''?false:true);
		}
	};			
	//设置保存方法
	$scope.saveFun = function(){
		if($scope.editBool){
			var obj = {};
			obj.firstName = $scope.firstName;
			obj.lastName = $scope.lastName;
			$scope.users.push(obj);
			obj = null;
		}else{
			$scope.users[Index].firstName = $scope.firstName;
			$scope.users[Index].lastName = $scope.lastName;
		}
	};
	//删除
	$scope.delUser = function(index){
		$scope.users.splice(index,1);
		setReset();//重置
		Index= '';
	}	
	})
	
##react
**引入js**
	
	<script type="text/javascript" src="../js/react.js"> </script>
    <script type="text/javascript" src="../js/react-dom.js"> </script>
    <script type="text/javascript" src="../js/browser.min.js"> </script>
    
  **本身js 格式为：text/babel**

	<script type="text/babel"> 	</script>
**html**
	
	<div id="test"></div>	
	
>ReactDom.render 执行 react 的方法
>两个参数：参数一：执行的dom内容 参数二：操作的dom
	
	ReactDom.render(
		<div>{2+3}</div>,
		document.getElementById("test")
	)	
	
**array**
	
	var arr = [
            <h1>小荷才露尖尖角</h1>,
            <h1>早有蜻蜓立上头</h1>
    ];
    ReactDom.render(
    		<div>{arr}</div>,
    		document.getElementById("test")
    )
 
**map**

>循环 map 可用 设置了style 样式	

	var person = ["曹操","曹丕","曹植"]; 
	var setStyle = {
		fontSize:20,
		background:"blue",
		color:"red"
	}; 	
	ReactDOM.render(
		<ul style={setStyle}>{person.map(
			function(name,key){
				return <li key={key}>{name}</li>})
				}</ul>,
	   document.getElementById("test")
	  );
 	
 **组件**
 
>组件：首字母必须大写，创建组件：createClass
>
>获取子节点的数量，没有子节点的返回 underfined 
>
>一个返回object 多个返回 array
>
>React.Children 专门处理 this.props.children

	var MyHtml = React.createClass({
		render:function(){
			return <ul>
				{React.Children.map(this.props.children,function(child){
					return <li>{child}</li>
				})}</ul>
		}
	})
	
	ReactDOM.render(
		<MyHtml>
			<span className="txt">少小离家老大回</span><span>字体么有添加class属性</span>
		</MyHtml>
	);
	
	
**组件调用组件**

	var MyHtml = React.createClass({
		render:function(){
			return <ClassHtml />
		}
	});
	var ClassHtml = React.createClass({
		render:function(){
			return <div className = "txt">往往如实</div>
		}
	})；
	ReactDOM.render(
		<MyHtml />,
		document.getElementById("test")
	)
	
 	
 **ref**
 
        	MyHtml = React.createClass({
        	propTypes:{ 
            /*
            * 验证必须为字符串
            * 相当于文档规范
            */
            classl:React.PropTypes.string.isRequired
        },
        getDefaultProps:function(){
            return{
                classl:"谁能书阁下"
            }
        },
        handleClick: function () {
            this.refs.myUl.style.background="#f00"
        },
        render:function(){
            var classl = this.props.classl;
            var _this = this;
            return <ul ref="myUl">{
                React.Children.map(this.props.children,function(child){
                return <li onClick={_this.handleClick}>{classl}{child}</li>
            })
            /*
            * ref 设置了一个 dom上 this.refs.name.refname 就获得了这个dom 就可以对该dom 操作
            * */
        }</ul>
        }
    });
	   /* var ClassHtml = React.createClass({
	        render:function(){
	            return <div className="txt">往往鬼哭,天阴侧闻</div>
	        }
	    });*/
	    var str = "绕树三匝,何枝可依";
	    /*
	    * 给属性赋值,如果直接写在组件里面,就用引号设定数据
	    * 如果是外部传入数据,就是用{} 包含变量即可
	    * */
	    ReactDOM.render(
	    <MyHtml classl={str}>
	                    <span>###曹操</span><span>###曹丕</span><span>###曹植</span>
	    </MyHtml>,
	            document.getElementById("test")
	    );	
 	
 **点击切换**
 	
	     /*
	    * 状态:state 状态
	    * 默认状态: getInitialState
	    * 改变状态: setState
	    * */
    var BtnHtml = React.createClass({
        getInitialState: function () {
            return {liked:false}
        },
        handleClick: function () {
          this.setState({liked:!this.state.liked});
        },
        render:function(){
            var txt = this.state.liked?"喜欢":"不喜欢";
           return <div><p  >你{txt}她,点击切换 </p><input onClick={this.handleClick} type="button" value="点击"/></div>
        }
    });
    ReactDOM.render(
        <BtnHtml />,
            document.getElementById("test")
    );	
 
**组件输入**
    
    	 /*
     * 状态:state 状态
     * 默认状态: getInitialState
     * 改变状态: setState
     * */
    var BtnHtml = React.createClass({
        getInitialState:function(){
            return {value:"输入"}
        },
        handleChange:function(event){
            this.setState({value:event.target.value});
        },

        render:function(){
            var value = this.state.value;
            return <div>
                        <input type="text" onChange={this.handleChange} value={value}/>
                        <p>{value}</p>
                    </div>
        }
    })


    ReactDOM.render(
    <BtnHtml />,
            document.getElementById("test")
    )
 
**生命周期**

		    var Input = React.createClass({
        getInitialState: function () {
            return {opacity:1,k:0.15}
        },
        componentWillMount: function () {
            console.log('即将被装载');
            this.timer = setInterval(function () {
                var opacity = this.state.opacity;
                opacity-=this.state.k;
                if(opacity<0||opacity>1){
                    this.state.k=-this.state.k;
                }
                console.log(opacity);
                this.setState({opacity:opacity});
            }.bind(this),300);
        },
        componentDidMount: function () {
            console.log('初始化被装载')
        },
        render: function () {
            return (
                    <div style={{opacity:this.state.opacity}} className="opacity">
            </div>
            )
        }
    });
    ReactDOM.render(

        <Input />,
            document.getElementById("test")
    );
    /*
    * 组件的生命周期
    *
    *
    * 1.初始化
    * getDefaultProps:设置默认属性
    * getInitialState :设置初始化状态
    * componentWillMount: 组件即将被装载
    * render: 渲染
    * componentDidMount:组件已经被装载,只会在第一个组件装载
    *
    *
    * 2.运行中
    *componentWillReceiveProps : 接收属性前调用
    *shouldComponentUpdate : 在接收一个新的 prop 或者 state 前调用
    *componentWillUpdate : render 触发之前 更新
    * render: 渲染
    * componentDidMount:渲染完成后触发
    *
    *
    * 3.销毁
    * componentWillUnmount:组件从 dom 中移出时候立即销毁
    *
    * */ 	
	