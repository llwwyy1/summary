# git学习报告

#### 1 使用git

##### 1.1.1基础目的

解决在多人共享工作时，避免多人更改同一份代码互相传来传去，（避免操作繁琐）

即：能更好的共享代码

##### 1.1.2 git 的两大特点

+ 版本控制： 可以解决多人同时开发的代码问题，也可以解决找回历史代码的问题

+ 分布式：Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。

  首先找一-台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器"

  仓库克隆- -份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，

  也从服务器仓库中拉取别人的提交。可以自己搭建这台服务器，也可以使用GitHub网站。

+ #集中式和分布式的区别在于对中央服务器的依赖程度

###### 1.2 安装git

略

##### 1.3创建一个版本库

+ ```
  $ mkdir learngit
  $ cd learngit
  $ pwd
  /Users/michael/learngit
  ```

+ ` pwd` 令用于显示当前仓库目录：

  ```
  llwwyy@LAPTOP-PTUPS403 MINGW64 ~ (master)
  $ pwd
  /c/Users/llwwyy
  
  ```

  

+ 使用`git init` 将该目录编程GIT可管理的仓库

``` 
$ git init

```

![image-20200304053540838](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304053540838.png)

+ 且创建一个名为readme.txt的文件并加入仓库中
  + ![](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304053916070.png)



###### 1.3时光机穿梭

+ 仓库状态

  + 修改`readme.txt`:

  ![image-20200304054132301](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304054132301.png)

  + 运行`git status`查看结果：

  ![image-20200304054303269](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304054303269.png)

  该命令可获知仓库状态，如图，告知我readme.txt被修改过但没有准备提交的修改

  + `git diff`可查看对仓库文件（即readme.txt）有过什么修改

  ![image-20200304054752618](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304054752618.png)

  观察易知改文件被删去了红色一行，并改为了绿色的一行

  + 将更改过的文件提交至仓库 `git add`
  + 在使用`git commit`前后使用`git status`可获取前后仓库的状态

  ![image-20200304055230809](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304055230809.png)

  （此时git告诉我们没有需要提交的修改，而且工作目录干净）

+ 版本回退

  + 再次修改一次并提交：

  ![image-20200304055814179](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304055814179.png)

  ![image-20200304055756132](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304055756132.png)

  + 回顾此时有三个版本呗提交到Git仓库：

  <img src="C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304055859388.png" alt="image-20200304055859388" style="zoom: 25%;" />

  + 使用`git log`查看仓库历史记录：

  <img src="C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304060139826.png" alt="image-20200304060139826" style="zoom: 80%;" />

  （由图可看出三次提交，最近的一次`append GPL` ，第二次是 `add distributed` ，最早的一次是 `wrote a readme file`）

  + `$ git log --pretty=oneline`则可输出相对较少的信息:

  ![image-20200304060509027](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304060509027.png)

  + 尝试将readme.txt回退到上个版本：
    + 在git中，`HEAD`表示当前版本，也就是上图中含蓝色的版本，上一个版本就是`HEAD^`,上上个就是`HEAD^^`且可以写成`HEAD~100`
    + 使用`git reset --HEAD`将当前版本回退到上个版本
    + 使用`git reset --hard 14dadb`回退到某个已知 版本号 的版本(这里不用输全部，git会自动寻找匹配)

  + 使用`git reflog`来查看自己的每一次命令:

  ![image-20200304061852352](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304061852352.png)

  + 使用`git log 和 git reflog`能很好的获取版本号，以便我们将仓库中文件的版本回溯到我们所想要的那样

+ 工作区和暂存区

  + 工作区：在电脑里能看到的目录，如learngit文件夹：

  ![image-20200304062702974](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304062702974.png)

  + 版本库：工作区有个隐藏目录`.git`，这个不是工作区，是Git的版本库

    当我们把文件加入Git版本库中时：

    第一步是用 git add 把文件添加进去，实际上就是把文件修改添加到暂存区(stag)；
    第二步是用 git commit 提交更改，实际上就是把暂存区的所有内容提交到当前分支。

+ 管理修改
  + 在如下操作时 第一次修改 -> git add -> 第二次修改 -> git commit 只有第一次的修改被保存，第二次的修改还需重复
  + Git 管理的是修改，当你用 git add 命令后，在工作区的第一次修改被放入暂存区，准备提
    交，但是，在工作区的第二次修改并没有放入暂存区，所以， git commit 只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交

