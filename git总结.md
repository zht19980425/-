# Git 基础语法及注意事项
## Git 基础语法
### 基本总结
1. 常见单词
	- `remote`表示与远程库相关
	- `tag`表示与标签有关
	- `stash`表示与暂存有关
	- `checkout`表示切换
	- `branch`表示分支的操作
	- `log`表示工作日志	
2. 常用参数
	- 参数`-m`表示自己的说明文字
	- 参数`-b`表示创建并切换分支
	- 参数`-d`表示删除，`-D`表示强制删除
### 具体语法
1. 基本操作(创建、提交、查看)
	- `$mkdir + A`：创建一个名称为A的文件夹
	- `$cd + A`:使git bash进入A中搞事情
	- `$git init`:使该文件夹成为工作区(实际上创建一个 *.git* 的隐藏文件夹)
	- `$pwd`:查看工作区路径
	- `$git add + 文件名(含拓展名)/(或者是一个文件夹(不带拓展名)、一张图片）`：使该文件进入暂存区
	- `$git rm --cached`:取消当前的add
	- `$git commit -m"描述性内容"`:将暂存区文件全部提交到本地仓库(创建指针),并获得 **commit id** *(一串数字与字母的混合)*
	- `$git status`:查看当前工作区情况 **(如是否有文件未add、未commit，是否有文件变动……)**
	- `$git diff`:查看工作区文件与指针下文件的区别并标注 *(红色为删除，绿色为添加)*
	- `$cat +文件名`:查看文件内容(如查看txt文本的内容)
	- `$git log`:查看更新日志(由上到下从晚到早)(加上参数` --pretty=oneline`(全部字符)或` --oneline`(前几位字符)(即命令为`$git log --pretty=oneline`或`git log --oneline`)只得到 **commit id**)
	- `$rm +文件名`:在暂存区中删除该文件
	- `$rm -r +文件名`:删除文件夹及其内部文件
2. 版本回退与返回
	##### 说明：当前版本为HEAD，之前为HEAD^，再之前为HEAD^^，多了可简写为"HEAD~数字"形式
	##### 说明：reset语句在注意事项中详细讲解
	- `$git reset --hard +需要的位置(如HEAD^)`：回退
	- `$git reset --hard +commit id`:可回退，也可返回现实
	- `$git reflog`:查看命令记录与 **commit id**
	- `$git checkout --+文件名`: *丢弃其在工作区的修改* (文件未add)
	- `$git reset HEAD`:将文件从暂存区中撤回 *(实质为返回当前版本下的状态)*
