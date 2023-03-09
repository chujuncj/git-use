# Git的使用

**Notes by :** chu-jun
**Learn from :** <https://www.bilibili.com/video/BV1vy4y1s7k6/>
**Blog :** <https://www.cnblogs.com/manmc/>
**Motto :** 择善修身，立学济世。

## 一、Git概述

> Git是一个免费的、开源的分布式版本控制系统，可以快速高效地处理从小型到大型的各种项目。
>
> Git 易于学习，占地面积小，性能极快。它具有廉价的本地库，方便的暂存区域和多个工作流分支等特性。其性能优于Subversion、CVS、Perforce和 ClearCase**等版本控制工具**。

### 1.1何为版本控制

> 版本控制是一种记录文件内容变化，**以便将来查阅特定版本修订情况的系统**。版本控制其实最重要的是可以记录文件修改历史记录，从而让用户能够查看历史版本,方便版本切换。

### 1.2为什么需要版本控制

> 个人开发过渡到团队协作。
>
> 如下图，红蓝两人同时将服务器中 1 版本下载到了本地进行改动，如果不借用版本控制工具，还利用多副本的情况下，蓝的修改文件很容易覆盖红修改的文件，在公司团队协作中这种操作显然是不靠谱的。这时就需要专业的版本控制工具（Git）合并两个人的修改文件。

![1678191415719](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202212521-1119102061.png)

### 1.3版本控制工具

- **集中式版本控制工具**

> 集中化的版本控制系统诸如CVs、SVN等，都有一个单一的**集中管理的服务器**，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。

![1677749419805](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202213075-2110529366.png)

**优点：**

> 多年以来，这已成为版本控制系统的标准做法。
> 这种做法带来了许多好处,每个人都可以在一定程度上看到项目中的其他人正在做些什么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个集中化的版本控制系统，要远比在各个客户端上维护本地数据库来得轻松容易。

**缺点：**

> 事分两面，有好有坏。这么做显而易见的缺点是中央服务器的单点故障。如果服务器宕机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作。

- **分布式版本控制工具**

> 像Git这种分布式版本控制工具，客户端提取的不是最新版本的文件快照，而是把代码仓库完整地镜像下来（本地库)。这样任何一处协同工作用的文件发生故障，事后都可以用其他客户端的本地仓库进行恢复。因为每个客户端的每一次文件提取操作，实际上都是一次对整个文件仓库的完整备份。

**分布式的版本控制系统出现之后,解决了集中式版本控制系统的缺陷:**

> 1.服务器断网的情况下也可以进行开发（因为版本控制是在本地进行的)
>
> 2.每个客户端保存的也都是整个完整的项目(包含历史记录，更加安全)

### 1.4 Git简史

![1677750566800](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202213598-291687948.png)

### 1.5 Git工作机制

![1](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202213942-1582860353.png)

> 工作区：存放代码的位置
>
> 暂存区：将工作区的代码添加到暂存区，临时存储可以删除
>
> 本地库：将暂存区的代码提交到本地库，一旦提交到本地库就会生成历史版本，就无法删除了

### 1.6 Git和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般我们简单称为**远程库**。

**局域网：**

- GitLabe

**互联网：**

- GitHub(外网）

- Gitee码云（国内网站)

## 二、Git安装

- 双击安装文件（傻瓜式安装，下一步）

  ![2](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202214398-64429721.png)

> 这里要注意，最好选择非系统盘，目录不是中文且不带空格

![3](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202214727-1935353741.png)

> 这里默认的第二个，我们选择第一个

![4](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202215096-1885861533.png)

> 没有说明的地方都是下一步，安装完成之后，鼠标哟及桌面出现如下图的Git Bash Here就成功了

![5](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202215442-909488345.png)

## 三、Git常用命令

![6](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202215733-1634486455.png)

### 3.1  设置用户签名

```shell
# 设置用户签名
git config --global user.name 用户名
# 设置邮箱，这里可以是虚假的
git config --global user.email  邮箱名

# 查看设置是否成功
cat ~/.gitconfig
## 或者时打开C盘用户里面的.gitconfig文件查看
```

**说明**:

