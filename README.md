[TOC]

# 资料备份管理

没用过版本控制系统的，开发过程中，每天copy一份来备份代码或其他文档，间歇性拿移动硬盘copy备份代码。

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/58718695.png)
存在的缺点：
1. PM说改回之前什么需求的代码，然后就开始找代码，不记得就每个工程打开，看代码是否符合要求
2. 今天下午代码写错了，测试有bug，想还原到上午的代码，只能凭记忆慢慢删除下午添加的代码，或copy昨天的代码，拿出来重新慢慢添加今天新增的代码
3. 多人一起开发一个项目，怎么合并代码？
4. 项目有多个功能需求，分2次上线，同时开发，需求1部分需要第一期上线，需求2部分第二期上线，但是同时开发，代码如何管理
5. 想查看最近都修改了那些代码，如何找记录
6. 各种项目office文档在项目群里面满天飞，如何统一管理

`git就是解决这些问题的一种解决方案`

# what it is

git是一种版本控制系统,版本控制系统是一种记录若干文件内容变化，以便将来查阅特定版本修订情况的系统，有了它你就可以将某个文件回溯到之前的状态，甚至将整个项目都回退到过去某个时间点的状态。你可以比较文件的变化细节，查出最 后是谁修改了哪个地方，从而导致出现怪异问题，又是谁在何时报告了某个功能缺陷等等。使用版本控制系统通常还意味着，就算你乱来一气把整个项目中的文件改 的改删的删，你也照样可以轻松恢复到原先的样子。但额外增加的工作量却微乎其微。

看下面git客户端sourectree的一个截图，可以记录每次提交的时间，描述说明，作者，修改了那些文件，修改的内容对比等等

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/34608600.png)






## 本地版本控制系统

许多人习惯用复制整个项目目录的方式来保存不同的版本，或许还会改名加上备份时间以示区别。这么做唯一的好处就是简单。不过坏处也不少：有时候会混淆所在的工作目录，一旦弄错文件丢了数据就没法撤销恢复。

为了解决这个问题，人们很久以前就开发了许多种本地版本控制系统，大多都是采用某种简单的数据库来记录文件的历次更新差异。


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/a1648f31-ce9b-4153-abbb-44289822def9.png)

## 集中化的版本控制系统

接下来人们又遇到一个问题，如何让在不同系统上的开发者协同工作？于是，集中化的版本控制系统（ Centralized Version Control Systems，简称 CVCS ）应运而生。这类系统，诸如 CVS，Subversion(SVN) 以及 Perforce 等，都有一个单一的集中管理的服务器，保存所有文件的修订版本，而协同工作的人们都通过客户端连到这台服务器，取出最新的文件或者提交更新。多年以来，这 已成为版本控制系统的标准做法（见图 1-2）。



![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/3604b39d-8e52-4c3b-ab0b-eee4da988d63.png)

这种做法带来了许多好处，特别是相较于老式的本地 VCS 来说。现在，每个人都可以在一定程度上看到项目中的其他人正在做些什么。而管理员也可以轻松掌控每个开发者的权限，并且管理一个 CVCS 要远比在各个客户端上维护本地数据库来得轻松容易。

事分两面，有好有坏。这么做最显而易见的缺点是中央服务器的单点故障。如果宕机一小时，那么在这一小时内，谁都无法提交更新，也就无法协同工作。要 是中央服务器的磁盘发生故障，碰巧没做备份，或者备份不够及时，就还是会有丢失数据的风险。最坏的情况是彻底丢失整个项目的所有历史更改记录，而被客户端 提取出来的某些快照数据除外，但这样的话依然是个问题，你不能保证所有的数据都已经有人事先完整提取出来过。本地版本控制系统也存在类似问题，只要整个项 目的历史记录被保存在单一位置，就有丢失所有历史更新记录的风险。



## 分布式版本控制系统

于是分布式版本控制系统（ Distributed Version Control System，简称 DVCS ）面世了。在这类系统中，像 Git，Mercurial，Bazaar 以及 Darcs 等，客户端并不只提取最新版本的文件快照，而是把代码仓库完整地镜像下来。这么一来，任何一处协同工作用的服务器发生故障，事后都可以用任何一个镜像出来的本地仓库恢复。因为每一次的提取操作，实际上都是一次对代码仓库的完整备份（见图 1-3）。


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/468ad203-e5ff-4f14-9f39-c8a3be61f6c9.png)


更进一步，许多这类系统都可以指定和若干不同的远端代码仓库进行交互。籍此，你就可以在同一个项目中，分别和不同工作小组的人相互协作。你可以根据需要设定不同的协作流程，比如层次模型式的工作流，而这在以前的集中式系统中是无法实现的。



