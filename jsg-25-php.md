###mac 本地环境搭建

>1、在没有安装xampp 情况下用mac 自带的
>	
>2、本地mac 开启环境： 开启终端，输入 sudo apachectl start
>
>3、回车，在网页中输入 localhost或者127.0.0.1或者当前链接的网络地址  显示 it works 即为正常
>
>4、打开 Finder ，左上角点击前往，点击前往文件夹，输入 /private/etc/apache2/httpd.conf
>
>5、编辑一个 php 文件，将文件复制到 硬盘下 - 资源库- WebServer - Document - 拷贝
>
>6、在浏览器下将文件名拷贝进去，回车
>

###Apache环境搭建
	
>1、安装xampp	到本地
>
>2、在终端中输入	sudo apachectl stop 停止本地服务器
>
>3、启动	xampp 程序，



###php基础
	
>1.可以放置于文档中的任何位置，PHP 脚本以 <?php 开头，以 ?> 结尾；
>
>2、PHP 语句以分号结尾（;）。PHP 代码块的关闭标签也会自动表明分号（因此在 PHP 代码块的最后一行不必使用分号）
>

###php标记
	
	1.<?php echo “hello php”; ?>	
	2. <script language=“php”>echo “hello php”</script>
	3. <? echo “hello php”; ?>     //短标记
	4. <% echo “hello php”; %>  //asp风格
	
	1.2 可以直接使用，3.4 需要修改php.ini 的 配置文件才能使用
	
###输出


**输出方法**

>echo 和 print
>
>echo 能够输出一个以上的字符串
>
>print 只能输出一个字符串，并始终返回 1
>
>echo 比 print 稍快，因为它不返回任何值

	1.echo 输出一个或多个字符串
	2.print 输出一个字符串
	3.printf 输出格式化字符串
	4.print_r 输出变量的内容，可以输出数组的信息
	5.var_dump 输出变量详细的信息(可以是多个变量),用于调试	


*展示如何用echo命令来显示字符串和变量*

	<?php
	$txt1="Learn PHP";
	$txt2="W3School.com.cn";
	$cars=array("Volvo","BMW","SAAB");
	
	echo $txt1;
	echo "<br>";
	echo "Study PHP at $txt2";
	echo "My car is a {$cars[0]}";
	?>

*展示print 来显示字符串和变量*

	<?php
	$txt1="Learn PHP";
	$txt2="W3School.com.cn";
	$cars=array("Volvo","BMW","SAAB");
	
	print $txt1;
	print "<br>";
	print "Study PHP at $txt2";
	print "My car is a {$cars[0]}";
	?>


###常量和变量

**常量 define() 函数**

>常量类似变量，但是常量一旦定义就无法更改或撤销定义
>
>常量是单个值的标识符（名称），在脚本中无法改变该值
>
>有效的常量名以字符或下划线开头，对大小写敏感，通常常量总是大写
>
>与变量不同，常量贯穿整个脚本是 自动全局的
	
*设置常量*
	
	三个参数：
		1、首个参数定义常量的名称
		2、第二个参数定义常量的值
		3、可选的第三个参数规定是否对大小写敏感，默认是false
		
		示例：对大小写敏感的常量
		
		<?php
			define("GREETING", "Welcome to W3School.com.cn!");
			echo GREETING;
		?>
		
		示例： 对大小写不敏感的常量
			
		<?php
		define("GREETING", "Welcome to W3School.com.cn!", true);
		echo greeting;
		?>	

**php变量规则**

>变量以$符号开头，其后是变量的名称
>
>变量名称必须以字母或下划线开头
>
>变量名称不能以数字开头
>
>变量只能包含字母、数字和下划线（A-z、0-9 以及 _）
>
>变量名称对大小写敏感

	例如：
	 $age = 28;
	 $color = “red”;
	 $sum = 15+”12”;   //$sum = 27;

**变量的赋值**
	
>1、直接赋值
>
>2、引用赋值
	
	$var_2 = &$var_1; //把变量var_1 的内存地址赋值给 var_2 ,即引用赋值	

**变量的作用域**
	
>local 局部 
>
>global 全局
>
>static 静态	
>
>函数之外的声明变量拥有global 作用域，只能在函数以外进行访问
>
>函数内部声明变量用于local 作用域，只能在函数内部进行访问
	
	<?php
	$x=5; // 全局作用域
	
	function myTest() {
	  $y=10; // 局部作用域
	  echo "<p>测试函数内部的变量：</p>";
	  echo "变量 x 是：$x";
	  echo "<br>";
	  echo "变量 y 是：$x";
	} 
	
	myTest();
	
	echo "<p>测试函数之外的变量：</p>";
	echo "变量 x 是：$x";
	echo "<br>";
	echo "变量 y 是：$x";
	?>

*解决局部引用全局变量问题*

>php 同时在名为  $GLOBALS[index] 的数组中存储了所有的全局变量，下标存有变量名。
>
>这个数组在函数中也可以访问，并能够用于直接更新的全局变量。
	
	<?php
	$x=5;
	$y=10;
	
	function myTest() {
	  $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y'];
	} 
	
	myTest();
	echo $y; // 输出 15
	?>
	
*php关键词 static*

	函数完成/执行后，会删除所有变量，不过需要不删除某个局部变量时，需要在首次声明变量时使用static 关键词
	
	<?php

	function myTest() {
	  static $x=0;
	  echo $x;
	  $x++;
	}
	
	myTest();
	myTest();
	myTest();
	
	?>
	
	运行结果：  0
				1
				2
				3
				4
				
	每当函数调用时，变量所存储的信息都是函数最后被调用时的信息
	
	注释：该变量仍然是函数的局部变量				
