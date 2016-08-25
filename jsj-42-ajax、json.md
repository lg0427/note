###ajax 综合使用之 图灵自动对话回复

**html部分及获取相关元素**

	<input type="text" name="word" id="word" value="" />
	<button id="btn">提交</button>
	<div id="huihua"></div>
	
	<script type="text/javascript">
		var word = document.getElementById('word');
		var btn = document.getElementById('btn');
		var huihua = document.getElementById('huihua');
		var robotwords = null;
		function create(){
				//创建会话气泡
				var myWords = document.creatElement('div');
				myWords.innerHTML = "我："+word.value;
				myWords.setAttribute("class","user");
				huihua.appendChild(myWords);
				
**建立请求及获取数据**
				
				//创建请求
				var http = new XMLHttpRequest();
				var url = "http://www.tuling123.com/openapi/api?key=fb6b7bcfbe52fccdb7f5d752a3088f75&info="+word.value+"&userid=1234567";
				
				http.open("get",url,true);
				http.send(null);
				http.onreadystatechange = function(){
					if(http.readyState == 4 && http.status >=200 && http.status < 300 || http.status == 304){
					robotwords = JSON.parse(http.responseText).text;
					var robotBox = document.createElement('div');
					huihua.appendChild(robotBox);
				}
				//点击提交请求对话
				btn.onclick = function(){
					create();
				}
				
				
####用jq 方式实现代码如下
	
		<script src="http://lib.sinaapp.com/js/jquery/1.9.1/jquery-1.9.1.min.js"></script>		
				
		var url = "http://www.tuling123.com/openapi/api?key=fb6b7bcfbe52fccdb7f5d752a3088f75&info="+word.value+"&userid=1234567";
		$(function(){
			$.get(url,function(data){
				robotwords = data.text;
				var robotBox = document.createElement('div');
				robotBox.innerHTML = "robot:"+robotwords;
				huihua.appendChild(robotBox);
			},"json")
		})
			
			
###留言板功能简单前后台交互实现

**html前端页面内容**

>引入jq - cdn
	
	<script src="http://lib.sinaapp.com/js/jquery/1.9.1/jquery-1.9.1.min.js"></script>
	<script type="text/javascript">
		$(function(){
			$("#btn").on("olick",function(){
				$.ajax({
					type:"get",
					url:"weibo.php",
					async:true,
					dataType:"json",
					data:{
						content:$("#content").val(),
						flag:"add"
					},
					success:function(data){
						if(data.success=="tr"){
							addList(data.id,data.time);
						}
					}
				})
			})
		$(document)。on("click",".remove",function(event){
			var target = $(event.target);
			var targetid = target.parents("li").attr("data_id");
			$.ajax({
				type:"get",
				url:"weibo.php",
				async:true,
				data:{
					id;targetid,
					flag:"remove"
				},
				success:function(data){
					if(data == "success"){
						var h = target.parents("li").height();
						target.parends("li").animate({
							height:0
						},function(){
							target.parents('li').remove();
						})
					}
				}
			})
		})
 		function addList(id,time){
 			var html = $('<li data_id='+id+'><p>'+$("#content").val()+'</p><div id="control"><span>'+time+'</span><a href="###" class="remove">删除</a></div></li>');
 			$('#list').prepend(html);
 			
 			var h = html.height();
 			html.height(0);
 			html.animate({
 				height:h
 			});
 		}	
	})
	</script>	
				
**php后台交互部分**

>php 完成后台交互
	
		$con = mysql_connect("localhost","root","");//连接数据库
		mysql_select_db("liuyanban",$con);//选择要操作的数据库
		mysql_query("set names utf8");//编码格式
		date_default_timezone_set("PRC");//设置时区
	
		$flag = $_GET['flag'];
		//判断进行添加操作
		switch($flag){
			case "add":
				$time = time();
				$timer = date("Y-m-d H:i:s",$time);
				$content = $_GET['content'];
				$sql = "insert into liuyan_users(id,content,time) values(null,'$content','$timer')";//执行sql语句

				mysql_query($sql);
				if(mysql_insert_id($con)>0){
					$insertId = mysql_insert_id($con);//mysql_insert_id返回插入数据的id,如果大于0,表明插入成功

					$arr = array("id"=>$insertId,"time"=>$timer,"success"=>"tr");

					echo json_encode($arr);//将数组转换成对象
				}
				break;
	
				case "remove":
				$id = $_GET["id"];//获取前端页面传送过来的id值
				$sql = "delete from liuyan_users where id = '$id'";
				mysql_query($sql);//执行sql语句
				if(mysql_affected_rows($con)>0){//判断有没有删除成功
				//mysql_affected_rows()函数返回前一次,mysql操作,所影响的行数
					echo "success";
				}else{
					echo "default";
				}
		}
		