---
title: Git命令
date: 2021-02-02 10:02:19
tags:
- Git命令
---



# 1. Git

## 1.1 Git简介

### 1.1.1 安装Git

<!--more-->
- Windows

  在官网下载Git最新版本后，安装。然后在命令窗口输入以下命令

  ```
  git config --global user.name "Your Name"
  git config --global user.email "email@example.com"
  ```

  注意`git config`命令的`--global`参数，用了这个参数，表示你这台PC上所有的Git仓库都会使用这个配置

- Mac OS X

  就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装。需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了

- Linux（Ubuntu）

  在终端中输入`sudo apt-get install git`即可完成安装

### 1.1.2 创建版本库

版本库又名仓库（repository），可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”

所以，创建一个版本库十分简单。

首先在一个合适的地方创建一个空目录，然后进入该目录，通过`git init`命令把这个目录变成Git可以管理的仓库

![image-20210124134101593](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124134101593.png)

当前目录下多了一个`.git`的目录，这个目录是Git来跟踪管理版本库的，不要随意更改目录中的内容

如果没有看到`.git`目录，那是因为它默认是隐藏的，用`ls -ah`命令就可以看见

![image-20210124134647313](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124163457340.png)

- 将文件添加到版本库（仓库）

  首先这里再明确一下，所有的版本控制系统，其实只能跟踪==文本文件==的改动，比如txt文件、网页、所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

  不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的。使用版本控制系统时要以纯文本方式编写文件。

  此外，千万不要使用Windows自带的**记事本**编辑任何文本文件，原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来保存UTF-8编码的文件。他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。故下载Notepad++代替记事本，记得把Notepad++的默认编码设置为UTF-8 without BOM

  因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，建议使用UTF-8编码，被所有平台所支持

  在git1目录下新建一个readme.txt文件（子目录下新建也可），内容如下

  ```
  Nobody knows China better than me.
  It's a fake news.
  没人能在法国投降之前占领巴黎。
  ```

  和把大象放到冰箱需要3步相比，把一个文件放到Git仓库只需要两步。

  - 第一步：用命令`git add`把文件添加到仓库

    ```
    git add readme.txt
    ```

  - 第二步：用命令`git commit`把文件提交到仓库

    ```
    git commit -m "first commit"
    ```

    ![image-20210124142530752](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124155134395.png)

  简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，这样你就能从历史记录里方便地找到改动记录

  `1 file changed`说明1个文件被改动（我们新添加的readme.txt文件）

  `3 insertions`说明插入了3行内容（readme.txt有3行内容）。

  可以多次`add`不同的文件，最后一次性全部提交，比如：

  ```
  git add file1.txt
  git add file2.txt file3.txt
  git commit -m "add 3 files."
  ```

- 注意事项

  Git命令必须在Git仓库目录内执行（`git init`除外），在仓库目录外执行是没有意义的

  添加某个文件时，该文件必须在当前目录下存在，用`ls`或者`dir`命令查看当前目录的文件，看看文件是否存在，或者是否写错了文件名

### 1.1.3 总结

初始化一个Git仓库，使用`git init`命令。

添加文件到Git仓库，分两步：

1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件
2. 使用命令`git commit -m <message>`，提交

## 1.2 时光机穿梭

### 1.2.1 修改文件

