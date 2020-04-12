### git与其他管理系统的差异
+ 其他管理系统记录的是基于差异的版本控制
+ `git`像是把数据看成小型文件系统的一系列快照

`git`无需连接服务器获取数据

`git`数据库中保存的信息都是由文件生成的`hash`值索引的。

### `git`的三种状态
+ 已提交（`committed`）
+ 已修改（`modified`）
+ 已暂存（`staged`）

### `git`三种状态对应的三个阶段
+ 工作区
+ 暂存区
+ `Git`目录

### `git`的一些常用命令
`git config --list`
`git config <key>`可以用来查看某一项固定的配置

`git clone <url>`克隆某一个库
`git add <files>` —— 如果`files`是一个目录，那么将递归地跟踪目录下的所有文件

`git diff` 直接查看尚未暂存的文件更新了哪部分
`git diff --staged` 查看已暂存的将要添加到下次提交里的内容

`git commit` 使用该命令时，弹出的编辑器为`git`默认编辑器，配置方式可以参考教程第一章
`git commit -m <message>` 按照`message`信息进行本次提交，每次提交都是对项目做一次快照
`git commit -a -m <message>` 按照`message`信息提交，因为加上了命令`-a`, 所以会自动把所有已经跟踪过的文件暂存起来一并提交。（往往用在一次性提交所有修改文件时）
`git remote` 列出指定的每一个远程服务器的简写
`git remote -v` 显示远程服务器简写及其URL
`git remote add <shortname> <url>` 将地址为`url`的远程仓库添加到本地，同时用`shortname`来进行简写
`git fetch <shortname>` 可以获取上文中使用`shortname`指定的`url`远程仓库的内容
`git fetch <url>` 如果没有使用上面命令中的`shortname`，就需要指定详细的`url`以获取远程仓库的内容，拉取后会拥有远程仓库中所有**分支的引用**

### `git`的基础应该学会的
+ 配置并初始化一个仓库
+ 开始/停止追踪文件
+ 暂存/提交更改

### 进一步需要了解的
+ 配置`git`忽略指定的**文件**和**文件模式**(`.gitignore`)
+ 撤销错误操作 
+ 浏览项目历史版本
+ 浏览不同提交之间的差异
+ 向远程仓库推送 (`push`)
+ 从远程拉取 (`pull`)

### `.gitignore`
该子目录中含有初始化的Git仓库中所有的必须文件
项目根目录一定有`.gitignore`文件，子目录下也可以有，但子目录下的`.gitignore`仅仅作用于子目录中

### 克隆远程仓库，本地执行步骤
1. 当前目录下创建一个目录（目录名为项目名）
2. 在创建的目录下初始化一个`.git`文件夹
3. 远程仓库拉取所有数据至`.git`文件夹
4. 从`.git`文件夹中读取最新版本的文件的拷贝

### 已跟踪文件与未跟踪文件状态
+ 创建一个新的文件，`VS Code`中显示为`U`绿色的文件为未跟踪文件。在之前的快照（提交）中没有这些文件
+ 其他除了被忽略的，都是已跟踪文件，就是在`git`中存在记录

### `git add`的三个功能
1. 追踪新文件
2. 将已跟踪的文件
3. 用于合并时把有冲突的文件标记
运行`git add`添加文件后，又修改文件，需要再次运行`git add`重新添加，否则，提交的文件为第一次使用`git add`时

### `.gitignore`文件格式规范
+ 所有空行或者以`#`开头的行都会被Git忽略
+ 使用标准的`glob`模式匹配，会递归地应用在整个工作区中 ？？？
+ 匹配模式可以以（`/`）开头防止递归
+ 匹配模式可以以（`/`）结尾指定目录
+ 忽略指定模式以外的文件或目录，可以在模式前加上叹号（`!`）取反

`glob`模式：`shell`所使用的简化了的正则表达式

### 移除文件注意事项
命令：`git rm <files>`
作用：从**已跟踪**文件清单中移除（准确地讲，是从暂存区域移除），同时该文件被删除，也就是说，如果文件只是新建，没有使用`add`进行跟踪，该命令对文件无效。
解决的问题：如果不使用该命令而直接删除某个文件，运行`git status`，会出现`"changes not staged for commit"`

命令：`git rm --cached <files>`
作用：从**已跟踪**文件清单中移除（准确地讲，是从暂存区域移除），同时保留文件。
解决的问题：当一个很大的日志文件忘记添加到`.gitignore`中时，使用这种方法十分有效

### 文件改名
命令：`git mv <file_from> <file_to>`
相当于执行了三个命令：
```bash
mv README.md README
git rm README.md
git add README
```
在使用工具批处理改名后，第二种方法比较常用

### 查看提交历史
+ `git log` —— 按时间先后顺序列出所有的提交，最近的更新排在最上面
+ `git log -p -2` —— 显示每次提交所引入的差异，`-2`参数限制显示的日志条目数量为2
+ `git log --stat` —— 可以看到每次提交的简略信息
+ `git log --pretty=<option>`(`option=[online, short, full, fuller]`)
+ `git log --pretty=format:"%h - %an, %ar : %s"` —— 按照固定格式显示提交信息
+ `git log --pretty=format:"%h %s" --graph` —— 结合`--graph`将会以图表方式显示
+ `git log --since=2.week` | `git log --since="2018-01-15"` | `git log --since="2 years 1 day 3 minutes age"` —— 显示出截止到某一时间的提交
+ `git log -S function_name` —— 显示添加或删除了`function_name`函数的引用的提交
+ `git`常用参数如图:
![`git log`常用参数](./assets/git/git_log相关参数.png)

### 撤销操作
+ `git commit --amend` —— 如果提交后忽然发现自己忘了添加一个文件，此时可以使用该命令及时补救添加
```bash
git commit -m "initial commit"
git add forgotten_file
git commit --amend
```
+ `git reset HEAD <file>` —— 取消暂存
+ `git checkout -- <file>` —— 取消本地修改

### 远程仓库
托管在因特网或其他网络中的项目的版本库

#### 管理远程仓库的内容包括
1. 如何添加远程仓库
2. 移除无效的远程仓库
3. 管理不同的远程分支
4. 定义仓库内的数据是否被追踪



























### 在服务器上搭建自己的git