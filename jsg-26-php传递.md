###传递
	
**$_GET**

>包含使用get 方法传递的参数的有关信息


	url: http://localhost/test.php?id=100&page=2;
	$id = $_GET['id'];
	$page = $_GET[‘page’];


**$_POST**

>$_POST  该变量包含使用 POST 方法传递的参数的有关信息
	
	html:
	<form name="reg" action="test.php" method="post">
		用户名：<input type="text" name="username" />
		密码: <input type="password” name="passwd"/>
		<input type="submit" value="提交" />
	</form>
	
	php:	
	$username = $_POST[‘username’];
	$passwd = $_POST[‘passwd’];
	
>$_REQUEST   该变量记录着通过各种输入方法传递给脚本的变量,缺点：不安全并且慢	
> $_COOKIE            cookie变量数组

###foreach循环

>foreach 循环用来遍历数组，每次遍历都将指针后移一位

语法格式1、
	
	foreach(array as $value){
		//statements
	}
	
语法格式2、
	
	foreach(array as $key=>$value){
		//statements
	}
	
###连接数据库
	
>第一步:连接数据库,使用mysql_connect(参数1,参数2,参数3)函数 
	
	$con = mysql_connect("localhost","root","");
	
* 参数一: 数据库的地址  localhost或127.0.0.1
* 参数二: 服务器的用户名 root
* 参数三: 服务器的用户密码 默认是""	
	
>第二步:选择要操作的数据库

	mysql_select_db("students",$con);
	mysql_query("set names utf8");//设置插入数据库的编码格式
	
* 使用mysql_select_db(参数1,参数2);
* 参数1:要操作的数据库的名字
* 参数2:数据库存放的地址 

###与后台建立连接

>第三步:具体的数据库操作

* $sql = "insert into h3student(student_name,student_sex,student_age) values('隔老','男','35')";

>最后一步:关闭数据库
	
	mysql_close($con);

**建立连接**
	
	$con = mysql_connect("localhost","root","");
	
**选择数据库**

	mysql_select_db("students",$con);
	
**设置编码格式**
	
	mysql_query("set names utf8");
	
**创建sql语句、执行sql语句**
	
	$sql = "select * from biandanming";
	$result = mysql_query($sql);
	
	
*关联数组形式返回数据*	
	
	mysql_fetch_array 以关联数组形式返回数据			
*普通数组形式返回*
	
	mysql_fetch_row 以普通数组的形式返回数据
	
**关闭数据库**
	
	mysql_close($con);	