> 签名的作用是区分不同操作者身份。用户的签名信息在每一个版本的提交信息中能够看到，以此确认本次提交是谁做的。
>
> Git首次安装必须设置一下用户签名，否则无法提交代码。
>

**※注意:**这里设置用户签名和将来登录GitHub(或其他代码托管中心）的账号没有任何关系。

### 3.2  初始化本地库

> 在需要git的文件夹里右击，选择Git Bash Here,输入初始化命令，如果初始化成功，可以在文件夹里看到一个.gitconfig文件，如果看不到，点击查看，勾选隐藏文件。

```shell
# 初始化本地库
git init
```

### 3.3 查看本地库状态

```shell
# 查看本地库状态
git status  # 若文件夹为空，会提示无文件提交

# 新建文件
vim hello.txt
git status # 此时再查看本地库状态，会显示hello.txx为红色，没有提交
```

### 3.4 添加暂存区

```shell
# 添加暂存区
git add hello.txt

# 查看本地库状态
git status # 会显示hello.txt为绿色

# 注意：
# 在暂存区的文件可以删除，而且不会影响本地的文件
# 删除暂存区文件
git rm --cached hello.txt 
# git status 此时再查看hello.txt又变为红色，因为，暂存区的文件删除了，且ll命令查看，本地文件依然在

# 再次添加暂存区
git add hello.txt
```

### 3.5 提交本地库

```shell
# 将暂存区文件提交到本地库
# "日志信息" 可以不写，但后面还是会弹出让我们填写，所以这里可以直接加上，主要是描述此次提交本地库修改的内容，或是次数，类似打个标签。
git commit -m "日志信息" 文件名 

git commit -m "first commit" hello.txt

# 查看本地库状态
git status 
# 此时不会再提示hello.txt文件，而是提示nothing to ommit
```

### 3.6 查看历史版本库

```shell
# 查看历史版本库
git reflog
# 不仅查看历史本地库，还可以查看是谁提交的
git log
```

### 3.7 版本穿梭

> 如果不满意当前版本修改的内容，想查看之前的版本，需要版本穿梭

```shell
# 首先根据git reflog 查看历史版本地库，找到需要穿梭的版本的版本号，复制一下
$ git reflog
# 输出：
2424376 (HEAD -> master) HEAD@{0}: commit: second commit
70edd43 HEAD@{1}: commit (initial): first commit


# 穿梭版本命令
git reset --hard 70edd43 
# 输出：HEAD指向
HEAD is now at 70edd43 first commit

```

## 四、Git分支操作

![1677830161420](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307201103693-827540077.png)

### 4.1 什么是分支

> 在版本控制过程中，**同时推进多个任务**，为每个任务，我们就可以**创建每个任务的单独分支**。使用分支意味着程序员可以把自己的工作从开发主线上**分离开来**，开发自己分支的时候，不会影响主线分支的运行。对于初学者而言，分支可以简单理解为副本，一个分支就是一个单独的副本。(分支底层其实也是**指针的引用**)

![1677830632785](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307201104174-356620713.png)

### 4.2 分支的好处

> 同时并行推进多个功能开发，提高开发效率。各个分支在开发过程中，如果某一个
>
> 分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。

### 4.3 分支的操作

#### 4.3.1 查看分区

```shell
# 查看分区
git branch -v
# * master 70edd43 first commit (*代表当前所在的分区)

```

#### 4.3.2 创建分区

```shell
# 创建分支
git branch 分支名
git branch hot-fix
# 结果
  hot-fix 70edd43 first commit(创建的新分支，并将分支master的内容复制了一份)
* master  70edd43 first commit
# 4、把指定的分支合并到当前分支上
git merge 分支名
```

#### 4.3.3 切换分支

```shell
# 切换分支
git checkout 分支名
git checkout hot-fix
# 查看分区
git branch -v

# 结果
* hot-fix 70edd43 first commit (*在hot-fix上，代表当前分支为hot-fix)
  master  70edd43 first commit
 
```

#### 4.3.4 修改分支

```shell
# 修改代码
vim hello.txt
# 添加暂存区
git add hello.txt
# 提交本地库
git commit -m "hot-fix first commit" hello.txt
```

#### 4.3.5 合并分支

- 正常情况合并分支，master分支没有改动，将hot-fix分支合并

```shell
# 如果想将hot-fix修改的hello.txt合并到master分支下，首先要先进入master分支下
git checkout master
# 虽然hot-fix分支下的hello.txt修改并提交了，但是master分支下的hello.txt并没有收到影响，所以要进行合并。

# 合并分支
git merge hot-fix
```

- 冲突合并

> 冲突产生的原因：合并分支时，两个分支在**同一个文件的同一个位置有两套完全不同的修改。**Git无法替我们决定使用哪一个。必须人为决定新代码内容。以查看状态（检测到有文件有两处修改)

