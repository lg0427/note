**零碎知识点**
defer="defer"让脚本在浏览器遇到</html>后才执行
trigger
delegate()方法：为指定的元素添加一个或多个事件处理程序，并规定当这个事件发生时运行的函数

**热点链接**
*在需要图形的上面进行操作*

 	<img src = '图形文件名' usemap='#图的名称'>
	<map name = '图的名称'>
		<area shape="形状" coords="区域坐标列表" href="url">
		<area shape="形状" coords="区域坐标列表" href="url">
	</map>
	
	用矩形
		四个数字：前两个为左上角坐标 后两个数字为右下角坐标
		<area shape="rect" coords="100,30,300,40" href="url">
	用圆形
		使用三个数字：前两个数字为圆心的坐标，最有一个为半径长度
		<area shape="circle" coords="85,133,30" href="url">
	用任意图形：将图形每一个转折点坐标依次输入
		<area shape="poly" coords="233,70,285,70,300,90,200,78" href="url"> 	
	