# why git
实际使用中，使用git(分布式版本控制系统)和svn(集中式版本控制系统)比较多，这里再一次集中比较一下优劣


## 本地仓储

- svn :本地开发版本+远端版本库 

- git: 本地开发版本+本地版本库+远端版本库，可以本地提交代码，提供了暂存区，可以方便指定提交内容，而不是全部



## 分支管理

- svn：无本地分支

- git：有本地分支



## 代码合并

- git：代码合并相对容易，冲突容易可通过第三方工具编辑解决。

- svn： 冲突比较难解决，如重命名（无论文件还有目录）提交后，你本地/或是分支上 有文件重命名前的这些文件的修改或提交，在做合并操作时，你会碰上传说中难搞的***树冲突***！



## 查看日志

- git: 本地包含完整日志

- svn: 需要从服务器拉取



## 其他比较

- [参考比较链接](https://www.cnblogs.com/dazhidacheng/p/7478438.html)

            版本工具

差异

svn

git

系统特点

1.集中式版本控制系统（文档管理很方便）

2.企业内部并行集中开发

3.windows系统上开发推荐使用

4.克隆一个拥有将近一万个提交(commit),五个分支,每个分支有大约1500个文件，用时将近一个小时

1.分布式系统（代码管理很方便）

2.开源项目开发

3.mac,Linux系统上开发推荐使用

4.克隆一个拥有将近一万个提交(commit),五个分支,每个分支有大约1500个文件，用时1分钟(Git 版本库所需的存储空间约为 SVN 的1/3)

灵活性

1.搭载svn的服务器出现故障，无法与之交互
2.所有的svn操作都需要中央仓库交互（例：拉分支，看日志等）

1.可以单机操作，git服务器故障也可以在本地git仓库工作
2.除了push和pull（或fetch）操作，其他都可以在本地操作
3.根据自己开发任务任意在本地创建分支
4.日志都是在本地查看，效率较高

安全性

较差，定期备份，并且是整个svn都得备份

较高，每个开发者的本地就是一套完整版本库，记录着版本库的所有信息（gitlab集成了备份功能）

分支方面

1.拉分支更像是copy一个路径
2.可针对任何子目录进行branch
3.拉分支的时间较慢，因为拉分支相当于copy
4.创建完分支后，影响全部成员，每个人都会拥有这个分支

5.多分支并行开发较重（工作较多而且繁琐）

1.我可以在Git的任意一个提交点（commit point）开启分支！（git checkout -b newbranch HashId）
2.拉分支时间较快，因为拉分支只是创建文件的指针和HEAD
3.自己本地创建的分支不会影响其他人

4.比较适合多分支并行开发

5.git checkout hash值(切回之前的版本，无需版本回退)

6.强大的cherry-pick

版本控制

1.保存前后变化的差异数据，作为版本控制
2.版本号进行控制，每次操作都会产生一个高版本号（svn的全局版本号，这是svn一个较大的特点，git是hash值）

1.git只关心文件数据的整体发生变化，更像是把文件做快照，文件没有改变时，分支只想这个文件的指针不会改变，文件发生改变，指针指向新版本
2. 40 位长的哈希值作为版本号，没有先后之分

3.git rebase操作可以更好的保持提交记录的整洁

工作流程

1.每次更改文件之前都得update操作，有的时候修改过程中这个文件有更新，commit不会成功
2.有冲突，会打断提交动作（冲突解决是一个提交速度的竞赛：手快者，先提交，平安无事；手慢者，后提交，可能遇到麻烦的冲突解决。）

1.开始工作前进行fetch操作，完成开发工作后push操作，有冲突解决冲突
2.git的提交过程不会被打断，有冲突会标记冲突文件

3.gitflow流程（经典）

内容管理

svn对中文支持好，操作简单，适用于大众

对程序的源代码管理方便，代码库占用的空间少，易于分支化管理

学习成本

使用起来更方便，svn对中文支持好，操作简单，适用于大众

更在乎效率而不是易用性，成本较高（有很多独有的命令，rebase，远程仓库交互的命令，等等）

权限管理

svn的权限管理相当严格，可以按组、个人针对某个子目录的权限控制（每个目录下都会有个.svn的隐藏文件）

git没有严格的权限管理控制，只有账号角色划分（在项目的home文件下有且只有一个.svn目录）

管理平台

有吧（这个“吧”字，肯定有，但本人没有接触过）

gitlab（建议使用，集成的功能较多，API开发），gerrit，github等


# how use it
本篇主要介绍git客户端sourcetree的使用，git详细知识原理等请参考文章最后的参考资料(熟悉git原理和常用命令可以使用更多git功能)
## windows环境souretree客户端下载安装
### 下载

官网下载windows souretree安装包https://www.sourcetreeapp.com,当前sourcetree使用的版本为 v2.6.10.0


### 跳过登录
![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/63752978.png)

安装好打开后，提示登录但是如果么有VPN是登录不了的，这里介绍一种不用登录的设置方法
，在弹出登录界面后，退出sourcetree,然后使用下面的路径输入到地址栏中打开
```
%LocalAppData%\Atlassian\SourceTree\
```
地址栏输入打开后，win7系统路径是这样的

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/64170872.png)