- 修改readme.txt文件，用命令`git status`查看结果：

  ![image-20210124155134395](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124142530752.png)

  上述输出结果告诉我们：readme.txt`被修改过了，但还没有提交

  

  若要查看修改的内容，则用命令`git diff readme.txt`：

  ![image-20210124163457340](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124134647313.png)

  输出结果说明修改的内容为：

  将“没人能在法国头像之前占领巴黎。” 改为 “没人能在法国头像之前占领巴黎”

  

  若继续改动，在上一次修改的基础上将前两句的句号也都删除：

  ![image-20210124173804691](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124174929199.png)

  可以发现，之前的修改并没有在保存到仓库中

  

  再修改一次，将首字母改为小写：

  ![image-20210124174549168](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124173804691.png)

  可以看到，之前的修改仍然没有保存

  

  此时，将修改添加到仓库后查看仓库当前状态：

  ![image-20210124174929199](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124174549168.png)

  可以看到，`changes to be committed`说明将要被提交的修改包括`readme.txt`

  

  提交之后，再查看仓库状态：

  ![image-20210124175611550](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124185500264.png)

​	Git告诉我们当前没有需要提交的修改，而且工作目录干净（working tree clean）

- 总结
  1. 要随时掌握工作区的状态，使用`git status`命令

  2. 如果`git status`告诉你有文件被修改过，用`git diff`可以查看修改内容

### 1.2.2 版本回退

-  首先，用`git log`命令查看提交（commit）的历史记录：

  ![image-20210124183017705](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124175611550.png)

  我们可以看到有2次提交，其中`first commit`和`second commit`是提交时加上的说明，当前仓库所处的状态是第2次提交之后的状态，若觉得容易眼花缭乱，可以加上`--pretty=oneline`参数：

  ![image-20210124183720437](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124183017705.png)

  在Git中，`HEAD`表示当前版本，上一个版本是`HEAD`\^，上上个版本是`HEAD`\^\^，上上上个版本是`HEAD`\^\^\^，前n个版本是`HEAD`~n

- 将当前版本（second commit）回退到上一个版本（first commit），用`reset`命令：

  ![image-20210124185500264](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124183720437.png)

  `--hard`参数以后再说，现在先使用。结果显示当前版本的版本号`commit id`与第1次提交时的版本号一致，说明回退到了上一个版本。

  如果不相信，可以通过`cat readme.txt`命令查看文件信息（cat命令是直接查看文件信息内容的）：

  ![image-20210124185859799](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124190329356.png)

  可以看到，此时`readme.txt`文件的内容与第1次提交时的一致，说明真的回退到了第1个版本

  

  此时再查看仓库的状态：

  ![image-20210124190329356](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124191403893.png)

  ==发现`second commit`版本已经消失不见了==。若想回到最新的版本`second commit`，则只要命令窗口没有关掉，就可以顺着窗口找到`second commit`版本的`commit id`，然后通过命令`git reset --hard 8e381`回退到之后的版本（版本号写前几位即可，Git会自己去找。当然了，也不能只写前一两位）。此时查看`readme.txt`的内容：

  ![image-20210124191403893](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124185859799.png)

  可以看到，成功回退到了`second commit`版本。而且回退速度非常快，因为Git内部有个指向当前版本的`HEAD`指针。回退版本的时候，Git仅仅是将`HEAD`指针由指向`first commit`改为指向`second commit`，然后顺便把工作区的文件更新了，所以使`HEAD`指向哪个版本，就把当前版本定位在哪。

  

  然而如果窗口关掉了，那么再次打开Git Bash使用命令`git log`便看不到`second commit`版本的id号，自然也就无法回退版本了。此时可以用命令`git reflog`查看命令历史（记录每一次改变`HEAD`的命令），此处可以看到每次提交的版本号：

  ![image-20210124194758839](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124194758839.png)

- 总结
  1. ``HEAD``指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`

  2. 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本

  3. 要重返未来，用`git reflog`查看改变`HEAD`的命令历史，以便确定要回到未来的哪个版本

### 1.2.3 工作区和暂存区

- 工作区（Working Directory）

  即在PC中能看到的目录，比如在我桌面上的git1文件夹就是一个工作区

- 版本库/仓库（Repository）

  工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库

  Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及==指向`master`的一个指针==叫`HEAD`。分支和`HEAD`的概念以后再说

  <img src="https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/0.jpg"  />

  `git add`把文件添加进版本库，实际上就是把文件修改添加到暂存区

  `git commit`提交更改，实际上就是把暂存区的==所有内容==提交到当前分支

  因为创建Git版本库时，Git自动为我们创建了唯一1个`master`分支，所以现在`git commit`就是往`master`分支上提交更改

  可以简单理解为：需要提交的文件及修改通通放到暂存区，然后，一次性提交暂存区的所有修改

- 在`git1`目录下新建一个LICENSE文件，内容随便写；然后修改`readme.txt`文件：

  ![image-20210124213528065](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124213528065.png)

  Git非常清楚地说明了：`readme.txt`被修改了，而`LICENSE`还从来没有被添加过，所以它的状态是`Untracked`

  

  现在，使用命令`git add`，把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下：

  ![image-20210124213644358](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124213644358.png)

  现在，暂存区的状态就变成了：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124213813600.png">

  

  一旦提交后，如果又没有对工作区做任何修改，那么工作区就是“干净”的：

  ![image-20210124213813600](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/1.jpg)

  现在版本库中暂存区就没有任何内容了：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2.jpg">

- 总结

  Git的暂存区十分重要

### 1.2.4 管理修改