```shell
# 案例：
# 在master分支下修改
vim hello.txt # (修改一处)
# 添加暂存区
git add hello.txt
#提交本地库
git commit -m "master test hello.txt" hello.txt

# 在hot-fix分支下修改
git checkout hot-fix
vim hello.txt # (修改一处)
# 添加暂存区
git add hello.txt
#提交本地库
git commit -m "hot-fix test hello.txt" hello.txt
###这个时候两个分支下同一个文件都进行了修改####
git checkout master
git merge hot-fix # 合并分支就会出现错误

# 解决冲突
# 手动解决冲突
# 在mster分支下修改
vim hello.txt # 会发现两处修改的位置，手动修改决定如何保留，修改后保存，再添加暂存区，提交本地
# 添加暂存区
git add hello.txt
#提交本地库(这个时候就不带文件名)
git commit -m "merge hot-fix " 

# 查看手动合并分支内容
cat hello.txt
```

> master、hot-fix其实都是指向具体版本记录的指针。当前所在的分支，其实是由HEAD决定的。
>
> 所以创建分支的本质就是多创建一个指针。HEAD 如果指向master，那么我们现在就在master分支上。HEAD如果执行hot-fix，那么我们现在就在 hotfix 分支上。
>
> 所以切换分支的本质就是移动HEAD指针。

## 五、Git团队协作机制

> 需要用到代码托管中心

### 5.1  团队内协作

![8](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307202216471-312732946.png)

### 5.2  跨团队协作

![1678191359556](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307201628794-832415760.png)

## 六、GitHub操作

GitHub 网址: <https://github.com/>

### 6.1 创建远程库

![1678102133084](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307201104986-1673306008.png)

![1678102386529](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307201105367-526709275.png)

生成远程库的链接**：

<https://github.com/chujuncj/git-demo.git>

### 6.2 远程仓库操作

#### 6.2.1创建远程库别名

```shell
# 起别名的原因：上面获得的远程库链接太长了，以后推送远程库不方便，起别名会跟便于操作

# 查看当前所有远程地址别名
git remote -v

# 起别名
git remote add 别名 远程地址
```

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307203343189-2139430538.png)
> 这里回生成两个别名，一个是推送或者pull用的还有一个是push

#### 6.2.2 推送本地分支到远程库

```shell
# 推送
git push 别名 分支
```

- 输入推送命令后，会出现如下页面，如果是已经打开的直接跳到第四张图
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307204105469-353456796.png)
- 登录
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307204146977-2086453047.png)
- 授权
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307204322385-1919412730.png)
- 成功
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307204334330-1113328797.png)
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307212703368-228691254.png)

**注意：**
> 因为github是外网，访问会很慢，甚至会报错，不用担心，反复访问，或者翻墙，在这个过程中注意可能会让你输入用户名和密码

#### 6.2.3 拉取远程库

```shell
# 推送
git pull 别名 分支
```

#### 6.2.4 克隆远程仓库到本地

```shell
# 克隆
git clone https://github.com/chujuncj/git-demo.git # 需要克隆的地址
```

小结:
  clone会做如下操作。
  1、拉取代码。
  2、初始化本地仓库。
  3、创建别名（自动生成一个别名）

#### 6.2.5 邀请加入团队

**1、添加伙伴。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307215536571-239651672.png)

**2、输入伙伴信息。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307215801018-1682196428.png)

**3、复制邀请函（链接地址）。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307215944136-919131726.png)

**4、被邀请的伙伴复制邀请函在自己的GitHub中打开，并确认。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230307220321418-152441282.png)

**5、确认之后，被邀请的伙伴就可以在自己的GitHub看到邀请人的远程库，并且可以推送、拉取等。**

