# HTML5 本地存储

[origin](http://www.cnblogs.com/xiaowei0705/archive/2011/04/19/2021372.html)
[origin01](http://www.w3school.com.cn/html5/html_5_webstorage.asp)
## WEB 存储发展
![web storage history](http://pic002.cnblogs.com/images/2011/219983/2011052411382518.jpg)

方式 | 大小 | 说明
:---: | :---: | :---:
cookies | 4k | HTTP
userData | 64k | IE
Flash | 100K |
SQLite | 无限制 | 微软推出
HTML5 | 5M | 无需插件

##  浏览器兼容性

![HTML5 WEB Storage 浏览器兼容性](http://pic002.cnblogs.com/images/2011/219983/2011052411384081.jpg)

浏览器 | 最低兼容版本
:----: | :----:
IE | 8.0
FireFox | 3.0
Opera | 10.5
Chrome | 4.0
Safari | 4.0
iPhone | 2.0
Android | 2.0

> IE/Firefox 需要把文件上传服务器或使用localhost

## 使用

> 在HTML5中，本地存储是一个window的属性，包括 **localStorage** 和 **sessionStorage**

> localStorage : 一直在本地存储，无时间限制

> sessionStorage : 和`session`类似，一旦关闭浏览器就清除

> 以下以 localStorage 为例

### 赋值与删除

> 操作与操作具体的JS对象相似

	localStorage.a = 3;
	localStorage['a'] = 'abc'; // 覆盖上面的值
	var temp = localStorage.a; // 取值

> 相关方法

* getItem()
  根据key获取值
* setItem()
  设置key和value
* removeItem()
  根据key删除该键值对
* clear()
  清除全部的键值对
* key()
  遍历时根据下标获取key

		localStorage.setItem('b','wtf');
		localStorage.setItem('c','null');
		var test = localStorage.getItem('b');
		localStorage.removeItem('b');
		for(var i=0; i<localStorage.length;i++){
			document.write(localStorage.key(i) +" : " + localStorage.getItem(localStorage.key(i))+"<br />");
		}
		localStorage.clear();

### 示例代码

计数器

	var storage = window.localStorage;
	if (!storage.getItem("pageLoadCount")){ storage.setItem("pageLoadCount",0);}else{
	storage.pageLoadCount = parseInt(storage.getItem("pageLoadCount")) + 1;//必须格式转换}
	document.getElementByIdx_x("count").innerHTML = storage.pageLoadCount;
	showStorage();

### 注意

HTML5 本地存储只能存储**字符串**，因此读取数据时根据需要进行**类型转换**

出现 `QUOTA_EXCEEDED_ERR` 时，先 `removeItem()` 然后再 `setItem()` 就行了
