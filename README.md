##搜索GitHub 详细教程


###mac下对目录的隐藏操作

**显示mac 隐藏文件命令**

	defaults write com.apple.finder AppleShowAllFiles YES
	
**隐藏mac 隐藏文件的命令**

	defaults write com.apple.finder AppleShowAllFiles NO
	
**输完单击Enter键，退出终端，重新启动Finder**

###修改中文乱码

**目录下有中文，乱码显示**
	
	git config --global core.quotepath false
	
###修改用户名和邮箱名对应

**无法上传文件**

	 git config —global user.name “your name"
	 
    git config —global user.email “your email"
    
 <hr>
    
##new creat

###creat a new repository on the command line

**新建一个记录提交操作的文档**

1 . echo "# Fly_bird" >> README.md


**初始化本地**

2 . get init 

**添加**

3 . git add README.md

**提交到仓库，并写一些注释**

4 . git commit -m "first commit"

**连接远程仓库并建一个名叫：origin 的别名**

5 . git remote add origin git@github.com:Stevendwy/Fly_bird.git

**将本地仓库的东西提交到地址是origin 的地址，master分支下**

6 . push -u origin master

***

### push an existing repository from the command line

>git remote add origin git@github.com:Stevendwy/Fly_bird.git

>git push -u origin master


###import code from another repository


>You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
>

***

###Linux 常用命令大全
	
**文件和目录**

**查看**		
>cd/home 进入home 目录
>
>cd . . 返回上一级
>
>pwd 显示工作路径
>
>ls 查看目录中文件
>
>ls -F 查看目录中的文件
>
>ls -l 显示文件中和目录的详细资料
>
>ls -a 显示隐藏文件
>

**创建**
>mkdir dii 创建一个叫做 “dii” 的目录
>
>mkdir dii1 dii2 同时创建两个目录
>

**删除文件**
>rm -f file1 删除一个叫 file1 的文件
>
>rmdir dir1  删除一个叫 dir1 的目录
>
>rm -rf dir1 删除一个叫 dir1 的目录并同时删除其内容
>

**拷贝文件**
>cp file1 file2 复制一个文件
>
>cp -a dir1 dir2 复制一个目录
>


**重启**
>reboot 重启
>
>shutdown -r now 重启
>
>

**清屏**
>clear


***

###md 的使用

 1、 编辑文件级别 用 #
 
 2、 文字前加- 或* 无序列表，加1、2、3 为有序
  *前后各有一个空格
 
 3、 插入链接与图片
 	
 	图片： ![](){img地址}
	链接： []() 
	
 4、 表格：冒号用于对齐，竖杠用于划分表格
 	
 	|表头|文字|
 	|:—|:—|
	
|表头|文字|	
|:--|:--|
|||

	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
<!---->	