在这个目录下新建一个`accounts.json`文件，内容为,copy的时候要注意，如果格式不正确会导致sourcetree启动崩溃
可以新建一个文本文件，然后copy进去
```
[
  {
    "$id": "1",
    "$type": "SourceTree.Api.Host.Identity.Model.IdentityAccount, SourceTree.Api.Host.Identity",
    "Authenticate": true,
    "HostInstance": {
      "$id": "2",
      "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountInstance, SourceTree.Host.AtlassianAccount",
      "Host": {
        "$id": "3",
        "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountHost, SourceTree.Host.AtlassianAccount",
        "Id": "atlassian account"
      },
      "BaseUrl": "https://id.atlassian.com/"
    },
    "Credentials": {
      "$id": "4",
      "$type": "SourceTree.Model.BasicAuthCredentials, SourceTree.Api.Account",
      "Username": "",
      "Email": null
    },
    "IsDefault": false
  }
]
```

如果一切正常，再次启动sourcetree就跳过登录了

### 打开后安装插件等

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/64268251.png)
选择第一个，根据提示安装完成后进入下一步(如图系统中已经安装git，也可以使用系统中的Git)

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/48935402.png)
选择最后一个`我不想使用Mercurial`，我们主要使用git，不需要Mercurial



## mac环境souretree客户端安装
官网下载好安装包后，双击安装即可，目前可以下载老版本或下载最新版本使用VPN登录souretree账号即可。

## SSH创建及配置
大多数 Git 服务器都会选择使用 SSH 公钥来进行授权通信，下面将介绍如何创建和使用SSH(本篇以RSA公私钥对形式)，将公钥内容添加到git仓库SSH key，电脑端使用私钥。

#### windows端生成
windows生成需要windows安装git命令行工具，可以在github上下载：https://github.com/git-for-windows/git/releases

安装参考：https://blog.csdn.net/lvkelly/article/details/54666868
安装好后，找到 Git Bash打开
![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/32884452.png)

输入如下命令，后面的为你自己的邮件地址或用户名都可以

ssh-keygen -t rsa -C "lbxia20091227@formail.com"

然后连续3次enter键即可

生成的ssh路径命令行中有提示（见途中红色下划线） ，将 id_rsa.pub文本打开，内容copy，添加到对应git仓库中ssh keys，在下面会介绍如何添加github和公司私有gitlab仓库中去


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/54065592.png)


souretree客户端设置 

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/35790675.png)


SSH客户端选择OpenSSH
SSH密钥选择对应路径的私钥文件即可
点击确定后

有时候按点击确定后报 ssh-agent 失败 system.nullreferenceException ，测试可以使用，应该是服务器端的bug。

首次使用私有仓库可能还会要输入账号密码 


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/57525443.png)



#### mac端生成

打开终端输入命令： ssh-keygen
然后系统提示输入文件保存位置等信息，一直使用默认值，连续敲三次回车即可，生成的SSH key文件保存在中～/.ssh/id_rsa.pub
vim ~/.ssh/id_rsa.pub
将.pub中的内容copy添加到git仓库的ssh key里面去即可

.ssh在mac系统中默认是隐藏的，一般路径为 硬盘/用户/user/.ssh/

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/56390050.png)


mac端sourectree客户端不需要配置，默认路径即可。

### github仓库SSH添加
github： 个人->Setting->SSH and GPG keys 
选择`New SSH key`


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/56390050.png)



将电脑端生成 id_rsa.pub文件文本打开，内容copy，复制到key选项里面即可，标题可以任意填写。

### 公司内部gitlab仓库SSH添加
操作步骤见图标注所示，最后将电脑端生成 id_rsa.pub文件文本打开，内容copy，复制到key选项里面即可，添加key之后标题默认显示邮件地址，当然也可以任意填写。

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/55159231.png)




## souretree使用介绍
本篇主要使用windows环境操作souretree，mac环境操作基本一样，souretree界面布局有少许差别。
#### git仓库创建
`github上创建一个仓库示例`

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/58231329.png)



`公司内部gitlab示例`
点击New project，内容有项目目录，项目名称，项目描述，项目等级

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/35473105.png)