### 6.3 跨团队协作

**1、将远程库地址链接发给跨团队的人K，K将地址链接复制在GitHub中打开就可以看到远程库了。**

**2、作为团队队外的人K，想要队项目进行修改。首先fork远程库。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308092632827-513614244.png)

**3、此时在K的远程库中可以看到此项目。K可以克隆到本地进行修改，也可以在线进行修改。**

**4、提交修改。此时的修改提交只是提交到了K自己的库中，在别人的团队中是看不到修改的。**

**5、拉去请求。Pull requests.**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308093218608-2050226938.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308093335676-2156090.png)

**6、创建拉去请求，同时在下方可以看到修改的内容。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308093514016-635256632.png)

**7、写备注、添加评论。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308093837557-1893349648.png)

**8、团队管理人打开远程库，会发现一个拉取请求。点开查看，可以看到是谁修改了代码以及代码修改的内容。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308094139249-335201426.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308094238919-1871283865.png)

**9、如有疑问可以和跨团队协作人K回话、添加评论。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308094552237-916622817.png)

**10、如果对K修改的内容满意，可以提出合并拉取请求。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308094933501-520499395.png)

**11、确认合并。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308095015930-47184466.png)

**12、合并之后在团队内就可以看到K修改的内容，并且团队成员可以克隆或在线修改，或学习。**

### 6.4 SSH 免密登录

> 我们可以看到远程仓库中还有一个 SSH 的地址，因此我们也可以使用 SSH 进行访问。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308095525252-1889503610.png)

**1、在家目录下右击打开git bash here。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308095813109-624489399.png)

**2、非加密协议算法，生成.ssh密钥目录。**

```shell
# ssh-keygen:生成公钥和私钥的命令
# -t : 指定用哪种加密算法
# rsa : 非对称加密协议
# -C : 描述
ssh-keygen -t rsa -C chummyj@qq.com
```

**3、输入命令后敲三次回车。回到家目录就可以看到.ssh文件。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308100555163-1746045636.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308100845527-1031504846.png)

**4、复制公钥。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308101232199-1510034664.png)

**5、配置。**
> setting ---> SSH and GPG keys ----> New SSH keys ---> 添加公钥

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308102314867-813715956.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308102341536-1895964804.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308102403063-740391985.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308102549478-1499618376.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308102625825-1446356327.png)

**6、配置成功。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308102729780-258361577.png)

**7、测试。**
> 复制SSH生成的远程库地址链接 ---> 在本地库右击打开git bash here ---> 拉取git pull SSH远程库地址链接

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308103321061-1394192708.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308103505923-1641811370.png)

## 七、IDEA集成Git

### 7.1 配置git 忽略文件

> 不想要这些特定文件（.idea .iml .... ）

**1、Eclipse 特定文件。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308104318169-1211600622.png)

**2、IDEA特定文件。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308104409991-186318816.png)

**3、Maven工程的target.**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308104713715-951349013.png)

**问题 1:为什么要忽略他们?**
> 答:与项目的实际功能无关，不参与服务器上部署运行。把它们忽略掉**能够屏蔽IDE 工具之间的差异。**

**问题 2: 怎么忽略?**
> 创建忽略规则文件 xxxxignore (前缀名随便起，建议是 **git.ignore**)这个文件的存放位置原则上在哪里都可以，为了便于让~.gitconfig 文件引用，建议也放在用户家目录下。

**4、文件的内容怎么写：想忽略什么文件就将其后缀写在文件里。**
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308105456869-1088164469.png)

```shell
# Compiled class file
*.class
# Log file
*.log
# BlueJ files
*.ctxt
# Mobile Tools for Java (J2ME)
.mtj.tmp/# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar
hs_err_pid*
.classpath
.project
.settings
target
.idea
*.iml
```

**5、在.igtconfig文件中引用忽略配置文件（此文件在Windows家目录下）。**

```shell
[core]
    excludesfile = C:/Users/cj/git.ignore
# note: 这里要使用“正斜线（/）”，不要使用“反斜线（\）”
```

### 7.2 定位Git程序

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308110507402-104001472.png)

### 7.3 初始化本地库

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308111405311-1699531050.png)

