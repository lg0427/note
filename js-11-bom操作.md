###1、Bom 的基础

**1、HTML文件**

>1、html -- 网页结构

>2、css -- 设置样式

>3、js -- 处理用户交互


	DOM：Document Object Model 的缩写（文档对象模型）
	作用：在js 中，通过Dom 操作的方式去访问和造作 HTML 中的标签以及设置元素的样式
	方式：通过节点的方式去获取符合条件的标签对象
	节点的分类：
	1、元素节点（重点） -- <div><p>
	2、注释节点 -- <！-- p标签的使用-->
	3、文本节点 -- 文本部分
	4、文档节点 -- document
	5、声明节点 -- doctype
	
	
**2、获取标签对象**

>1.获取 nodeName 节点下的 id 名为 name 的元素，节点对象（只有一个）

	nodeName.getElementById(name)；
	
>2.获取 nodeName 节点下的类名为 name 的所有元素，节点对象（返回值是数组，一个或多个节点对象）

	nodeName.getElementsByClassName(name)；
	
>3、获取 nodeName 节点下的标签名为 name 的所有元素节点对象（返回值是数组，一个或多个元素节点对象）

	nodeName.getElementsByTagName(name)；
	
>4、获取 nodeName 节点下的（标签名或者类名或者 id 名）：第一个元素节点（只有一个）

	nodeName.querySelector(name)；
	
>5、获取 nodeName 节点下的符合name (标签名或者类名或者id名)要求的所有元素节点（返回值是数组，一个或多个元素节点对象）
	
	nodeName.querySelectorAll(name)；
	

###2、节点
	
**特殊节点**

>1、文档节点 - document
	
>2、声明节点 - doctype

>3、body head title 节点


**节点之间的关系**

>1、父节点
	
	//获取父节点
	var p1 = document.getElementById('p1');
	console.log(p1.parentNode);

>2、子节点

	//获取子节点 childNodes
	var ul1 = document.getElementById('ul1');
	console.log(ul1.childNodes);
	//获取第一个子节点
	console.log(ul1.firstChild);
	//获取最后一个节点
	console.log(ul1.lastChild);

>3、兄弟节点	

	//下一个相邻兄弟节点
	console.log(p1.nextSibling);
	//上一个相邻兄弟节点
	console.log(p1.previousSibling);
	
**获取元素节点**

>1、获取子元素节点
		
	//获取第一个子元素节点
	console.log(ul1.firstElementChild);
	//获取所有的子元素节点
	console.log(ul1.children);
	//获取最后一个子元素节点
	console.log(ul1.lastElementChild);

>2、获取相邻兄弟元素节点

	//获取上一个相邻兄弟元素节点
	console.log(p1.previousElementSibling);
	//获取下一个相邻兄弟元素节点
	console.log(p1.nextElementSibling);

**节点属性**

>nodeValue：如果是文本节点或者属性节点，则打印内容，如果是元素节点则输出 null


**nodeType 节点类型**

	元素节点 ------ 1
	文本节点 ------ 3
	注释节点 ------ 8
	文档节点 ------ 9
	声明节点 ------ 10
	
**nodeName 节点名称**

	1.文本节点  ---- #text
	2.注释节点 ----- #comment
	3.元素节点 ----- 输出该标签名的大写
	
**往元素节点中添加内容（获取该元素节点的内容）**

	1.innerHTML 获取该元素节点里的所有内容(
		开始标签到结束标签之间的内容),
		包括文本节点,注释节点,元素节点
		
	2.innerText  获取该元素节点里的所有文本节点
	console.log(contentDiv.innerHTML);
	
	3、可以使用：childNodes和 nodeValue 属性来获取元素的内容
		
	var txt=document.getElementById("intro").childNodes[0].nodeValue;

**removeArribute -删除属性**

>inp.removeAttribute('value');

**replaceChild -替换标签**

>replaceChild(a,b);替换节点,将a和b节点进行替换

**insertBefore(a,b)**

>insertBefore(a,b);将元素节点a插入到元素节点b之前


###3、节点的使用--留言板


**1、div 设置**

	<input type="button" name="" id="message" value="留言" />
	<input type="text" name="" id="txt" value="" placeholder="请留言"/>
	<input type="button" name="" id="delay" value="删除" />
	<h2>留言板</h2>
	<ul id="ul1">
		<li></li>
	</ul>

**2、获得标签**

		var message = document.getElementById("message");
		var txt = document.getElementById("txt");
		var delay = document.getElementById("delay");
		var ul1 = document.getElementById("ul1");
		var lis = ul1.querySelectorAll("li");
		//给留言按钮添加点击事件
		var index =0;
	
**3、添加留言**
	
		message.onclick = function(){
		if(txt.value == ""){
			alert('不说点啥');
			return;
		}
		index++;
		if(index>1){
			var liObj = document.creatElement('li');
			liObj.innerHTML = '第'+index+'条：'+txt.value;
			ul1.insertBefore(liObj,ul1.children[0]);
		}else{
			var liObj = document.createElement('li');
			liObj.innerHTML = '第'+index+'条：'+txt.value;
			ul1.appendChild(liObj);
		}
		
		txt.value = "";//将输入值置空
	}	
	
	
**4、删除留言**

		1、删除最后添加的留言
		delay.onclick = function(){
		ul1.removeChild(ul1.children[0]);
		}
		2、删除最下的留言
		delay.onclick = function(){
		ul1.removeChild(ul1.children[ul1.children.length-1]);			
		}
	
###4、地址自动选中效果

>思路：将附带显示地址中的地址清空然后赋值为数组中值

**获得标签**

	var heNanCity = ['郑州市','开封市','信阳市','洛阳市'];
	var liaoNingCity = ['沈阳','大连','铁岭','抚顺'];
	//获取select元素对象
	var select1 = document.getElementById('sel1');
	var select2 = document.getElementById('sel2');


**为select1 添加点击切换 option 事件**

	//	注意:只有选中的option改变,才会触发事件
		select1.onchange = function  () {
	//	alert(select1.value);
	// 将seclect2中的所有option删除
        for (var i = 0;i < select2.children.length;i++) {
        	    //删除所有的option节点
        	    select2.removeChild(select2.children[i]);
        	    i--;
        }

**判断第一选项值是哪个**

	     //如果选中的是河南省
        if (select1.value == '1') {
        	for (var j = 0;j < heNanCity.length;j++) {
        		//创建option节点
        	  var opObj = document.createElement('option');
        	  opObj.innerHTML = heNanCity[j];
        	  //插入节点
        	  select2.appendChild(opObj);
        	}
        }
        //如果是辽宁省
        if (select1.value == '2') {
        	for (var k = 0;k < liaoNingCity.length;k++) {
        	var opObj =	document.createElement('option');
        	opObj.innerHTML = liaoNingCity[k];
        	select2.appendChild(opObj);
        	}
        }