- Git追踪的并不是文件，而是修改

  在文件中增加一行`年轻人不讲武德。`，然后添加，然后再次修改将其句号删掉，然后提交，查看状态：

  ![image-20210124220836695](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124220836695.png)

  可以发现，第2次的修改即删除句号没有被提交

  整理一下过程：第1次修改 -> `git add` -> 第2次修改 -> `git commit`

  其实，Git管理的是修改，当用`git add`命令后，工作区的第1次修改被放入暂存区，准备提交，但是，工作区的第2次修改并没有放入暂存区。所以`git commit`只负责把暂存区的修改（即第1次的修改）提交了，第2次的修改由于没有添加进暂存区，不会被提交

  提交后，用`git diff `HEAD` -- readme.txt`命令可以查看==工作区（绿字）==与==版本库中的最新版本（红字）==之间的区别：

  ![image-20210124221534325](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124221534325.png)

  可见，第2次修改确实没有被提交

  若想提交第2次修改，则只需将其添加，然后再提交即可：

  ![image-20210124222059271](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124222059271.png)

  可以看到，添加再提交后，工作区与版本库之间没有区别，所以用`git diff `HEAD` -- readme.txt`命令时没有显示（Unix的哲学即为“没有消息就是好消息”）

- 总结

  每次修改文件，如果不用`git add`到暂存区，那么就不会加入到`commit`中

### 1.2.5 撤销修改

- 工作区改乱了文件的内容（修改如下），但是修改之后的文件没有添加到暂存区

  ![image-20210124225508963](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124225508963.png)

  若想直接丢弃工作区的修改，可以通过编辑文件手动修改，也可通过命令`git checkout -- file`

  ![image-20210124224317826](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124224317826.png)

  命令`git checkout -- readme.txt`把`readme.txt`文件在工作区的修改全部撤销，这里有两种情况：

  - `readme.txt`修改后没有添加到暂存区，此时，撤销修改就回到和版本库一模一样的状态

  - `readme.txt`添加到了暂存区，工作区的文件又做了修改，此时，撤销修改就回到添加到暂存区后的状态

  总之，命令`git checkout -- readme.txt`将使这个文件回退到最近一次`git commit`或`git add`时的状态

  此外，`git checkout -- readme.txt`命令中的`--`很重要，没有`--`，就变成了“切换到另一个分支”的命令。此处不深究，分支管理中再细说

- 工作区改乱了文件的内容（修改如下），而且修改之后的文件还添加到了暂存区中

  ![image-20210124225410528](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124225410528.png)

  若想直接丢弃暂存区，也可通过命令`git reset `HEAD` readme.txt`把暂存区的修改撤销掉（unstage），重新放回工作区，然后重复第一步即可

  ![image-20210124230438521](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124232241633.png)

  `git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区，当使用`HEAD`时，表示最新的版本

- 已经将修改提交到版本库时，想要撤销本次提交，只能通过版本回退来修改版本（不过前提是没有推送到远程库）

- 总结

  1. 场景1：当改乱工作区某个文件的内容，但没有添加到暂存区时，想要直接丢弃工作区的修改时，用命令`git chekout -- file`

  2. 场景2：当不但改乱了工作区某个文件的内容，而且添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset `HEAD` <file>`，就回到了场景1，第二步按场景1操作

  3. 场景3：已经将修改提交到版本库时，想要撤销本次提交，只能通过版本回退来修改版本（不过前提是没有推送到远程库）

### 1.2.6 删除文件

- 首先，新建一个文本文件`test.txt`，内容随意，提交。一般是通过命令`rm test.txt`删除该文件。此时Git知道该文件已经删除了，故而工作区和版本库的文件就不一致了，`git status`命令会立刻告诉哪些文件被删除了

- ![image-20210124231804631](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124231804631.png)

  现在有两个选择：

  - 要从版本库中删除该文件，那就用命令`git rm`删掉（与用`git add`效果一样），并且提交

    ![image-20210124232241633](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125101015857.png)

    这样文件从版本库中删除了

    如果直接用`git rm test.txt`删除文件而不用`rm test.txt`，那么该文件是无法恢复的。总之一句话：`git rm`命令直接从版本库中删除文件

  - 删错了，因为版本库中还有，所以可以很轻松地把误删的文件恢复到最新版本

    ![image-20210124232846497](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124230438521.png)

    `git checkout -- test.txt`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”

    

    注意：没有被添加（`git add`）到版本库的文件，删除之后是无法恢复的！换言之，添加（`git add`）后的文件删除（非`git rm`）之后是可以恢复的


### 1.3 远程仓库

### 1.3.1 关联PC主机与GitHub服务器