### 7.4 添加到暂存区

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308111708993-2000844564.png)

**添加了代码后，可以将整个项目都添加到暂存区。**
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308112258963-348531765.png)

**这时候会有一个提示，问是否要强制添加忽略文件，点击取消。**
![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308112416433-1502985450.png)

### 7.5 提交到本地库

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308112753749-1220743941.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308112942209-1851257114.png)

- 有时候提交本地库会提示有警告，不要管他，继续提交。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308131703291-1815075345.png)

### 7.6 切换版本

> 在IDEA的左下角，点击Version Control（如果没有，在左下角会有一个git,点击它）,然后点击Log查看版本，在此之前对代码进行修改，重复7.4-7.5多提交几次。

**1、版本查看。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308132306552-1232071551.png)

> 注意看上图中有两个颜色的指针，右下角解释，绿色的是分支的指针，黄色是版本的指针，当前是mater分支第四次提交的版本。

**2、切换版本。**

> 直接选择要切换的版本，右击选择checkout revision ....

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308132543824-465456314.png)

> 切换完成后，会发现版本指针发生了改变，指向了切换的版本；其次代码也切换回了版本对应的代码。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308132858905-1511489108.png)

### 7.7 创建分支

> 方法一：右击项目名称 ---> Git ---> Repository ---> Branches... ---> New Branches
> 方法二：点击IEDA右下角Git:master ---> New Branches

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308133712614-633392526.png)

### 7.8 切换分支

> 点击右下角hot-fix选择master ---> Checkout

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308133952985-1898826082.png)

### 7.9 合并分支

**1、正常合并。**

> 在IDEA窗口的右下角，将hot-fix分支合并到当前master分支。在此之前在hot-fix分支下对代码进行修改，并提交，然后切换到master分支下。点击右下角master选择hot-fix分支，点击Merge 'hot-fix' into 'master'.

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308135259630-596242077.png)

> 如果代码没有冲突，分支合并成功，分支合并成功以后，代码自动提交，无需手动提交到本地库

**2、解决代码合并冲突。**

> 解决冲突之前先制造冲突，在master分支和hot-fix下同时修改一个代码。并回到master分支下合并。点击右下角master选择hot-fix分支，点击Merge 'hot-fix' into 'master'.

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308141158951-1842655803.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308141851568-1430937901.png)

> 日志信息，合并成功

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308141950867-1772311090.png)

## 八、IDEA集成GitHub

### 8.1 设置GIthub账号

> File ---> settings ---> Version Control ---> GitHub ---> 添加账号（有的可以直接添加账号密码，这种方式很慢）我这里不能直接添加，点击Generate到GitHub上生成一个口令，将口令复制在Token中即可。
> 如果没有GitHub 在File ---> settings --->Plugins中下载一个

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308142811330-788610103.png)

> 生成口令方法二：登录GitHub点击头像，选择settings(拉到最下面) ---> 点击Developer settings ---> Personal access tokens ---> Tokens (classic) ---> Generate new token

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308143811135-1068738333.png)

> 口令生成的时候有权限选择，全部都勾上，点击生成，出现如下图口令，复制，回到IEDA粘贴

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308144144078-1018037023.png)

### 8.2 分享项目到Github

> 通常情况下我们需要在GitHub上创建一个远程库，再进行上传。但这里，由于上面8.1中IDEA和GitHub已经绑定，可以直接上传。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308145526933-143733359.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308145925024-1661296050.png)

#### 8.3 push推送本地库到远程库

> Git ---> Push

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308192559317-960676568.png)

> ssh免密push：在GitHub里复制ssh的远程库地址链接，将其复制到URL。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308192633220-2005176043.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308193058714-386124449.png)

> 注意: push 是将本地库代码推送到远程库，如果本地库代码跟远程库代码版本不一致，push 的操作是会被拒绝的。也就是说，要想 push 成功，一定要保证本地库的版本要比远程库的版本高! 因此一个成熟的程序员在动手改本地代码之前，一定会先检查下远程库跟本地代码的区别! 如果本地的代码版本已经落后，切记要先 pull 拉取一下远程库的代码，将本地代码更新到最新以后，然后再修改，提交，推送!

#### 8.4 pull拉取远程库到本地库

