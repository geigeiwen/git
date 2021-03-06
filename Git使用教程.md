***Git 使用教程***

由于ICS作业提交问题，故而要使用git。

下面是有关git的介绍：

（https://www.runoob.com/w3cnote/git-five-minutes-tutorial.html）这是git五分钟教程

（https://www.runoob.com/w3cnote/git-guide.html）这是简明的git教程

git的结构图

![img](https://upload-images.jianshu.io/upload_images/14329037-157479f50f6997e4.png?imageMogr2/auto-orient/strip|imageView2/2/w/666/format/webp)

其中：

working directory 是存放工作代码的位置，平时最新的工作代码存放在这里。

stage 是暂存区域，暂时存放你的变动。

repository 是仓库，存放每一个版本的信息的地方，方便记录你的编辑记录，方便回溯改动。

Git 的工作流程一般是：

1. 在工作目录中添加、修改文件；
2. 将需要进行版本管理的文件放入暂存区域；
3. 将暂存区域的文件提交到 Git 仓库。

因此，Git 管理的文件有三种状态：已修改（modified）、已暂存（staged）和已提交（committed），依次对应上边的每一个流程。



### Git 入门教程



初始化GIT：

先使用git init来初始化，把某个目录加入git的版本追踪之中



最简单的添加与提交：

git add “某个文件”

git commit -m “...”后面可以添加任意关于提交的修改备注

需要注意的是commit可以在多次add之后一次性提交多个文件

Q：我commit的文件去哪儿了？



对文件进行修改：

1.先对readme.txt进行修改

2.输入git status 来查看git现在的状态

![image-20200829143225876](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829143225876.png)

现在我们可以看到出现了修改的记录

如果要详细查看到底修改了什么内容，输入git diff

![image-20200829143338149](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829143338149.png)

例如上图，就显示出我增加了一行"git is so hard"

同样也可以先add 然后对git 使用git status，查看add的内容，总之在提交之前对自己的修改内容比较熟悉，有助于我们放心的进行提交。

总之，要掌握工作区的动态，及时使用git status进行查看



就像打galgame进行存档一样，我们随时可以对现有的git进度进行保存和读取，万一退出，也可以恢复之前的进度。

要打开存档列表（或者说编辑记录列表），我们需要输入命令：git log

![image-20200829145015166](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829145015166.png)

从而我们得到了从开始到现在的各个版本的区别改动

commit id就是前面那一串很长的十六进制数，就是我们的提交编号



如何进行读档（版本回退）呢？

由于git的HEAD指向的是最新的版本，上一个版本就是HEAD^，上上个版本就是HEAD^^

如果版本个数过多，我们采用HEAD～x来表示

现在我们进行版本回退工作

![image-20200829145721769](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829145721769.png)

输入： git reset --hard HEAD^，我们成功回到了过去

也可以输入 git reset --hard + 具体的commit id（一般来说只需要前几位，git会自动查找）

但是如果我们想回到未来怎么办？

同样输入git reset --hard + 具体的commit id（如果你上面的窗口没有关闭你可以轻松找到那个id）

那如果我把窗口关闭了，同时也想不起来id了怎么办呢？

输入git reflog，它记录了你的每一次命令，你可以轻松找到id

![image-20200829150450109](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829150450109.png)

例如以上截图，我们找到了HEAD指针的指向变化

事实上，上面的种种操作都是改变了git中的HEAD指针的指向位置，这样就能显示出不同的版本号了



温习一下git的结构：

![image-20200829151456327](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829151456327.png)

我刚刚的git目录就是工作区，stage就是在工作区中修改的readme.txt提交到的地方，然后会commit到master分支树

操作结构：

1.在工作区进行修改

2.把修改提交到暂存区

3.把暂存区的修改commit到分支（这时暂存区被清空）

注意：commit只会提交存储在暂存区的修改，如果修改仅仅保留在工作区那么是无法被提交的



如何放弃修改呢？

输入git checkout -- <filename> 可以丢弃工作区的修改，文件返回到最近一次commit或者add的情况

输入git reset HEAD <filename>  可以丢弃暂存区的修改，回到工作区状态（HEAD表示最新状态）

输入git reset --hard HEAD^ （或者是id）可以返回到其他版本，适用于已经commit的情况

如果你已经提交到了远程版本库...那你💊



删除文件：

rm <文件名>

输入git status，可以看到git对修改作出了反应

此时，你有两个选择：

1.你选择从git的版本库删除这个文件

输入git rm和git commit，可以成功提交删除（从这里可以看出git保存的其实是修改）

2.你错误删除了文件

使用git checkout -- <filename>恢复文件

checkout命令实际上就是用版本库里面的最新文件替代工作区的文件



### Git进阶（远程仓库）

以github为例子

首先创造一个github账号和仓库

在本地产生ssh钥匙，在github账号中添加

下一步，将本地仓库和远程仓库关联起来

（我输入的是：git remote add origin git@github.com:geigeiwen/git.git）

然后就可以进行推送了

第一次推送到远程库，输入git push -u origin master，加上-u是把远程的master分支和本地的master分支关联起来

之后就可以通过git push origin master来不断推送远程库了



反过来，我们可以从远程库克隆到本地，再进行查询与编辑，之后提交到远程

git clone git@github.com:michaelliao/gitskills.git



#### 创建分支

git最终产生的结果由分支和主线来组成，git鼓励用户产生很多分支，最终合并成一个主线

首先我们创造一个新的分支并切换到那个分支：

git checkout -b dev

约等于

git branch dev
git checkout dev

切换成功后可以在另一个分支下面进行修改（往往这样更加安全）

使用git checkout  <branchname>可以切换到不同的分支

事实上

也可以用switch命令

例如创建并切换到新的分支上：

git switch -b dev

之后就可以使用：git switch dev 切换到dev分支上

这样更加自然

最后进行合并，我们切换到master分支上，输入命令：git merge <branchname>从而可以把支线合并到主线之上

**注意**可能出现问题，比如在支线只做了修改而没有进行add和commit，就会报错Already up to date

![image-20200829191746406](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829191746406.png)

合并成功

Fast-forward 是一种快进合并方式

合并结束后输入git branch -d dev，成功删除dev分支

**注意**

当master和dev都有新的提交（比如各自修改并commit了一个readme版本）的时候，强行进行merge会有风险，此时我们应该手动进行修改

![image-20200829192603708](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829192603708.png)

转化为以下的图形：

![image-20200829192635898](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829192635898.png)

这样就可以合并了

输入命令：git log --graph可以看到分支的合并和拆分情况



合并也可以不采用fast模式，因为这样会消除合并的历史

我们采用以下的输入：

![image-20200829193536326](/home/lkw/snap/typora/6/.config/Typora/typora-user-images/image-20200829193536326.png)

加上--no-ff和备注""之后，就可以保留合并的历史了