实际情况往往是这样，找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交

完全可以自己搭建一台运行Git的服务器，不过现阶段，为了学Git先搭个服务器绝对是小题大作。好在这个世界上有个叫GitHub神奇的网站，从名字就可以看出，这个网站就是提供Git仓库托管服务的。所以，只要注册一个GitHub账号，就可以免费获得Git远程仓库

由于Git仓库与GitHub仓库之间的传输是通过SSH加密的，所以需要进行一些设置：

1. 创建SSH Key。在用户主目录下（C:\Users\29239），看看有没有`.ssh`目录。如果有，再看看有没有`id_rsa`和`id_rsa.pub`这两个文件，如果有，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），输入如下命令创建SSH Key：

   ```
   ssh-keygen -t rsa -C "youremail@example.com"
   ```

   输入邮箱后，直接一路回车。如果一切顺利，可以在用户主目录里找到`.ssh`目录。里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人

   ![image-20210125101015857](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210124232846497.png)

2. 登录GitHub，打开“Account settings”，“SSH Keys”页面。然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容。点“Add Key”，你就应该看到已经添加的Key：

   ![image-20210125101217562](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125101217562.png)

   当然，GitHub允许添加多个Key。假定有若干电脑，一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了

   注意：在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去

   如果不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是自己的Git服务器，所以别人也是看不见的

### 1.3.2 添加远程库

现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，一举多得

- 首先，登录GitHub，然后点击左上角repository的new按钮，创建一个新的仓库。然后在Repository name填入`git1`，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：

  ![image-20210125102159633](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125104426601.png)

  ![image-20210125102513346](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125102159633.png)

  目前，GitHub上的这个`git1`仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以==把一个已有的本地仓库与之关联==，然后，把本地仓库的内容推送到GitHub仓库

  现在，根据GitHub的提示，在本地的`git1`仓库下运行命令：

  ```
  git remote add origin git@github.com:zhenyoung6/git1.git
  ```

  添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库

  下一步，就可以把本地库的所有内容推送到远程库上：

  ```
  git push -u origin master
  ```

  把本地库的内容推送到远程，用`git push`命令，实际上是==把当前分支`master`推送到远程==

  ![image-20210125104426601](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125105819675.png)

  由于远程库是空的，第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送到远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令

  推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：

  ![image-20210125104059199](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125102513346.png)

  此后，只要本地作了提交，就可以通过命令：

  ```
  git push origin master
  ```

  把本地`master`分支的最新修改推送到GitHub

- 总结

  1. 要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`

  2. 关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容

     此后，每次本地提交后，可以使用命令`git push origin master`推送最新修改

  3. 分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！而Git在有网络的时候，再把本地提交推送一下就完成了同步

### 1.3.3 从远程库克隆

上节中讲了先有本地库，后有远程库的时候，如何关联远程库。现在，假设从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆

- 首先，登陆GitHub，创建一个新的仓库，名字叫`gitskills`：

  现在，远程库已经准备好了，下一步是用命令`git clone`在`desktop`目录下克隆一个本地库：

  ![image-20210125105819675](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/1.png)

  如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了

  此外我们注意到，GitHub给出的地址不止一个，还可以用`https://github.com/zhenyoung6/gitskills.git`这样的地址

  ![image-20210125110223367](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/2.png)

  实际上，Git支持多种协议，默认的`git://`使用ssh，但也可以使用`https`等其他协议。使用`https`除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`

- 总结

  1. 要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆

  2. Git支持多种协议，包括`https`，但`ssh`协议速度最快

## 1.4 分支管理

### 1.4.1 创建与合并分支

- 在版本回退中，已经了解到：每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫做主分支，即`master`分支。==`HEAD`严格来说不是指向提交，而是指向`master`==，`master`才是指向提交的。所以，`HEAD`指向的就是当前分支

  一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/3.png">

  每次提交，`master`分支都会向前移动一步，这样，随着不断提交，`master`分支的线也越来越长

  当创建新的分支如`dev`时，Git新建了一个指针叫`dev`，指向与`master`相同的提交，再将`HEAD`改为指向`dev`，就表示当前分支在`dev`上：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125104059199.png">

  Git创建一个分支很快，因为除了增加一个`dev`指针，更改`HEAD`的指向，工作区的文件都没有任何变化！

  不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/5.png">

  假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。合并最简单的方法，就是将`master`指向==`dev`的当前提交==，就完成了合并：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/4.png">

  所以Git合并分支也很快！更改指针即可，工作区内容也不变！

  合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125110223367.png">

- 下面举一个例子

  首先，创建`dev`分支，然后切换到`dev`分支：

  ```
  git checkout -b dev
  ```

  `git checkout`命令加上`-b`参数表示创建并切换，相当于两条命令：

  ```
  git branch dev
  git checkout dev
  ```

  然后，用`git branch`命令查看当前分支：

  ![image-20210125225049612](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125225049612.png)

  `git branch`命令会列出所有分支，当前分支前会标一个`*`号

  然后，就可以在`dev`分支上正常提交，比如对`readme.txt`做修改，加上一行：

  ```
  Creating a new branch is quick.
  ```

  然后提交，之后切换回`master`分支：

  ```
  git checkout master
  ```

  切换回`master`分支后，再查看`readme.txt`文件：

  ![image-20210125225618044](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/6.png)

  刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交并没有改变：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125230121019.png">

  现在，将`dev`分支的工作成果合并到`master`分支上：

  ```
  git merge dev
  ```

  `git merge`命令用于合并指定分支到当前分支。合并后，再查看`readme.txt`的内容：

  ![image-20210125230121019](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125230531420.png)

  可以看到，和`dev`分支的最新提交是完全一样的

  注意到上面的`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快

  当然，也不是每次合并都能`Fast-forward`，此处先按下不表，后面再提

  合并完成后，就可以放心地删除`dev`分支了：

  ```
  git branch -d dev
  ```

  删除后，查看`branch`，就只剩下`master`分支了：

  ![image-20210125230531420](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125233813834.png)

  ==因为创建、合并和删除分支非常快，所以Git鼓励使用分支完成某个任务，合并后再删掉分支，这与直接在`master`分支上工作效果是一样的，但过程更安全==

