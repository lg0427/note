###函数

>php 不支持函数的重载
>
>定义：调用的时候可以根据函数传入的类型匹配不同的函数
>
>内置函数有1000多个
>
>自定义函数有 ：
	
	无参无返回值
	有参无返回值
	无参有返回值
	有参有返回值

举例：	

	function sayHello (){
		echo "hello";
	}	
		sayHello(); //调用函数
		
	形参或实参的使用	
	function minValue($num1 = 10,$num2 =20){
		return $num1<$num2? $num1:$num2;
	}		
		$minV = minValue();//两个参数都使用
		$minV = minValue(80);//参数1值==80
		$minV = minValue();//不使用默认值
		
###自身函数调用	
	
	function outFn(){
		function inFn(){
			echo "我是一个内部函数";
		}
		inFn();//调用内部
	}	
	outFn();//调用外部函数
	
	<!--函数自身调用-->
	(function(){
		echo "自身调用";
	})();	
		
	$fn = function(){
		echo "函数指针调用";
	}	
	$fn();	
		
	function fn3($fnPara){
		$fnPara();
	}	
	
	<!--函数指针-->	
	$fn4 = function(){
		echo "我是通过回调调用"；
	}	
	fn($fn4);	
		
	fn3(function(){
		echo "我是通过回调调用！22222";
	});	
		
###算法
	
*递归*
	
	//递归 n * (n -1)..*3 * 2 *1
	function mul($num){
		if($num == 0){
			return 1;
		}
		return $num * mul($num - 1);
	}
	echo mul(3)."<hr>";		
		
*传地址*

	$a = 100;
	function changeA($num){
		$num = 200;
		echo "函数内A：{$num}<hr>"; 
	}
	
	changeA($a);//是两个变量，作用域问题（复制了一份实参）
	echo "函数外A：{$a}<hr>";		
	
###地址传入& ： 地址符号
		
>&$num 接受的是变量的地址（引用类型），函数调用传入的实参是实参的地址，
>php默认是自动识别形参地址符(传入的时候不能取地址传入)

	function changB （&$num）{
		$num = 200;
		echo “内部B的值：{$num}<hr>”;
	}		
	changeB($b);		
	echo "外部B的值：{$b}<hr>";		
		
	//写个函数交互两个值
	$val1 = 100;
	$val2 = 200;	
	function changeValue(&$num1, &$num2){
		$temp = $num1;
		$num1 = $num2;
		$num2 = $temp;
	}
	changeValue($val1,$val2);
	echo "val1 = {$val1} --- val2={$val2}";	
		
###变量域
	
>与js 不同：函数内部使用全局变量，报错： Undefined variable
>解决办法：

	1、使用global 声明
	2、$GLOBALS 数组（系统定义好的超全局变量）自己定义的全局变量在里面存储			
	$a = 100;
	$b = 200;		
	
	function test(){
		global $a;
		$a = 300;
		echo $GLOBALS['a'];
	}	
	test();
	echo "<hr>";	
	echo $a."<hr>";
	
###栈区
	
>栈区 ---> 堆区
>//$x 局部变量：（变量保存在栈区：特点：出了函数作用域，栈区变量被销毁，内存释放）
 	
	function staticFn(){
		static $x =100;
		echo ++$x."<br>";
	}		
	for($i = 0; $i < 5; $i++){
		staticFn();
	}
	
*进栈：添加到后面*

	array_push($numbers,5,6,7);
	
*出栈：从后面删除，每次删除一个*
	
	array_pop($numbers);
	
*从前面添加*
	
	array_unshift($numbers,100,200);			
*从前面删除*

	array_shift($numbers);	
	
**数组的排序** 

*value 值的排序*

>1、sort //升序
	
	sort(数组名);
	
>2、rsort //降序	
	
	rsort(数组)	
	
>asort() 根据关联数组的值，对数组进行升序(保证索引不变);
	
*key 值的排序*

>1、ksort 升序
>
>2、krsort 降序	
		
###索引及数组操作
	
>查看类型	*echo gettype($days);*
>	
>查看长度  echo count()
>
>遍历数组
	
	//遍历数组
	for ($i=0; $i < count($days); $i++) { 
		echo $days[$i]."<hr>";
	}
	//赋值 如果已经存在则修改，没有就添加
	$days[0] = 'new星期';//修改
	$days[3] = '星期四';//添加
	$days[] = '星期五';//默认添加到数组最后面
	
	
	
>使用函数*range()*创建指定范围的数组

	//range($start, $limit, $step)
	//参数1：开始
	//参数2；结束
	//参数3：间隔步数  默认1
	
	echo "<hr>";
	//	$ages = range(15, 20);
	$ages = range(15, 20, 2);
	print_r($ages);
	echo "<hr>";
	
	$letters = range('a', 'd');
	print_r($letters);			
		
		
>释放数组元素 *unset()*理解为带下标一起删除
	
	$numbers = array(1,2,3,4);		
	unset($numbers[0]);
	prinr_r($numbers);//输出	Array ( [1] => 2 [2] => 3 [3] => 4 )
		