点击如图中的图标复制SSH路径，然后再sourcetree中clone添加新项目即可。

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/35574946.png)





#### 首次下载(clone)
clone地址为 http或https形式，表示客户端和服务器通信通过账号密码形式
clone地址为git@形式，表示客户端和服务器通信通过SSH形式


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/39282898.png)




仓库文件介绍

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/40362072.png)



.gitignore文件(隐藏文件)，表示忽略哪些文件或文件夹，不用记录到版本控制仓库
.git文件夹(隐藏文件夹) 仓库文件夹，本地版本仓库

新建2个文件，暂存提交（可以选择部分暂存提交，方便更细的写代码修改记录）


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/36256220.png)





![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/5f601715-aaf6-4a4f-8e12-749a798f60c0.png)



提交后会有个推送的提示(项目新clone首次修改提交存在不显示推送提示bug，可主动点击推送)

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/36547712.png)





### 多人开发
多人合作开发一个项目的时候，难免会遇到修改冲突的时候，这个时候合并代码的时候就需要解决冲突，如果没有好的工具，只能手动修改，或者以谁为准，然后再添加另外一个人的代码上去。
#### 冲突解决工具Beyond Compare
Beyond Compare是一款优秀的文件比对工具，这里使用它来帮我们解决冲突问题。
souretree设置外部比对工具，选择Beyond Compare
mac OS：偏好设置，选择Diff

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/59259956.png)



windows端: 工具->选项->比较

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/61238366.png)




冲突操作示例
以mac下的souretree示例，windows类似

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/60044271.png)



BeyondCompare工具打开的冲突对比编辑窗口

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/57199503.png)



图中标注的`1`、`2`、`3`分别表示
- `1`： 本地的代码
- `2`：远程代码
- `3`：默认显示的远程代码，可通过右下角选项，选择某项操作后，然后编辑下方代码，也可以直接编辑

对`3`编辑完成后，按保存快捷键 ctrl+s(mac:cmd+s)，然后检查souretree中冲突代码是否修改正确，然后右冲突文件(有感叹号)右键，标记为已解决，后缀为 orig的文件为解决冲突生成的临时文件，右键选择移除即可。
![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/60530927.png)



### 恢复到历史版本

提交回滚操作适合在最新的提交记录上面提交回滚，否则选中的记录提交回滚之后会提示很多和之前的版本文件冲突，很麻烦，这个时候可以选择重置到这次提交系列操作方案。

#### step1
选中某次需要恢复的提交，右键选择 "将master重置到这次提交" （master为当前分支）

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/53956722.png)



然后选择如下图的使用模式

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/54266809.png)




#### step2
step1完成后，只是本地分支内容恢复到我们想要的历史记录，远程代码没变，所以显示落后2个版本，在最新提交上右键，选择重置到这次提交


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/54729041.png)



然后选择如图所示的

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/54780140.png)



会出现需要新提交的改变内容，其实就删除了这个历史版本之后提交的代码，提交后即完成恢复到历史版本的目的，可以注意到，这套操作不会改变提交记录。

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/54881868.png)




### 分支
一般仓库默认有个主分支master，可以基于某个提交任意创建新分支。（可以类比为某个提交为基类，新分支为子类，子类继承了基类的所有，新建很多分支，就是新建了很多子类，子类互不干扰。）

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/40429175.png)



#### 新建分支

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/37197428.png)



创建后只是本地创建了分支，需要操作推送到远程服务器端

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/36989710.png)



#### 删除分支
不能删除当前显示的分支

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/37148548.png)




#### 分支合并
先切换到最终合并的分支，然后选择需要合并的提交记录，右键选择合并，合并的时候如果有冲突，会有提示，使用第三方工具解决即可。

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/38054460.png)




![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/38038313.png)




### 标签
tag(标签)就是对某次commit提交记录(可能比较重要的时间点，比如某次上线代码)一个标签，方便将来查找
选择某次commit，右键选择标签


![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/58766764.png)



然后填写标签名称和勾选推送标签后，点击按钮`添加标签`即可

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/58378979.png)




如何查看tag
左侧标签列表或右侧跳转到均可以

![image](https://raw.githubusercontent.com/MxABC/Resource/master/git-sourcetree/58655447.png)




# git学习参考资料
- [git-scm](https://git-scm.com/book/zh/v1)
- [廖雪峰Git教程链接](http://t.cn/zQ6LFwE)
- [geeeeeeeeek](https://github.com/geeeeeeeeek/git-recipes)
- [my-git](https://github.com/xirong/my-git)
- [git原理入门](http://www.ruanyifeng.com/blog/2018/10/git-internals.html)