- 最新Git支持的`switch`命令

  我们注意到切换分支使用`git checkout <branch>`，而前面讲过的撤销修改则是`git checkout -- <file>`。同一个命令，有两种作用，容易搞混且难以区分记忆

  实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支

  创建并切换到新的`dev`分支，可以使用：

  ```
  git switch -c dev
  ```

  直接切换到已有的`master`分支，可以使用：

  ```
  git switch master
  ```

  使用新的`git switch`命令，比`git checkout`要更容易理解

  ![image-20210125233813834](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210125225618044.png)

- 总结

  Git鼓励大量使用分支：

  1. 查看分支：`git branch`
  2. 创建分支：`git branch <name>`
  3. 切换分支：`git checkout <name>`
  4. 创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`
  5. 合并某分支到当前分支：`git merge <name>`
  6. 删除分支：`git branch -d <name>`

### 1.4.2 解决冲突

- 以下面一个例子说明冲突及如何解决冲突

  创建新的分支：`git switch -c feature1`

  修改`readme.txt`最后一行，改为：

  ```
  Crreating a new branch is quick AND simple.
  ```

  然后在`feature1`分支上提交，然后切换到`master`分支：

  ![image-20210126003723275](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126003723275.png)

  `Your branch is ahead of 'origin/master' by 1 commit.`提示我们：当前`master`分支比远程的`master`分支要超前1个提交

  在`master`分支上把`readme.txt`文件的最后一行改为：

  ```
  Creating a new branch is quick & simple.
  ```

  然后在`master`分支上提交：

  ![image-20210126004422409](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/branch1.png)

  现在，`master`分支和`feature1`分支各自都分别有新的提交，变成了这样：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126004422409.png">

  

  此时，Git无法执行“快速合并”，只能试图把各自的修改合并起来，若执行合并命令：

  ![image-20210126005635204](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126005635204.png)

  可以发现：合并出现冲突且冲突出现在`readme.txt`文件中，必须解决冲突后提交

  `git status`也说明了冲突的文件：

  ![image-20210126010007855](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126010007855.png)

  查看`readme.txt`的内容：

  ![image-20210126010235214](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/branch2.png)

  Git中使用`<<<<<<<`，`=======`，`>>>>>>>`标记出分支之间相异的内容

  将`“年轻人不讲武德”`一句后修改为一行：

  ```
  Creating a new branch is quick and simple.
  ```

  提交之后，`master`分支和`feature1`分支变成了下图所示：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126010748786.png">

  用带参数的`git log`也可以看到分支的合并情况：

  ![image-20210126010748786](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126010235214.png)

- 总结

  当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成

  而解决冲突就是把Git合并失败的多份文件手动编辑为我们希望的内容，再提交

  用`git log --graph`命令可以看到分支合并图

### 1.4.3 分支管理策略

通常，合并分支时，如果可能，Git会用`Fast forward`模式，但这种模式下，删除分支后，会丢掉分支信息

如果要强制禁用`Fast forward`模式，Git就会在merge合并时生成一个新的commit提交，这样，从分支历史上就可以看出分支信息。

- 下面举一个例子说明一下分支管理

  首先，仍然创建并切换`dev`分支，修改`readme.txt`文件，并提交一个新的`commit`，然后切换回`master`。然后输入以下命令合并`dev`分支：

  ```
  git merge --no-ff -m "merge with no-ff" dev
  ```

  `--no-ff`参数，表示禁用`Fast forward`

  因为本次合并要创建一个新的`commit`，所以要加上`-m`参数，把`commit`描述写进去

  合并后，用`git log`查看分支历史：

  ![image-20210126013421958](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/fast forward1.png)

  可以看到，不使用`Fast forward`模式，`merge`后就像这样：

<img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126013421958.png">

- 分支策略

  在实际开发中，我们应该按照几个基本原则进行分支管理：

  首先，`master`分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

  那在哪干活呢？干活都在`dev`分支上，也就是说，`dev`分支是不稳定的，到某个时候，比如1.0版本发布时，再把`dev`分支合并到`master`上，在`master`分支发布1.0版本；

  你和你的小伙伴们每个人都在`dev`分支上干活，每个人都有自己的分支，时不时地往`dev`分支上合并就可以了。

  所以，团队合作的分支看起来就像这样：

  <img src = "https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/fast forward.png">

- 总结

  合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并

### 1.4.4 Bug分支

### 1.4.5 Feature分支

### 1.4.6 多人协作

### 1.4.7 Rebase

## 1.5 标签管理

标签`tag`就是一个让人容易记住的有意义的名字，它跟某个`commit`绑在一起。可以理解为：每个tag就对应着1个版本的`commit`

- 创建标签

  首先，切换到需要打标签的分支上。然后，用命令`git tag <name>`就可以打一个新标签。可以用命令`git tag`查看所有标签：

  ![image-20210126152723642](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126154130846.png)

  默认标签是打在最新提交的`commit`上的。有时候，如果忘了打标签，比如，现在已经是周五了，但本应该在周一打的标签没有打，怎么办？

  方法是找到历史提交的commit id，然后打上就可以了：

  ![image-20210126153713606](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126154211177.png)

  若要对最近的`conflict fixed`这次提交打标签，它对应的commit id是`5c03c59`，用命令`git tag v0.9 5c03c59`，然后再用`git tag`查看标签

  ![image-20210126154130846](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126152723642.png)

  注意，标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息

  ![image-20210126154211177](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126154444485.png)

  可以看到，`v0.9`确实打在`conflict fixed`这次提交上

  还可以创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字：

  ```
  git tag -a v0.1 -m "version 0.1 released" d22cb3a
  ```

  用命令`git show <tagname>`可以看到说明文字：

  ![image-20210126154444485](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126153713606.png)

  注意：标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

- 操作标签

  如果标签打`v0.1`错了，也可以用命令`git tag -d v0.1`删除。因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除

  如果要推送某个标签到远程，使用命令`git push origin v0.1`

  或者，一次性推送全部尚未推送到远程的本地标签`git push origin --tags`

  ![image-20210126160150241](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126160958026.png)

  如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除`git tag -d v0.9`。然后，从远程删除`git push origin :refs/tags/v0.9`

  ![image-20210126161432619](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126160150241.png)

  若要查看是否真的从远程库删除了标签，可以登陆GitHub查看是否真的从远程库删除了标签

  以下删除了v0.9，还剩v1.0和v0.1版本

  ![image-20210126160925273](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126160925273.png)

  

  以下删除了v0.1，还剩v1.0版本

  ![image-20210126160958026](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126161128493.png)

  

  以下删除了最后的v1.0版本

  ![image-20210126161128493](https://pic-blogs.oss-cn-beijing.aliyuncs.com/img/image-20210126161432619.png)



- 总结

  1. 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id

  2. 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息
  3. 命令`git tag`可以查看所有标签
  4. 命令`git push origin <tagname>`可以推送一个本地标签
  5. 命令`git push origin --tags`可以推送全部未推送过的本地标签
  6. 命令`git tag -d <tagname>`可以删除一个本地标签
  7. 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签

## 1.6 使用GitHub

## 1.7 使用Gitee

## 1.6 自定义Git

### 1.6.1 使用SourceTree

# 2. GitHub
