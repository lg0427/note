###DOM-jQ 操作

####获取节点中的父节点和兄弟元素节点

>**parent()获取父节点**

>**next()获取下一个兄弟元素节点**

####创建添加节点

**创建元素（元素节点），添加节点**
		
	var p = '<p>菲菲</p>'

>**在A元素的内部前面添加B元素**
	
	$(A).prepend(B) 
	
>**将A元素添加到B元素内部的的前面**
	
	$(A)prependTo(B) 
	
>**往A元素内部的尾部添加B元素**
	
	$(A).append(B)  
	
>**将A元素添加到B元素内部的尾部(最后)**
	
	$(A).appendTo(B) 
	
>**在A元素的外面的后面添加B元素**
	
	$(A).after(B) 
	
>**将A元素添加到B元素外部的后面**
	
	$(A).insertAfter(B) 
	
>**将A元素添加到B元素外部的前面**
	
	$(A).insertBefore(B) 
	
>**在A元素外部的前面添加B元素**
	
	$(A).before(B)  
	
####删除节点
	
**eq()默认删除第一个元素**	

**根据下标删除元素**
	
	$('p:eq(2)').remove();

**删除符合p类型标签的第一个元素**
	
	//$('p:first-of-type').remove();
	
	//$('p:nth-of-type(0)').remove();
	
	//$('a:eq(1)').remove();

**用detach（）也是完成删除**
	
	$('a:eq(0)').detach();

**全部删除**
	
	$(A).empty() 将A节点下的所有子节点全部删除

***

###jQ-css样式

**对数值的获取**
	
	parseInt()解析整数
	parseFloat()解析浮点数  （解析小数)
	
**css(样式,样式值/函数)**

	1、直接设置		$('.oneDiv').css('color','red');
	
	2、设置多个样式 
		
		$('.oneDiv').css({
			width:'300',
			height:'300',
			backgroundColor:'green'
		});
	

**获取样式值**

	$('.oneDiv').css('color')

**获取对象的下标**
	
	$(this).index()  获取执行该事件的下标

####jQ实现的大图滚动

			//点击按钮的触发事件
		$('input').click(function  () {
			//自定义动画
        $('#content').animate({
        
	//   $(this).index()  获取执行该事件对象的下标
	
        	left:-$('#wrap').width() * $(this).index()
        },200);
		});
