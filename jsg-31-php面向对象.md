###定义一个类

	class Person{
	//定义属性和方法时要有访问修饰符，属性和属性之间使用分号分开
		public $name = "神人";
		public $age;
		public $sex;
	}
	//实例化具体的对象
	$p1 = new Person();
	//访问对象的属性和方法用 -> .属性名前加 $
	
	$p1 -> name = "仙人"."<hr>";
	echo $p1 -> name;
	
	
###访问修饰符

	1、public  protected  private
	2、public 类的内部 外部 子类中都可以访问
	3、protected 只能在类内部或者子类内部访问
	4、private 只能在自己类内部访问	
	
###调用方法和封装

	//  php中定义一个类 
		class Person{
	//	定义属性和方法时要有访问修饰符,属性与属性之间使用分号隔开
			public $name = "万象";
			public $age;
			public $sex;
	//	设置方法,方法前也要加访问修饰符
			public function sayName(){
	//	在类的内部访问属性
				echo $this->name;
			}
	//	封装 
			function setAge($ages){
				if($ages<0 || $ages>130){
					echo "您设置的年龄有误,请重新输入";
				}else{
					$this->age = $ages;
				}
			}
		}	
	//实例化出具体的对象
	$p1 = new Person();
	$p1 -> sayName();//调用方法
	$p1->setAge(1000);//封装
	

###函数类的继承

			class Person{
			public $name = "万象";
			public $age;
			public $sex;
			protected $length = 110;
		// private $height = 175;
		//	final 禁止子类重写父类中的方法
			final public function test1(){
				//echo "方法一";
			}
		}	
	
	
	//		继承 extends
		class Students extends Person{
			public function test2(){
					echo $this->height;
					//echo "方法二";
				}
			} 
	//		实例化出具体的对象
			$s1 = new Students();
			$s1->test2();
				
###内部类的调用 :: 范围解析符

	class Person{
	//	定义属性和方法时要有访问修饰符,属性与属性之间使用分号隔开
	public $name = "万象";
	public $age;
	public $sex;
	
	//在类的内部定义常量 使用const
	//在类的内部定义的常量,只有这个类才有
	const AAA = "二毛";
	public function sayA(){
	//内部访问常量的方法
		echo $this::AAA."<hr>";
		echo self::AAA."<hr>";
	}
	}	
	//echo AAA;//类内部定义的常量不能直接访问
	
	//实例化出具体的对象
		$p1 = new Person();
		
	//在类外部访问类里面的常量的方法
	//一:用类名来访问常量,这里的::叫做范围解析符
			echo Person::AAA."<hr>";
	//二:用一个代表类名的字符串访问
			$str = "Person";
			echo $str::AAA."<hr>";
	//三:使用对象访问
			echo $p1::AAA."<hr>";
			$p1->sayA();
			
###静态变量
	
	//静态变量的定义： static 
	//静态变量不属于任何一个对象，是属于这个类，是一个公共的变量
	
	class Person{
		public $name = "万象";
		public $age;
		public $sex;
		//静态方法
		static public $aa = "hhh";
		static public function staticM(){
		//静态方法中不能使用$this
			echo "这是一个静态方法";
		}
	}
		//实例化出具体的对象
	$p1 = new Person();
	  $p1::staticM();
	
	
	访问静态变量
		
		echo $p1::$aa;
		
	//赋新值	
		
		$p1 = new Person();
		echo $p1::$aa = "xinzhi";
	
###构造函数
	
			class Person{
			public $name = "万象";
			public $age;
			public $sex;
			
		//	创建一个构造函数,构造函数没有返回值
		//	一个类里面有了构造函数之后,就可以进行传参
			public function __construct($nm,$ag,$sx){
				$this->name = $nm;
				$this->age = $ag;
				$this->sex = $sx;
				
		//	echo "这是一个构造函数,创建对象的时候会自动调用";
			}
		} 
		//	实例化出具体的对象
		$p1 = new Person("晓晨",30,"不明");
		echo $p1->name."<hr>";
		echo $p1->age."<hr>";
		echo $p1->sex."<hr>";	
	

	
	
	
	
	
	
	
	
	
	
		
<!---->		