3. 远程库的操作
	- `$git remote add +自己命名的远程库的名字 +地址.git`:链接上远程库
	- `$git push -u +名字 +分支名`:将当前分支推送至远程库的分支 **(第一次推送)** (之后不用参数`-u`) **(远程库命名为所打名字)**
	 `$git clone +地址`:从云端克隆一份文档下来 **(默认只有master分支)** *(以文件夹形式克隆下来)*
	- `$git pull`:从远程库拉取文件(不以文件夹形式) **(可能发生分支冲突）** *(pull=fetch+merge)*
	- `$git pull --rebase +远程库名称 +分支名`:拉取 *并将文件合并至当前分支中* **(需本地有相同名字的分支，否则报错)**
	- `$git remote`:看远程库的名称
	- `$git remote -v`:查看远程库的名称与地址 **(分为*fetch*与*push*部分，无权限看不到*push*地址)**
	- `$git remote rm +远程库名称`:删除关联远程仓库
4. 分支的相关操作
	- `$git branch`:查看所有分支 **(用"*"、"高亮"来显示当前分支)**
	- `$git branch +分支名`:创建一个分支
	- `$git checkout +分支名`:切换分支
	- `$git checkout -b +分支名`:创建并切换至该分支
	- `$git merge +分支名`:将该分支合并至当前分支
![](https://gitee.com/HTLing/buptsice_training_2017_2/raw/git%E6%80%BB%E7%BB%93/fast_forward.png)
	- `$git branch -d +分支名`:删除该分支
	- `$git merge --abort`:放弃合并 **(在合并冲突分支时)**
	- `$git log --graph --pretty=oneline --abbrev-commit`:以分支图形式查看分支情况以及相应提交的*commit id*
	- `$git merge --no-ff -m"描述性内容” +分支名`:禁用*fast-forward*分支合并模式 **(删除分支后可保存分支信息，而采用fast-forward的方式不会保留)(如图)**
![](https://gitee.com/HTLing/buptsice_training_2017_2/raw/git%E6%80%BB%E7%BB%93/no_fast_forward.png)
	- `$git branch -D +分支名`:强制性删除该分支 **(即使其未进行合并)**
5. 其他(标签与暂存)
	- `$git stash`:使当前数据保留，进入stash区，从而放心debug
	- `$git stash list`:查看stash区与stash编号(如*stash@{0}*)
	- `$git stash apply +编号`:恢复但不删除stash区内容
	- `$git stash drop +编号`:删除stash内容
	- `$git stash pop +编号`:恢复并删除stash内容
	- `$git tag +标签名`:为当前分支最新commit文件打上标签
	- `$git tag`:查看所有标签
	- `$git show +标签名`:显示该标签的详细信息
	- `$git tag +标签名 +commit id`:为该commit自打标签 **(即可以为以前commit的文件打上标签)**
	- `$git tag -d +标签名`:删除该标签
	- `$git tag -a "标签名" -m"描述性内容"`:添加一个带说明的标签
	- `$git push +远程库名称 +标签名`:将标签推上远程库
	- `$git push +远程库 --tags`:一次性将标签全部推上远程库
## 一些注意事项
1. **使用之前设置全局用户名(推送上远程库有用)与全局邮箱(用于创建公钥与私钥)**

	1.1 语法：

		$git config --global user.name"用户名"
		$git config --global user.email"邮箱地址"

	1.2 在git中输入`$ssh-keygen -t rsa -c"全局邮箱地址”`来获得公钥与私钥 *(之后一路回车)*

2. **在远程仓库设置下设置SSH公钥(id_rsa.pub文件，用记事本打开)**。

	在git中用`$ssh-add ~/.ssh/id_rsa`添加私钥。

3. **远程仓库无法push**

	先pull一份文件下来，合并后即可上传 *(即保证云端与本地是同步的)*
> `pull`注意：推送时还会遇到一种情况，就是你克隆下来，然后修改，这时候别人已经在你克隆之后提交了修改，也就是他修改的部分并没有存在于你要提交的版本上，这就造成了你可能覆盖某个人的劳动成果，所以你需要先`git pull`，把他的和你的冲突手动解决之后再提交，注意commit修改之后再提交

4. **在根目录下创建`.gitignore`文件，向其中添加需要忽略的文件名称及后缀 (一类文件可用`*.后缀名`形式来表示)，然后add，commit即可设置忽略文件(或上网收集[gitignore](https://github.com/github/gitignore))**

	4.1. 使用`-f`参数进行强制添加

	4.2. 使用`$git check-ignore`检查哪行出问题

5. **打地址可使用https加密或ssh加密，但最后都要加上`.git`，否则无法上传 (链接时无法查出错误，只会在push等操作时进行报错)**

	5.1. https写法：`https://gitee(github).com/用户名/项目名.git` **(需要每次打开git的首次上传时进行账户检验，较麻烦)**

	5.2. ssh协议地址写法:`git@gitee(github).com:用户名/项目名.git`


6. **合并冲突(即两个分支都存在最新提交且不能快速合并时出现)**

	6.1. 在文件中，使用`<<<HEAD`之前代表相同，之后用`======`分割两个不同，最后`>>>+“被合并分支名”`来结束

	6.2. 解决完冲突后，再add、commit

	6.3. 对于云端，若本地文件不太重要(或只是单纯地搞搞)，可使用`$git pull --rebase +远程库名称 +分支名`语句直接抓取云端文件并自动将本地分支合并至云端分支**(仅限当前分支)**

	6.4. 若不行，则先设置本地分支与云端分支联系(master与master除外):`$ git branch --set-upstream +本地分支名 +云端分支名`，成功后在pull进行抓取，并在本地完成冲突合并，最后add、commit、推送上云端

7. **reset语句的三个参数:` --soft`,` --mixed`,` --hard`**
	
	7.1. ` --soft`参数：最轻微的回退，只回退至版本commit时的状况，即不改变工作区文件、暂存区文件

	7.2. ` --mixed`参数：中等程度的回退，回退至上一版本暂存区情况，但不改变工作区文件
	
	7.3. ` --hard`参数：最重的回退，完全回退至上一版本，改变暂存区与工作区的文件(一般情况少使用)
	
	7.4. **以上回退均可通过相应参数的回溯功能回归现实，句法与之前的相同，只是参数变化**
	
	7.5. 详情参见  [*这里*](http://blog.csdn.net/carolzhang8406/article/details/49761927)
	
	7.6. **最好自己实践一下，体会其中的的差别**

>### 本文感谢廖雪峰学长的官网支持(学长为北邮大佬),现附上链接[廖雪峰的git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)，在这表示忠心的感谢