**魔术常量**

>__LINE__	文件中的当前行号;
>
>__FILE__	文件的完整路径和文件名;
>
>__FUNCTION__	函数名称;
>
>__CLASS__	类的名称;
>
>__METHOD__	类的方法名;	
	
						
###注释和大小写

**注释方式**

>1、单行注释

	//这是单行注释
	
	# 这也是单行注释

>2、多行注释

	/*
		多行注释块
		可以跨行
	*/

**大小写**

>1、在php中，所有的变量对大小写敏感
>	
>2、所有用户定义的函数、类、关键词 都对大小写不敏感

###数据类型

>PHP var_dump() 会返回变量的数据类型和值

**字符串**
	
	字符串可以是引号内的任何文本，单引号或双引号都可以使用
	单引号字符串中出现的变量会被变量的值替代
	双引号字符串中最重要的一点是其中的变量不会被变量值替代
	
	如果遇到美元符号 $ ,解析器会尽可能多的取后面的字符以组成一个合法的变量名
	如果想明确指定名字的结束，用花括号把变量名括起来
	
	字符串转义
		\n 换行
		\r 回车
		\t 水平制表符
		\\ \反斜杠
		\$ 美元符
		\“” 双引号
		

**整数**
	
	不能包含逗号或空格，不能有小数点
	$age = 25;
	
**浮点数**
	
	是有小数或指数形式的数字
	$num = 5.39;	

**逻辑 布尔值**
	
	false 返回值不显示，true 显示为 1
	$bo = TRUE;
	$bo = FALSE;
	
**数组**

	数组可以存储多个值，用逗号分开
	$week = array(‘星期一','星期二','星期三');
		
**对象**
	
	必须明确声明对象，首先必须声明对象的类，使用class 关键词
	$db = new db();

**null**

	特殊的null值表示 变量无值，标志变量为空，也用于区分 字符串和空值数据库
	可以通过把值设置为null 将变量清空 使用函数 unset() 清除
	
	<?php
	$x="Hello world!";
	$x=null;
	var_dump($x);
	?>

###类型相关函数
	
>gettype() 返回变量的类型
	
	$str = ‘hello’;
		 echo gettype($str)
		 
>is_type() 查看变量是否属于某个类型，是返回 TRUE ，否 返回 FALSE
	
	$arr = array(1);
	 echo is_array($arr);
		
	 $num = 5;
	 echo is_int($num);	
	 
>	 	 


###字符串函数
	
**strlen()函数**

	strlen（）函数返回字符串的长度，以字符计
	常用于循环和其他函数，在确定字符串何时结束很重要
	
**strpos()函数**	

	用于检索字符串内指定的字符或文本，如果找到匹配则返回首个匹配的字符位置，如果未找到，返回false


###运算符及字符串

|运算符|名称|例子|结果|	
|:--|:--|:--|:--|
|.|串联|$txt1 = "Hello" $txt2 = $txt1 . " world!"|	现在 $txt2 包含 "Hello world!"|
|.=|串接赋值|	$txt1 = "Hello" $txt1 .= " world!"	| 现在 $txt1 包含 "Hello world!"


	下例展示了使用字符串运算符的结果
	
	<?php
	$a = "Hello";
	$b = $a . " world!";
	echo $b; // 输出 Hello world!
	
	$x="Hello";
	$x .= " world!";
	echo $x; // 输出 Hello world!
	?>

运算符参考 js 运算符

###逻辑运算符

php 赋值运算 从右到左

**比较运算符**

|运算符|名称|例子|结果|	
|:--|:--|:--|:--|
|and|与|$x and $y	|如果 $x 和 $y 都为 true，则返回 true。
|or	|或	|$x or $y	|如果 $x 和 $y 至少有一个为 true，则返回 true。
|xor|异或|$x xor $y	|如果 $x 和 $y 有且仅有一个为 true，则返回 true。
|&&	|与	|$x && $y	|如果 $x 和 $y 都为 true，则返回 true。
|\|\|	|或	|$x \|\| $y	|如果 $x 和 $y 至少有一个为 true，则返回 true。
|!	|非	|!$x	|如果 $x 不为 true，则返回 true。

**数组运算符**

|运算符|名称|例子|结果|	
|:--|:--|:--|:--|
|+	|联合	|$x + $y	|$x 和 $y 的联合（但不覆盖重复的键）
|==	|相等	|$x == $y	|如果 $x 和 $y 拥有相同的键/值对，则返回 true。
|===	|全等	|$x === $y	|如果 $x 和 $y 拥有相同的键/值对，且顺序相同类型相同，则返回 |true。
|!=	|不相等	|$x != $y	|如果 $x 不等于 $y，则返回 true。
|<>	|不相等	|$x <> $y	|如果 $x 不等于 $y，则返回 true。
|!==	|不全等	|$x !== $y	|如果 $x 与 $y 完全不同，则返回 true。


**比较运算符**

>返回一个布尔值TRUE 或 FALSE

	>	大于
	<	小于
	>=	大于或等于
	<=	小于或等于
	!=	不等于
	<>	不等于
	==	等于
	===	全等于  （两个比较的内容里，类型也要一样）
	!== 	全不等


			