+ 撤销修改

  + 使用`git checkout -- readme.txt`：

    +  一种是 readme.txt 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    + • 一种是 readme.txt 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

    总之，就是让这个文件回到最近一次 git commit 或 git add 时的状态（此时没有

    `git add`）。

  +  `git reset HEAD file` 可把暂存区的修改（已经`git add`）撤销掉（unstage），重新放回工作区

  + `git reset` 命令既可以回退版本，也可以把暂存区的修改回退到工作区

+ 删除文件

  +  在添加一个`test.txt`文件进入仓库，若在文件管理器将该文件删掉（或用rm命令）时，使用`git status`则会有所提示
  + 确实要从版本库中删除该文件，那就用命令 `git rm` 删掉，并且 `git commit` 

  + 另一种情况是删错了`git checkout` 其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

  ![image-20200304071309233](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304071309233.png)

###### 1.4远程仓库

远程仓库为Git重要功能之一。

+ 生成 SSH key:

  + 使用`$ ssh-keygen -t rsa -C "youremail@example.com"`创建SSH Key,找到.ssh目录并用`记事本`打开id_rsa.pub文件，复制到`github`里即可：

  ![image-20200304110327997](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304110327997.png)

![image-20200304110014257](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304110014257.png)

值得注意的是，Github允许添加多个key，若有多个设备，可将每台电脑的key添加到Github

+ 添加远程库

  + 使本地和github上的两个git库同步：
    + 使用 `git remote add origin git@github.com:githubname/filename.git`将该仓库与本机电脑相关联
    + `$ git push -u origin master`将本地库的所有内容推送到远程库上
    + `git push origin master`在第一推送后，就可使用不加`-u`的代码来进行远程推送

  ![image-20200304111656365](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304111656365.png)

  ![image-20200304111642581](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304111642581.png)

  ![image-20200304111625564](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304111625564.png)

+ 从远程库克隆

  + 在github上创建一个新的仓库，名字叫gitskills

  ![image-20200304112857467](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304112857467.png)

  + 使用`$ git clone  git@github.com:<githubname>/<filename>.git `来克隆出一个本地库

![image-20200304112753260](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304112753260.png)

##### 1.5分支管理

+ 分支：但 Git 的分支是与众不同的，无论创建、切换和删除分支，Git 在 1 秒钟之内就能完成！无论你的版本库是1个文
  件还是 1 万个文件。
+ 创建与合并分支
  + 创建dev分支：
    + `$ git checkout -b dev`表示创建并切换到dev分支
    + `$ git branch dev ` + `$ git checkout dev`同上
    + `git branch`查看当前分支有哪些
    + `$ git checkout master`在操作完dev分支后切换回master分支
    + `$ git merge dev`把dev分支的工作成果合并到master分支上
    + `$ git branch -d dev`删除dev分支

![image-20200304115645170](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304115645170.png)

![image-20200304115658949](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304115658949.png)

+ 解决冲突

  1. 准备新的feature1分支：创建一个名为`feature1`的分支，更改`readme.txt`文件内容为：

  `Creating a new branch is quick AND simple`

  2. add，commit后切回`master`分支，更改`readme.txt`文件内容为:

  `Creating a new branch is quick & simple.`

  提交。

  3. 使用`git merge feature1`命令合并两次修改，发现出冲突
  4. 再次add+commit，发现文件最终合并为一个（如最下图）

![image-20200304125927659](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304125927659.png)

![image-20200304125942842](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304125942842.png)

![image-20200304125947345](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304125947345.png)

![image-20200304130023394](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304130023394.png)

  5. `git log --graph`命令可以看到分支合并图（真是简单易懂呢_(:з」∠)_）

     ![image-20200304131427025](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304131427025.png)

+ Bug 分支

  + Git 提供 stash 功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：`$ git stash`（该功能能清空工作区，即使用`git status`查看工作区，显示工作区清空）

  + 然后去某个分支上修复bug，如到master修复后

  + 回到dev（此时有两种选择）：

    + `git stash apply`恢复后，stash内容不删除，要使用`git stash drop`来删除
    + `git stash pop`回复的同时将stash内容也删去

    ![image-20200304133208788](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304133208788.png)

  + 此时再使用`git stash list`查看，查看不到任何内容

    + 可以使用多次stash，回复时使用该指令查看后恢复指定的stash：
    + `$ git stash apply stash@{0}`

  + 结：当手头工作没有完成时，先把工作现场 git stash 一下，然后去修复 bug，修复后，再 git stash pop ，回到工作现场。

+ Feature分支
  
+ 开发一个新 feature，最好新建一个分支，要丢弃一个没有被合并过的分支，通过 git `branch -D <name>` 强行删除
  
