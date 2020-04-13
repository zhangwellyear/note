## `Git 分支`
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
`git push <remote> <branch>` 将`branch`分支推送到`remote`服务器


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
+ `git log --oneline --decorate` —— 查看各个分支当前所指的对象

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

### 打标签
`git tag` —— 列出已有的标签

#### `git`支持的两种标签
+ 轻量标签（lightweight）—— 某个特定应用的引用（像一个不会改变的分支）
+ 附注标签（annotated）

#### 添加附注标签:
`git tag -a <version> -m <message>` —— 为某个`tag`添加附注信息
`git show <version>` —— 可以查看到版本为`version`的信息

#### 添加轻量标签
轻量标签本质上是将提交校验和存储到一个文件中 —— 没有保存其他信息
`git tag <version_name>` —— 创建名为`version_name`的轻量标签
`git show <tag>` —— 显示某一`tag`下的信息

#### 共享标签
`git push`命令不会传送标签到远程仓库，必须显式推送
`git push origin <tagname>`这个命令将传送标签到远程仓库
`git push origin --tags`这个命令会将不在远程仓库上的所有标签全部传送到远程仓库
`git tag -d <tagname>`删除标签

使用`git checkout <version>`命令会使仓库处于“分离头指针”的状态，一般不使用

### 创建别名
```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```

创建别名最有用的地方是能够为一些`git`中不存在短命令的指令创建别名，例如:<br>
1. 设置`unstage`命令（这个命令在`git`中是没有的） —— `git config --global alias.unstage 'reset HEAD --'`
2. 则`git unstage fileA`和`git reset HEAD -- fileA`两个命令是等价的

下面这个也十分常用：
`git config --global alias.last 'log -1 HEAD'` —— 设置后就可以用`git last`直接列出最后一次提交的相关信息啦

## `git`分支
使用分支意味着可以把工作从开发主线上分离开来

### `git`的便捷之处
+ 创建新分支
+ 不同分支之间进行切换

### 提交操作所保存提交对象所包含的内容
+ 作者的姓名和邮箱
+ 提交时输入的信息
+ 指向它的父对象的指针

### 提交操作的父对象
+ 首次提交没有父对象
+ 普通提交操作产生的提交对象只有一个父对象
+ 多个分支合并产生的提交对象有多个父对象

### 暂存操作
+ **暂存操作会为每一个文件计算校验和（使用`SHA-1`哈希算法）**
+ 会把当前版本的文件快照保存到`Git`仓库中（`Git`使用`blob`对象保存它们）

### 提交
1. `git commit`提交操作会计算每一个子目录的校验和
2. Git仓库中这些校验和保存为树对象
3. 创建一个提交对象，除包含1, 2步骤中的信息外，还包含指向树对象的指针

初次提交，git仓库中会有五个对象，三个`blob`对象，一个`树对象`，以及一个`提交对象`
做些修改后提交，产生的提交对象会含有上次提交对象的指针，上次提交对象为本次提交对象的父对象。

### 新建分支
`git checkout -b <branch_name>` —— 新建一个分支`branch_name`，并切换到对应分支
上述命令等价于:
1. `git branch <branch_name>`
2. `git checkout <branch_name>`

### 切换分支
切换分支前，保持一个干净的状态，否则可能会与即将切入的分支产生冲突。

暂存（`stashing`）和修补提交（`commit amending`）都能绕过该问题

### 合并分支
当合并两个分支时，从一个分支可以到达另一个分支，在合并时，只会简单的将指针向前推进

合并早期分支的情况：（开发历史可能从很早的地方分叉开来，`master`分支不再是另一个分支的祖先，如图所示）
![分叉处不同版本](./assets/git/分叉处的不同版本.png)
合并后的情况：（将两个枝杈的末端进行合并）
![分支合并](./assets/git/合并后不同版本.png)

### 删除分支
`git branch -d <branch_name>` —— 删除分支`branch_name`
临时因为处理一些紧急任务创建的分支，可以在被`master`分支合并后立即删除，主要协同开发分支尽量不要动。

### 解决分支冲突
`========`分割线将冲突的两个分支划分成了两个部分

### 分支管理
`git branch`命令既可以创建与删除分支，也可以得到当前所有分支的一个列表。
`*` 字符标记的分支代表现在检出的分支，此时提交，标记的分支将会向前移动。
`git branch -v` 查看每一个分支的最后一次提交
`git branch --merged` | `git branch --no-merged` 可以查看**已经合并到当前分支**的分支及**未合并到当前分支**的分支

`git branch -d <branch_name>` —— 如果`branch_name`分支尚未合并，此时运行该命令删除`branch_name`会失败

### 分支应用于开发工作
大型项目基本上有三个分支：
+ 稳定分支
+ 建议(`proposed`)分支
+ 建议更新(`pu: proposed updates`)分支

### 远程分支
远程引用是对远程仓库的引用，可以通过`git ls-remote <remote>`来显式地获取远程引用的完整列表

多个远程仓库与远程分支情况下，可以运行`git remote add`命令添加一个新的远程仓库引用到当前的项目。eg:
`git remote add teamone git://git.team1.ourcompany.com`

`git fetch <name>` 可以获取远程仓库有而本地没有的数据，eg:
`git fetch teamone`

### 共享分支
如希望共享分支`serverfix`, 可以运行如下命令：
`git push origin serverfix`，也就是`git push <remote> <branch>`

本地仓库名与远程仓库名不相同：
`git push origin serverfix: awsomebranch`: 将本地的`serverfix`分支推送到远程仓库上的`awsomebranch`

### 保存密码几分钟
`git config --global credential.helper cache`: 不用每次输入密码，密码可以暂存几分钟
` git checkout -b <branch_local> <remote>/<branch_remote>`: 基于远程的`branch_remote`创建一个名为`branch_local`的分支，这两个可以不一样，但是很多时候都是一样的，git提供了一种新的命令：
`git checkout --track` —— 创建本地与远程名字相同的库

### 跟踪
设置已有的本地分支跟踪刚刚拉取下来的远程分支，可以在任意时刻使用`-u`命令
`git branch -u origin/serverfix`

### 拉取代码
`git pull` 实际上等价于:
1. `git fetch`
2. `git merge`

### 删除远程分支
`git push origin --delete serverfix`

















### 在服务器上搭建自己的git