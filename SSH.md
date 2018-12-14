

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