+ 多人协作
  
  + 查看远程库信息：
  
    + 使用`git remote/git remote -v`来显示远程库简略/更详细的信息
  
    ![image-20200304142335391](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304142335391.png)
  
    + 上面显示了可 抓取 和 推送的origin的地址，若无权限，则看不到push地址
  
  + 推送分支
  
    + 推送指定本地分支：
  
      `$ git push origin master`
  
    + 若要推送其他分支，如dev：
  
      `$ git push origin dev`
  
    + 推送注意事项：
  
      • master 分支是主分支，因此要时刻与远程同步；
      • dev 分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
      • bug 分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
      • feature 分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
  
  + 抓取分支
  
    • 首先，可以试图用 `git push origin branch-name` 推送自己的修改；
    • 如果推送失败，则因为远程分支比你的本地更新，需要先用 `git pull` 试图合并；
    • 如果合并有冲突，则解决冲突，并在本地提交；
    • 没有冲突或者解决掉冲突后，再用 `git push origin branch-name` 推送就能成功！
    如果 `git pull` 提示`“no tracking information”`，则说明本地分支和远程分支的链接关系没有创建，用命令 `git branch --set-upstream branch-name origin/branch-name` 。
  
  + 结：
  
    • 查看远程库信息，使用 git remote -v ；
    • 本地新建的分支如果不推送到远程，对其他人就是不可见的；
    • 从本地推送分支，使用 git push origin branch-name ，如果推送失败，先用 git pull 抓取远程的新提交；
    • 在本地创建和远程分支对应的分支，使用 git checkout -b branch-name origin/branch-name ，本地和远 程分支的名称最好一致；
    • 建立本地分支和远程分支的关联，使用 git branch --set-upstream branch-name origin/branch-name ；
    • 从远程抓取分支，使用 git pull ，如果有冲突，要先处理冲突。

##### 1.6标签管理

+ 创建标签

  + 标签简介：标签是一个版本的快照，发布一个版本时，在版本库中打一个标签，就唯一确定了打标签时刻的版本。将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。

  + 标签操作：

    + 一种是切换到需要打标签的分支上，使用`git tag <name>`就可打一个标签

    ![image-20200304145524636](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304145524636.png)

    +  使用`git tag`可查看所有标签

    + 第二种是找到历史提交的`commit id` 然后打上即可：

    + ![image-20200304150108668](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304150108668.png)

    

![image-20200304150120275](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304150120275.png)
    
（注意标签不是以时间顺序排列，而是以字母排序的）
    
+ 创建有说明信息的标签，`-a`指定标签名， `-m`指定说明文字
  
  ![image-20200304154134868](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304154134868.png)
  
+ 使用`git show<lagname>`查看标签信息，
  
  ![image-20200305083333148](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200305083333148.png)
  
    + `-s`用私钥签名一个标签：（详略）
    
      ![image-20200304154400821](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200304154400821.png)
    
    + 结：• `git tag <name>` 用于新建一个标签，默认为` HEAD`，也可以指定一个`commit id `；
      • `git tag -a <tagname> -m "blablabla..." `可以指定标签信息；
      • `git tag -s <tagname> -m "blablabla..."` 可以用 PGP 签名标签；
      • ` git tag `查看所有标签。

+ 操作标签

  + 删除标签：

    `$ git tag -d <tagname>`

    ![image-20200305085905584](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200305085905584.png)

  + 标签推送：

    + 创建的标签只会储存在本地，不会推送到远程，所以若要推送某个标签，要进行特殊操作

    +  `git push origin <tagname>`推送某个标签到远程

    +  `git push origin --tags`推送所有本地标签到远程

    + 若要删除已推送的标签：

      + 先删除本地标签，然后使用`$ git push origin :refs/tags/<tagname>`

        ![image-20200305090608179](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200305090608179.png)

      + 至于是否远程删除成功，那要去github上查看了

    + 结：

      • 命令 git push origin <tagname> 可以推送一个本地标签；
      • 命令 git push origin --tags 可以推送全部未推送过的本地标签；
      • 命令 git tag -d <tagname> 可以删除一个本地标签；
      • 命令 git push origin :refs/tags/<tagname> 可以删除一个远程标签。

##### 1.7使用GitHub

+ 参与开源项目：

  + 首先在github上使用`fork`在自己账号下克隆一个`<repositoryname>`仓库，然后在从自己账号下clone:

    `git clone git@github.com:<githubname>/<repositoryname>.git`

  + 在对该库某个功能进行修改并希望官方能接受你的修改时，就可以在GitHub上发起一个`pull request`（当然，接不接受还得看对方）

##### 1.8自定义Git