> 注意: pull 是拉取远端仓库代码到本地，如果远程库代码和本地库代码不一致，会自动合并，如果自动合并失败，还会涉及到手动解决冲突的问题。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308193953637-900649530.png)

> 选择免密登录。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308194103245-320759308.png)

#### 8.5 clone克隆远程库到本地库

> URL链接可以用ssh免密登录链接

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308212055025-1286653274.png)

## 九、国内代码托管中心-码云

### 9.1 简介

> 众所周知，GitHub 服务器在国外,使用 GtHub 作为项目托管网站,如果网速不好的话严重影响使用体验，甚至会出现登录不上的情况。针对这个情况，大家也可以使用国内的项目托管网站-码云。
> 码云是开源中国推出的基于 Git 的代码托管服务中心，网址是 <https://gitee.com/> ，**使用方式跟 GitHub 一样**，而且它还是一个中文网站，如果你英文不是很好它是最好的选择。

### 9.2 码云账号注册和登录

> 进入码云官网地址: <https://gitee.com/> 点击注册 Gitee

**1、注册账号。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308212657222-1778866260.png)

> 姓名、空间地址、邮箱、密码

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308212733974-1518791031.png)

### 9.3 码云创建远程库

> 点击首页右上角的加号，选择下面的新建仓库。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308213126160-1647347380.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308213422055-247492167.png)

> 创建成功，这里有HTTPS和SSH，这里推荐用HTTPS，因为码云是国内的，基本不会因为网络延迟出现问题，如果想设置SSH免密，同上述GitHub配置过程相同。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308213711697-2147064941.png)

### 9.4 IDEA集成码云

#### 9.4.1 IDEA安装码云插件

> IDEA 默认不带码云插件，我们第一步要安装 Gitee 插件。“如图所示，在Idea 插件商店搜索 Gitee，然后点击右侧的 Install 按钮。
> File ---> settings ---> Plugins
> 下载完成后重启，在File ---> settings --->Version Control 里面就可以看到Gitee

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308214711048-725045273.png)

#### 9.4.2 IDEA链接码云

> IDEA登录码云

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308215216050-1736438940.png)

> 1、分享本地项同GitHub一样

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308215804110-1353495909.png)

> 2、如果不想直接分享本地项目，而是提前在码云上建好仓库，然后复制远程仓库的链接，在IDEA中Push

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308215835427-1701587134.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308215912955-2089296528.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308220238264-1261720027.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308220212292-285092625.png)

> 注意push的时候，要选择刚刚配置的码云链接的名称，否则有可能失败

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230308220448562-1247984457.png)

> pull拉去码云远程库

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309100722776-664574985.png)

> 这里要选择码云的链接，否则会拉去错误

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309100754565-2075162412.png)

> 克隆等其他操作同GitHub中相似

### 9.5 码云复制迁移GitHub项目

> 新建仓库--->导入已有仓库--->复制GitHub仓库链接--->导入

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309103048282-364980991.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309103530800-458162845.png)

> 如果GitHub更改了，在码云上点击右边的强制更新，即可同步

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309103726744-1771768862.png)

> 批量导入：新建仓库--->导入已有仓库--->导入GitHub仓库--->导入当前所有仓库/选择导入

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309104139486-1679228935.png)

## 十、自建代码托管平台-GitLab

### 10.1 GitLab简介

>GitLab 是由 GitLabInc.开发，使用 MIT 许可证的基于网络的 Git 仓库管理工具，且具有wiki 和 issue 跟踪功能。使用 Git 作为代码管理工具，并在此基础上搭建起来的 web 服务。
> “GitLab 由乌克兰程序员 DmitriyZaporozhets 和 ValerySizov 开发，它使用 Ruby 语言写成。后来，一些部分用 Go 语言重写。截止 2018 年 5 月，该公司约有 290 名团队成员，以及 2000 多名开源贡献者。GitLab 被IBM，Sony，JulichResearchCenter，NASA，Alibaba,Invincea，OReillyMedia，Leibniz-Rechenzentrum(LRZ)，CERN，SpaceX 等组织使用。

### 10.2 GitLub 官网地址

官网地址: <https://about.gitlab.com/>
安装说明: <https://about.gitlab.com/installation/>