>检查数组是否包含某值 *in_array($needle,$haystack,$strict)*
	
	参数1：待查询
	参数2：数组
	参数3：可选布尔值，true为严格类型
	
	$ifIn = in_array('4',$numbers);
	

###截取函数 array_slice 实现截取、替换、删除等

>截取 *array_slice($array, $offset, $length, $preserve_keys)*

	$numbers = array(1,2,3,4,5);
	//( [0] => 3 [1] => 4 [2] => 5 )
	
	//参数3省略，默认截到末尾
	$subArr =  array_slice($numbers, 2);
	
	//从0下标，截取3个
	$subArr =  array_slice($numbers, 0,3);
	
	//负数：从后面-1开始
	$subArr =  array_slice($numbers, -4,3);
	
	//	参数4：bool值，默认false  传入true，可以返回原来的下标
	$subArr =  array_slice($numbers, 1,3,TRUE);


	//array_splice($null, $offset, $length, $replacement)
	//修改的是原数组
	
	$numbers = array(1,2,3,4);
	//删除前两个值（参数2：删除的个数）
	$result = array_splice($numbers,0,2);
	echo "<hr>";
	//返回值（删除元素组成的数组）
	
	print_r($result);
	echo "<hr>";
	print_r($numbers);
	//前面添加一个
	array_splice($numbers,0,0,100);
	echo "<hr>";
	print_r($numbers);	
	//从后面添加元素 == push
	array_splice($numbers,count($numbers),0,200);
	echo "<hr>";
	print_r($numbers);


>array_keys($input,$search_value,$strict)
>
>获取关联数组中的key 值

	$color = array('red','blue','green','red');
	$keys = array_keys($color);
	//参数2：选出数组对应值的key（键）值
	$keys = array_keys($color,'red');
	echo '<hr>';
	print_r($keys);
	
	//获取数组中所有value
	$values =  array_values($color);
	echo "<hr>";
	print_r($values);
	
	//查询数组中 'red' 对应的键（多个值默认返回第一个键）
	$key = array_search('red', $color);
	echo "<hr>".$key."<hr>";

###二维数组
	
**比较使用 foreach 和 for 循环**
	
	$info = array(
		array('张三','男',10),
		array('李四','男',10),
		array('王六','男',10)
	);

	for($i = 0; $i < count($info); $i++){
		$personInfo = $info[$i];
		for($j = 0; $j < count($personInfo); $j++){
			echo $personInfo[$j].'-';
		}
		echo "<hr>";
	}
	
	foreach ($info as $key => $personInfo) {
		echo "<hr>";
		foreach($personInfo as $value){
			echo $value.'-';
		}
	}
	
###字符串转成数组 explode
	
>explode($delimiter,$string,$limit)

	参数1： 分割
	参数2：要处理的字符串
	参数3：限制数组中最多包含几个元素
	
 	$str = '1,2,3,4,5';		
	$arr = explode(',',$str);
	$arr = explode(',',$str,3);//[0] => 1 [1] => 2 [2] => 3,4,5 )
	print_r($arr);
	
	
###数组转字符串 implode
	
	$arr2 = array(1,2,3,4);
	$newStr = implode('-',$arr2);//1-2-3-4
	echo '<hr>'.$newStr;


###字符串中元素的查找

	$str = 'hello world';
	//strpos($haystack,$needle,$offset),从下标 0 开始查找，默认最近一个
	
	$pos = strpos($str,'o');
	$pos = strpos($str,'o',5);//参数3：偏移到指定下标开始寻找
	
	echo $pos."<hr>";
	
###替换	

>str_replace($search,$replace,$subject,$null)
	
	参数1：指定查找的值
	参数2：替换的值
	参数3：操作的字符串
	参数4：可选，计数器（替换的字符数量计数）	


	举例：
		$str = '随便一个字符串';
		$newStr = str_replace('一个'，'二二'，$str);//随便二二字符串
		echo $newStr;
		
		//参数4：
		$str = 'hello world';
		$newS = str_replace('o','M',$str,$count);//hellM wMrld
		echo "<hr>".$newS."<hr>";
		echo $count //传入地址	
		
###字符串截取

>substr($string,$start,$length)

	//默认返回后面部分
		
	$str = 'hello world';
	$sub = substr($str,3);//从下标3处开始截取
	
	$sub = substr($str,3,4);  //从下标3处截取，截取长度为4，中间有空格也计算		
	
	参数3： bool 类型，默认false 返回后面一半， true 返回前面	
	$val = strstr('hello-world', 'or',TRUE);//hello-w	
	
##其他函数

*获取字符粗长度*

	echo strlen('hello');

*转换小写*
	
	echo strtolower("LANOU");

*转换大小*

	echo strtoupper('lanou');

*翻转字符串*

	echo strrev('lanou');	
		
###删除标签

>strip_tags($str, $allowable_tags)	
	
	echo strip_tags($str,'<a><h2>');//参数2：允许存在的标签
	
	
*HTML实体*

	$str = '<p>段落</p>';
	echo $str;
	echo htmlspecialchars($str);	
	
