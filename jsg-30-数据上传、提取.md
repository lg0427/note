###文件上传

####文件上传 html
	
	<form action="phpreset.php" method="post">
			<p>用户名：<input type="text" name="username" id="username" value="" /></p>
			<p>密码：<input type="password" name="password" id="password" value="" /></p>
			<p>确认密码：<input type="password" name="password2" id="password2" value="" /></p>
			<input type="submit" value="注册"/>
		</form>
		
####上传php文件

**获取上传内容**
	
	$username = $_POST['username'];
	$password = $_POST['password'];
	$password2 = $_POST['password2'];
	//打印看是否获取
	//var_dump($username,$password,$password2);
	
	//判断输入是否合法
	 if($username == ""){
	 	exit('名字不能为空');
	 }
	 if($password != $password2){
	 	exit('两次输入不一致');
	 }
	
**入库操作**
	
*1、建立连接*

	$con = mysql_connect('localhost','root','');	//选择数据库 $connection = mysql_select_db("setuse",$con);
	//设置编码格式
	mysql_query("set names utf8");
	
*2、上传文件内容*
		
	if($con){
		$password = md5($password);//用密文加密密码
		$connection = mysql_select_db("setuse",$con);
		$sql = "insert into `setuser` (`Username`,`password`) values ('$username','$password')";
		
		$result = mysql_query($sql);
		if($result){
			echo $username."注册成功";
		}else{
			die("注册失败");
		}
	}
		
###获取后台数据
	
####获取后台 html 部分
	
	<form action="phpreset2.php" method="post">
		<p>用户名：<input type="text" name="username" id="username" value="" /></p>
		<p>密码：<input type="password" name="password" id="password" value="" /></p>
		<input type="submit" value="登录"/>
	</form>	
	
####php部分
	
*获取上传内容比较用*
	
	$username = $_POST['username'];
	$password = $_POST['password'];
	if($username == ""){
			die('用户名不能为空');
		}
	if($password == ""){
			die('密码不能为空');
		}			
		
*建立连接*

	$con = mysql_connect("localhost","root","");
	
	mysql_query("set names utf8");
	
	if($con){
		$password = md5($password);//密文加密
		$connection = mysql_select_db("setuse",$con);
		$sql = "SELECT * FROM `setuser` WHERE `Username` = '$username' AND `password` = '$password'";
		$result = mysql_query($sql);
		
		if($row){
			echo row["Username"].'登陆成功';
		}else{
			echo "用户名和密码不一致";
		}
	}else{
		die(‘登录失败’);
		}
	}
		
	

			