+ 忽略特殊文件

  + `$ git config --global color.ui true`让 Git 显示颜色，会让命令输出看起来更醒目

  + 有些时候，你必须把某些文件放到 Git 工作目录中，但又不能提交它们,在git工作区目录下建立一个特殊的` .gitignore`文件，然后在里面把要忽略的 文件名字 填入进去，git就会自动忽略这些文件，且github上已经准备了各种配置文件：https://github.com/github/gitignore

  + 忽略文件的原则是：

    + 忽略操作系统自动生成的文件，比如缩略图等；
    + 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成 的文件就没必要放进版本库，比如Java编译产生的.class文件；
    + 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

  + 举例:
    假设你在 Windows 下进行 Python 开发，Windows 会自动在有图片的目录下生成隐藏的缩略图文件，如果有自定义目录，目录下就会有 `Desktop.ini` 文件，因此你需要忽略 Windows 自动生成的垃圾文件,然后，继续忽略 Python 编译产生的 `.pyc` 、 `.pyo` 、 `dist` 等文件或目录,加上你自己定义的文件，最终得到一个完整的 `.gitignore` 文件，内容如下：

    ![image-20200305093005754](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200305093005754.png)

  + 最后一步就是把 `.gitignore` 也提交到 Git，就完成了！当然检验 `.gitignore` 的标准是 `git status` 命令是不是说 `working directory clean`。

+ 配置别名

  + `$ git config --global alias.st status`告诉 Git，以后 `st` 就表示 `status`

  + `git config --global alias.unstage 'reset HEAD'`

+ 配置文件

  + 配置 Git 的时候，加上 `--global` 是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。每个仓库的 Git 配置文件都放在 `.git/config `文件中：

    ![image-20200305094555330](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200305094555330.png)

  + 而当前用户的配置文件放在一个隐藏文件`.gitconfig`中：

![image-20200305094808357](C:\Users\llwwyy\AppData\Roaming\Typora\typora-user-images\image-20200305094808357.png)

+ 搭建Git服务器(莫得实践机会，只能照搬)

  搭建 Git 服务器需要准备一台运行 `Linux` 的机器，推荐用 `Ubuntu` 或 `Debian`，这样，通过几条简单的 `apt`命令就可以完成安装。

  + 假设你已经有 `sudo `权限的用户账号，下面，正式开始安装。
    1. 安装git：`$ sudo apt-get install git`
    
    2. 创建git用户:`$ sudo adduser git`
    
    3. 创建证书登录：
       
    + 收集所有需要登录的用户的公钥，就是他们自己的 `id_rsa.pub `文件，把所有公钥导入到 `/home/git/.ssh/authorized_keys `文件里，一行一个。
       
    4. 初始化Git仓库：
    
       + 先选定一个目录作为 Git 仓库，假定是`/srv/sample.git `，在 `/srv` 目录下输入命令：`$ sudo git init --bare sample.git`
       + Git 就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的 Git 仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的 Git 仓库通常都以 `.git` 结尾。然后，把 `owner` 改为 `git`：
       + `$ sudo chown -R git:git sample.git`
    
    5. 禁用shell登录：
    
       + 出于安全考虑，第二步创建的git用户不允许登录 `shell`，这可以通过编辑 `/etc/passwd `文件完成。找到类似下面的一行：
         + `git:x:1001:1001:,,,:/home/git:/bin/bash`
         + 改为
         + `git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell`
         + 这样，Git 用户可以正常通过 ssh 使用 git，但无法登录 shell，因为我们为 git 用户指定的 git-shell 每次一登录就自动退出
    
    6. 克隆远程仓库
    
       + 通过`clone`克隆远程仓库即可
    
         + ```
           $ git clone git@server:/srv/sample.git 
           Cloning into 'sample'... 
           warning: You appear to have cloned an empty repository.
           ```

+ 管理公钥
  
+ 如果团队很小，把每个人的公钥收集起来放到服务`/home/git/.ssh/authorized_keys` 文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用 `Gitosis` 来管理公钥。这里我们不介绍怎么玩 `Gitosis` 了，几百号人的团队基本都在 500 强了，相信找个高水平的 Linux 管理员问题不大。
  
+ 管理权限
  
+ 有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为 Git 是为 Linux 源代码托管而开发的，所以 Git 也继承了开源社区的精神，不支持权限控制。不过，因为 Git 支持钩子（`hook`），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。`Gitolite `就是这个工具。这里我们也不介绍 `Gitolite `了，不要把有限的生命浪费到权限斗争中。
  
+ 结：
  +  搭建 Git 服务器非常简单，通常 10 分钟即可完成
  +  要方便管理公钥，用 `Gitosis`
  +  要像 `SVN` 那样的控制权限，用` Gitolite`。