---
title: Git
---
## Git的起源
linux内核源代码一直在 bitkeep 上托管，但是bitkeep 突然收回对linux的授权，因为bitkeep说开源社区中的一个成员对bitkeep的协议进行逆向工程。因此，自己写了git。

`SVN`->`集中式版本控制系统`：只有中央服务器有版本的数据库，其他电脑没有，所有版本控制都要通过中央服务器进行交互。（要是中央服务器当机离线，则就出大问题了）  
`git`->`分布式版本控制`：每一个台电脑上面都有一个版本的database。由于每台电脑都有数据库，所以大多数操作可以离线进行。支持比较多的控制模式-也可以安装一个中央服务器。  

1. git每个版本存储的都是当前版本的所有内容，不需要与其他版本进行差异比较之后再进行文件的合成。  
1. git可以离线完成大部分操作。  
1. git有更优雅的分支和合并实现。  
1. git有更强大撤销修改和修改版本历史的能力。  
1. git速度更快，效率更高。

## 为什么学习git：
研究GitHub  
越来越多的公司通过git调整

## git如何存储文件，历史记录：
`git通过40个16进制字符的SHA-1 Hash 来唯一标识对象` 例如：     e98757d0598ab6eeaf1df0d87dd00826048bd80b  
git有`四种对象`：  
	1. blob：文本文件或者二进制文件或者链接文件  
	2. tree：目录  
	3. commit：历史提交	  
	4. tag：指向固定的历史提交  
	(->）指向的意思  
`tag`  `->`  `commit`  `->`  `tree`  `->`  `多个tree对象或者多个blob对象 ` 
对工作区的这些内容进行SHA-1 Hash 之后，就可以得到唯一标识。  
如果两个文件内容是相同的，则他们指向同一个blob对象。而文件名这种信息会存在tree对象中。  

有了git对象之后，需要git仓库去存储对象，和操作对象。  
git init   git clone  两种方法获取仓库。  
![](https://i.imgur.com/InyuRGB.png)
cd 到.git 文件夹中 （GIT_DIR!）-> git工作区间 	用 ls 查看git需要的文件  
再退出来  
用init方法创建一个裸仓库。然后查看仓库中有什么。  
git init --bare git_bare_repo  
通过--bare 方法创建一个 git_bare_repo 文件夹。这个文件夹只有git工作需要的文件。  
git clone 克隆出一个仓库 一般来说需要远程裸仓库的地址  
git clone git_bare_repo/ git_clone_repo （复制之前创建的本地仓库，并创建在文件夹  git_clone_repo中）  
	
## git分为三个区域：
> 1. working directory（工作区，日常编辑代码的地方）  
> 1. staging area（暂存区，工作区与历史提交的缓存，维护的是虚拟的树形结构）  
> 1. history repository（历史仓库）   

（1）工作区  添加文件到  暂存区  提交整个暂存区的状态   历史纪录区  
（2）历史记录区   检出文件到   暂存区和工作区  
大部分时间我们都在做第一个工作  
对应的就是 `git add（到暂存区）`  和  `git commit（到历史记录区）`  
    git status（查看工作区和暂存区的区别，确保提交是我们所需要的）  
    git rm（从暂存区删掉我们不需要的东西）  
    git mv（移动文件）  
    gitignore（确保不想添加到暂存区和历史纪录区的文件不被添加）  

> 先 创建  a b 两个文件  
> 	touch a  
> 	touch b  
> 然后添加到暂存区  
> 	git add a b  
> 查看一下   
> 	git status  
> 提交到历史纪录  
> 	git commit -m "initial commit" （加入一个提交的历史信息）  
> 修改一下a    
> 	vim a（加入一些文字信息）  
> 再看一下 git status   
> 	提示 a 修改了 但是没有提交到暂存区   
> 提交a到暂存区中  
> 	git add a   
> 再status 看一下  
> 	git status  
> 再提交 a 就行   
> 	git commit -m "modify a"  
> 删除a，会删除 工作区 ，暂存区中的a   
> 	git rm a   
> 还原一下a  
> 	git checkout a  
> 如何只删除暂存区的文件，不删除工作目录的文件  
> 	git rm --cached a  

<hr>
![](https://i.imgur.com/tAGY09M.png)
> git status 看看就会提示有一个没有跟踪的文件  
> git mv a c （将a名字命名为c）（这个命令是一系列操作的总和）  
> 	如果直接再工作区修改文件名  
> 		mv a c （工作目录直接 修改名字）  
> 	再 git status  
> 		提示 a 被删除了 ， 有个c 的文件没有被跟踪  
> 	再 git add a c（添加a c 到文件中）  
> 		提示文件 a 被更改为 c  
> git add -A 添加整个工作区都暂存区  
> git .gitignore	在顶层目录下创建一个.gitignore文件    
> *.[oa]通过通配符提示git，以 o 和 a 结尾的文件不要添加到git仓库中   
> 例如：加入了  *.~, *.pyc ， 但是如果以.pyc为后缀的文件，有一个要加到仓库，这个时候就要在文件名上加  !test.pyc，告诉 test.pyc 不要被忽略。如果需要ingore文件名第一个字符就是“！”，就要加上"\"转义字符。  
> **/res 匹配 res，所有路径下的res，任何文件夹下的res。  
> git add .gitignore  
> git commit -m "add ingore"//添加到仓库中，用于整个仓库的共享  


## git暂存区
> .git/objects 对象库  
> 当执行 git add 命令时，.git 目录下多了一个index文件，整个index文件就是暂存区，每条索引有个的四十位的十六进制的SHA-1 Hash，文件模式，权限，时间戳等。每个索引都对应对象库中的某个对象对应。  
> 除了索引之外，还维护了提前计算好的tree对象的内容。当我们提交的时候，可以直接通过提前计算好的，直接生成索引等内容。  
> 当文件名更改时，根据文件内容所计算出来的SHA-1 也不会变。  
> 暂存区索引每次更新的时候，都会重新计算index 和暂存区的内容。  

## git本地分支与合并  
	git branch（创建分支)  
	git tag（给commit做标记）  
	git checkout（分支之间的切换）  
	git stash（切换分支之前保存本地修改）  
	git merge（合并分支）

> 例如：git branch test  新建分支 test。但是只是新建，要切换过去才能使用  
> git checkout test 切换到test分支。   
> test分支做的修改，不会影响到master分区的工作。也就是说分支互不影响。

	tag 分 轻量级 本地引用  和 annotady 带注解的tag
	通过 git log --online --decorate --graph -all 查看hash值，以及提交，查看历史示意图  
	git tag "v0" a1abda30   （a1abda30 就是上述命令查出的hash值）  
	git tag -a "INITAL_COMMIT" a1abda30   标注tag，提示输出tag信息。  
	git tag 查看以有的设置过的tag  
	git config --global alias.lol "log --oneline --decorate --graph --all" 用 git lol 代替 log --oneline --decorate --graph --all  
	git show v0 （v0是一个tag的名字）  
   
## GitHub
提供个人或者企业的代码托管。可以查看其他的开源项目托管。  
![](https://i.imgur.com/qDXMcAv.png)