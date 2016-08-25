###判断有没有get 到值


**php代码如下**

	if($_GET["path"]){
		$path = $_GET["path"];
	}else{
		$path = ".";//第一次进入php 文件时不会$_GET 到值
	}
	echo $path."<hr>"
	
	//判断是否删除
	if ($_GET['remove']){
		$removePath = $_GET['remove'];
		function remove(){
			//先判断是文件夹还是文件，如果是文件直接删除，如果是文件夹就先删除其中的文件，然后删除
			if(is_dir($removePath)){
				$dirArr = scandir($removePath);//是文件，获取文件夹下的子文件
				if(count($dirArr) > 2){
					//文件夹不为空，遍历其中的所有文件
					for ($i=2;$i<count($dirArr;$i++){
						$dirn = $dirArr[$i];//找到每一个子文件
						$url = $removePath."/".$dirn;//拼接子文件的具体路径
						remove($url);//对子文件再次判断
					}
				}
				rmdir($removePath);//当文件夹中的文件全部被清除后，再删除文件夹
			}else{
				unlink($removePath);//是文件
			}
		}
		remove($removePath);
	}
	
	$files = scandir($path);
	print_r($files);
	
	
**html 代码如下**	

		<table border="1">
		<tr>
			<th>文件名</th>
			<th>创建时间</th>
			<th>文件大小</th>
			<th>文件操作</th>
		</tr>
		
		<!--使用循环遍历当前文件夹下面的文件-->
		<?php 
		foreach($files as $value){
			//	拼接文件的具体路径
		    	$url = $path."/".$value;
					echo $value;
		?>
			<tr>
				<td>
					<?php 
					//	 判断当前文件是不是文件夹
						if(is_dir($url)){
							echo "<a href='files.php?path={$url}'>{$value}</a>";
						}else{
							echo $value;//	如果不是文件夹而是具体的文件
						}   
					?>
				</td>
				<td>
					<?php 
							//	设置时间为北京时间
					    date_default_timezone_set("PRC");
							$time = filectime($url);//获取时间戳 
							echo date("Y-m-d H:i:s", $time);
					?>
				</td>
				<td>
					<?php 
					    	$filesize = filesize($url); //获取文件的大小
							echo sprintf("%.2fkb",$filesize/1024);
					?>
				</td>
				<td>
					<a href="files.php?remove=<?php echo $url; ?>">删除</a>
				</td>
			</tr>
			
		<?php 
		} 
		?>
	</table>
	