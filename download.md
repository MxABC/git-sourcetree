
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