### 10.3 GitLub安装

#### 10.3.1 服务器准备

>准备一个系统为 CentOS7 以上版本的服务器，要求内存 4G，磁盘 50G。“关闭防火墙，并且配置好主机名和IP，保证服务器可以上网。
此教程使用虚拟机:
主机名: gitlab-server
IP 地址:192.168.6.200

#### 10.3.2 安装包准备

> Yum 在线安装 gitlab- ce 时，需要下载几百MB的安装文件，非常耗时，所以最好提前把所需RPM包下载到本地，然后使用离线rpm的方式安装。

**下载地址:**
> <https://packages.gitlab.com/gitlab/qitlab-ce/packages/e1/7/gitlab-ce-13.10.2-ce.0.e17.x86> 64.rpme

注:资料里提供了此rpm 包，直接将此包上传到服务器/opt/module 目录下即可。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309111700751-144644939.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309111756875-1908183696.png)

#### 10.3.3 编写安装脚本

> 进入官网 官网地址: <https://about.gitlab.com/>

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309112003251-510727312.png)

> 点击centos7

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309112111041-852749356.png)

> 会有配置的步骤

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309112249657-1158376971.png)

**安装 gitlab 步骤比较繁琐，因此我们可以参考官网编写 gitlab 的安装脚本。**

```shell
sudo rpm -ivh /opt/module/gitlab-ce-13.10.2-ce.0.e17.x86 64.rpm

vim gitlab-install.sh

sudo yum install -y curl policycoreutils-python openssh-server cronie

sudo lokkit -s http -s ssh

sudo yum install -y postfix

sudo service postfix start

sudo chkconfig postfix on

curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash

sudo EXTERNAL_URL="http://gitlab.example.com" yum -y install gitlab-ce

```

```shell
# 给脚本增加权限
chmod +x gitlab-install.sh

# 然后执行该脚本，开始安装 gitlab-ce。注意一定要保证服务器可以上网。
./gitlab-install.sh

```

#### 10.3.4 初始化GitLub服务

> 执行以下命令初始化 GitLab 服务，过程大概需要几分钟，耐心等待...

```shell
# 初始化 GitLab 服务
gitlab-ctl reconfigure
```

#### 10.3.5 启动GitLub服务

> 执行以下命令启动 GitLab 服务，如需停止，执行 gitlab-ctl stop

```shell
# 启动GitLub服务
gitlab-ctl start
```

### 10.3.6 使用浏览器访问GitLab

> 使用主机名或者IP 地址即可访问 GitLab 服务。需要提前配一下 windows 的 hosts 文件。
> 打开C:\Windows\System32\drivers\etc找到hosts文件，如下图配置，IP地址和主机名的映射。

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309145526840-284111557.png)

> 在浏览器输入IP地址或者主机名,访问GitLab,会让我们改密码,密码要求八位字母数字特殊符号组成.

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309145855900-285105326.png)

> 首次登陆之前，需要修改下 GitLab 提供的 root 账户的密码，要求8 位以上，包含大小写子母和特殊符号。因此我们修改密码为 Atguigu.123456

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309150317928-1709082636.png)

### 10.3.7 GitLab创建远程库

> New Project ---> Create blank project

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309150441388-142597855.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309150509713-1133250561.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309150547651-1723381140.png)

### 10.3.8 IDEA集成GitLab

**1、安装GitLab插件。**
> File ---> settings ---> Plugins
> 下载完成后重启，在File ---> settings --->Version Control 里面就可以看到GitLab

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309151149320-1154675958.png)

**2、添加GitLab服务器。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309151754641-1883366739.png)

**3、Push到GitLab服务器。**

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309152016582-148949934.png)

> 默认给的是例子的链接<http://gitlab.example.com/root/git-test.git>
> 要将其改成<http://gitlab-server/root/git-test.git>

- 将连接复制到IDEA中,自定义远程库链接

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309152453299-439855131.png)

![img](https://img2023.cnblogs.com/blog/2865045/202303/2865045-20230309152620798-1146207626.png)

> 只要 GitLab 的远程库连接定义好以后，对 GitLab 远程库进行 pull 和 clone 的操作和Github 和码云一致，此处不再赘述。
