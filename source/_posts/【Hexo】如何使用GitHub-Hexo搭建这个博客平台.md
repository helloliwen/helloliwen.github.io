---
title: 如何使用GitHub+Hexo搭建这个博客平台
categories: hexo
abbrlink: 62ffb8b5
date: 2019-06-03 20:47:42
tags:
keywords: hexo,hexo安装部署,hexo主题配置,SEO优化
description: 本文介绍为什么要写博客以及使用的博客平台和Hexo安装部署、Hexo主题配置信息等
---

### 一、为什么要写博客

　　**当自己主动学习，主动思考其效率和对个人的提升无疑是高于被动接受的。然而使你提高最大的是主动说出自己认知，把自己的知识和理解传达给他人，这种方式是对你提升无疑是最显著的。**

<!--more-->

引用《码农翻身》里的一段话：

<font color="red">对自己狠一点，开始写作吧。</font>

　　自己心里觉得对一个技术点已经掌握了，但是当我试图给别人讲述的时候，发现并不能轻松自如、深入浅出地讲出来，这就说明了一个问题：自以为掌握了，其实并没有真正掌握。

　　为什么要有这门技术、这门技术解决了什么问题，然后才是这门技术是怎么使用的。

　　整理资料和思考的过程是很珍贵的，只有这样才能把信息变成自身的知识。不写出来，很容易放弃深度思考。

　　我们已经进入了一个碎片化的时代，我们的大脑已经养成了碎片化的习惯，一天不看碎片化的信息就觉得不舒服，这样下去会慢慢的丧失深度思考的能力。写作会逼着你去思考，梳理知识体系，防止自己被碎片化所填满。

　　最后，能够坚持的人才更有可能成功！

　　[为什么你要写博客？——陈素封](https://zhuanlan.zhihu.com/p/19743861?columnSlug=cnfeat)

### 二、为什么使用GitHub+Hexo

　　我很喜欢掘金的风格，里面也有很多大牛，但是因为没有文章分类，只好作罢。CSDN是很多人的入门博客，但是不屏蔽广告完全没法看。简书也不错，但是个人感觉总少点技术氛围。其他博客平台没有使用过，不作评论。至于为什么选择GitHub+Hexo，可能出于成就感吧，而且给我的感觉完全像一张白纸可以在上面任意发挥，而且文章有分类、没有广告、风格很简约，喜欢，所以选择这个平台。

　　至于其他平台的评论，参看这篇文章：[程序员可以选择哪些平台写技术博客？](<https://mp.weixin.qq.com/s?src=11×tamp=1559567191&ver=1646&signature=M8olE56Lf0LYxFyo5e5mClnfNlP0dHG04YgH-pTO1AIe3r5Ao7RSccXBVIn1PAATEhuniqA-Nr2cI*XCQEdrQ6SzjtrtFBmZv8G7vmOs8lOr9Ip4gG9gJLqapMh2SXk6&new=1>)，如果提示无法访问，使用[搜狗微信](https://weixin.sogou.com/)平台搜索文章。

### 三、准备环境

#### 1.关于Hexo、Node.js

**Hexo的工作机制**

　　由于github pages存放的都是静态文件，博客存放的不只是文章内容，还有文章列表、分类、标签、翻页等动态内容，假如每次写完一篇文章都要手动更新博文目录和相关链接信息，相信谁都会疯掉，所以hexo所做的就是将这些md文件都放在本地，每次写完文章后调用写好的命令来批量完成相关页面的生成，然后再将有改动的页面提交到github。

　　Hexo基于Node.js，将/source文件夹下的资源(文章、图片、模板)，按照预定的配置文件，转换成静态页面放置到/public目录下。如果需要预览或者部署，hexo会把public作为web目录处理。具体的细节可以通过实践接下来的步骤，来逐渐明晓。

**Hexo 特点**

1. 支持Markdown: 支持Markdown意味着你可以把经历从排版中解放出来
2. 轻量: 无需拥有后台及数据库，专心写好你的文章
3. 一键部署: 可以通过Git或者ftp来将生成的静态页面部署到服务器或者主机空间中
4. 插件丰富: 丰富的插件可以满足你的各种需求

**Node.js**
　　Node.js是一个基于Chrome V8引擎的JavaScript运行环境，为我们的Hexo提供js脚本的运行环境。而npm则

是一个JavaScript的包管理工具。主流的很多语言都会有自己的包管理器，Hexo官网教程中使用的是npm。

**优势：**

1. 全是静态文件，访问速度快；
2. 免费方便，不用花一分钱就可以搭建一个自由的个人博客，不需要服务器不需要后台；
3. 可以随意绑定自己的域名，不仔细看的话根本看不出来你的网站是基于github的；
4. 数据绝对安全，基于github的版本管理，想恢复到哪个历史版本都行；
5. 博客内容可以轻松打包、转移、发布到其它平台；
6. 等等。

**博客搭建过程**

一个博客的搭建过程分为三步：

- 编写：包含内容的书写与格式的配置
- 构建：从编写的原始内容生成可发布的最终内容
- 发布：让待发布的内容对读者可见

　　依托于博客平台（如博客园、新浪博客等）发布内容的用户只需要关注编写部分，但要搭建一个独立的个人博客则以上三方面都需要关心。幸运的是，现在有大量的工具帮助我们简化这个过程：丰富的 Markup 语言简化了编写；强大的静态站点生成器简化了构建；友好的托管平台简化了发布。

这个博客的诞生也得益于这些工具：

- 编写：使用 Markdown，内置大量层级、列表、超链接、代码等的简便语法支持
- 构建：使用 Hexo，几条命令完成生成、预览、发布步骤
- 发布：使用 GitHub Pages 进行托管，方便又免费

#### 2.准备工作

（1）有一个Github账户

（2）安装Node.js

[Node.js官网](https://nodejs.org/zh-cn/download/)下载LTS版本，并安装，配置环境变量，在命令行中通过查看版本。

（3）安装Git

[Git官网](https://git-scm.com/downloads)下载，安装，配置环境变量，使用git --version查看是否安装成功。


（4）注意事项

　　很多命令既可以用Windows的cmd来完成，也可以使用git bash来完成，但是部分命令会有一些问题，为避免不必要的问题，建议全部使用git bash来执行；

　　hexo不同版本差别比较大，网上很多文章的配置信息都是基于2.x的，所以注意不要被误导；

　　hexo有2种`_config.yml`文件，一个是根目录下的全局的`_config.yml`，一个是各个`theme`下的。

#### 3.设置使用ssh提交到Github Pages

**设置用户名和邮箱**

初次安装git需要配置用户名和邮箱，否则git会提示：please tell me who you are.

你需要运行命令来配置你的用户名和邮箱：

```shell
$ git config --global user.name "yourName"
$ git config --global user.email "your_email@example.com"
```

注意：引号内请输入你自己设置的名字，和你自己的邮箱。此用户名和邮箱是git提交代码时用来显示你身份和联系方式的，并不是github用户名和邮箱。

**git使用ssh密钥**

　　git支持https和git两种传输协议。相应的，github分享链接时会有两种协议可选：git格式和https格式。使用https协议，每次pull, push都会提示要输入密码。使用git协议，然后使用ssh密钥，这样免去每次都输密码的麻烦。

（1）生成密钥对

　　大多数 Git 服务器都会选择使用 SSH 公钥来进行授权，SSH 公钥默认储存在账户的主目录下的 ~/.ssh 目录。首先需要检查你电脑是否已经有 SSH key 

　　运行 git Bash 客户端，输入如下命令，看一下有没有id_rsa和id_rsa.pub(或者是id_dsa和id_dsa.pub之类成对的文件)，有 .pub 后缀的文件就是公钥，另一个文件则是密钥。假如没有这些文件，甚至连 .ssh 目录都没有，可以用 ssh-keygen 来创建。

```shell
$ cd ~/.ssh
$ ls
```

（2）创建一个 SSH key，直接按Enter就行。然后，会提示你输入密码，如下(建议输一个，安全一点，当然不输也行，应该不会有人闲的无聊冒充你去修改你的代码)：

```shell
$ ssh-keygen -t rsa -C "your_email@example.com"
```

**添加公钥到你的远程仓库（github）**

（1）查看你生成的公钥：

```shell
$ cat ~/.ssh/id_rsa.pub
```

（2）登陆你的github帐户。点击你的头像，然后 `Settings -> 左栏点击 SSH and GPG keys -> 点击 New SSH key`

（3）然后你复制上面的公钥内容，粘贴进“Key”文本域内。 title域，自己随便起个名字。

（4）验证

```shell
$ ssh -T git@github.com
```

如果看到

```shell
Hi helloliwen! You've successfully authenticated, but GitHub does not provide shell access.
```

恭喜你，你的设置已经成功了。

**修改git的remote url**

在hexo目录下，使用命令 git remote -v 查看你当前的 remote url

```shell
$ git remote -v
origin https://github.com/someaccount/someproject.git (fetch)
origin https://github.com/someaccount/someproject.git (push)
```

如果是以上的结果那么说明此项目是使用https协议进行访问的（如果地址是git开头则表示是git协议），你可以登陆你的github，就像本文开头的图例，你在上面可以看到你的ssh协议相应的url。

复制此ssh链接，然后使用命令 git remote set-url 来调整你的url。

```
git remote set-url origin git@github.com:someaccount/someproject.git
```

然后你可以再用命令 git remote -v 查看一下，url是否已经变成了ssh地址。

然后你就可以愉快的使用git fetch, git pull , git push，再也不用输入烦人的密码了。

[让git push命令不再每次都输入密码 ssh配置_已迁移](https://my.oschina.net/Majw/blog/750049)

[保存、删除、编辑已记住的 Git 账号和密码](https://alvinwp.com/common-sense/1887)

**记录一次困恼一天的问题：**

~~~shell
$ ssh -vT git@github.com
OpenSSH_7.7p1, OpenSSL 1.0.2o  27 Mar 2018
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Connecting to github.com [43.240.146.45] port 22.
debug1: Connection established.
debug1: identity file /c/Users/liwen/.ssh/id_rsa type 0
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_rsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_dsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_dsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_ecdsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_ecdsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_ed25519 type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_ed25519-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_xmss type -1
debug1: key_load_public: No such file or directory
debug1: identity file /c/Users/liwen/.ssh/id_xmss-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_7.7
debug1: Remote protocol version 2.0, remote software version OpenSSH_7.4
debug1: match: OpenSSH_7.4 pat OpenSSH* compat 0x04000000
debug1: Authenticating to github.com:22 as 'git'
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: ecdsa-sha2-nistp256
debug1: kex: server->client cipher: aes128-ctr MAC: umac-64-etm@openssh.com compression: none
debug1: kex: client->server cipher: aes128-ctr MAC: umac-64-etm@openssh.com compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: Server host key: ecdsa-sha2-nistp256 
SHA256:***
debug1: Host 'github.com' is known and matches the ECDSA host key.
debug1: Found key in /c/Users/liwen/.ssh/known_hosts:1
debug1: rekey after 4294967296 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey after 4294967296 blocks
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<rsa-sha2-256,rsa-sha2-512>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Next authentication method: publickey
debug1: Offering public key: RSA  ***
/c/Users/liwen/.ssh/id_rsa
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Trying private key: /c/Users/liwen/.ssh/id_dsa
debug1: Trying private key: /c/Users/liwen/.ssh/id_ecdsa
debug1: Trying private key: /c/Users/liwen/.ssh/id_ed25519
debug1: Trying private key: /c/Users/liwen/.ssh/id_xmss
debug1: Next authentication method: password
git@github.com's password:
~~~

无论删除.ssh/文件夹，然后重新添加公钥到github，都需要输入密码。可是生成ssh文件的时候没有输入密码的。所以碰到这个问题不知道哪里出了问题，只能去谷歌找答案。但是大部分都是Linux免秘钥登录，出现的问题解决方案都是.ssh/文件夹和authorized_keys文件权限不对，但是windows文件夹没有600或者700权限这一说！或者教你如何ssh登录github，步骤大同小异。还是无法解决问题。而且这几天github国内网络无法直接访问，不知道和这个有没有关系。最后怀疑可能github缓存导致，过几天再看吧！

[After uploading ssh pub key, git still ask for password]( https://www.drupal.org/project/git_dev/issues/1164232 )

几天之后，突然发现github.com可以正常访问了！测试：

~~~shell
C:\Users\liwen>ssh -T git@github.com
The authenticity of host 'github.com (52.74.223.119)' can't be established.
RSA key fingerprint is ***
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,52.74.223.119' (RSA) to the list of known hosts.
Hi helloliwen! You've successfully authenticated, but GitHub does not provide shell access.
~~~

之前ping github.com的时候，域名为43.240.146.45，来自深圳。今天是：

~~~shell
C:\Users\liwen>ping github.com

正在 Ping github.com [13.250.177.223] 具有 32 字节的数据:
请求超时。
请求超时。
请求超时。
请求超时。

13.250.177.223 的 Ping 统计信息:
    数据包: 已发送 = 4，已接收 = 0，丢失 = 4 (100% 丢失)，
~~~

什么都没做，问题解决！

~~~shell
C:\Users\liwen>ssh -vT git@github.com
OpenSSH_for_Windows_7.7p1, LibreSSL 2.6.5
debug1: Connecting to github.com [13.250.177.223] port 22.
debug1: Connection established.
debug1: identity file C:\\Users\\liwen/.ssh/id_rsa type 0
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_rsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_dsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_dsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_ecdsa type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_ecdsa-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_ed25519 type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_ed25519-cert type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_xmss type -1
debug1: key_load_public: No such file or directory
debug1: identity file C:\\Users\\liwen/.ssh/id_xmss-cert type -1
debug1: Local version string SSH-2.0-OpenSSH_for_Windows_7.7
debug1: Remote protocol version 2.0, remote software version babeld-2e9d163d
debug1: no match: babeld-2e9d163d
debug1: Authenticating to github.com:22 as 'git'
debug1: SSH2_MSG_KEXINIT sent
debug1: SSH2_MSG_KEXINIT received
debug1: kex: algorithm: curve25519-sha256
debug1: kex: host key algorithm: rsa-sha2-512
debug1: kex: server->client cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: kex: client->server cipher: chacha20-poly1305@openssh.com MAC: <implicit> compression: none
debug1: expecting SSH2_MSG_KEX_ECDH_REPLY
debug1: Server host key: ssh-rsa 
SHA256:***
debug1: Host 'github.com' is known and matches the RSA host key.
debug1: Found key in C:\\Users\\liwen/.ssh/known_hosts:1
Warning: Permanently added the RSA host key for IP address '13.250.177.223' to the list of known hosts.
debug1: rekey after 134217728 blocks
debug1: SSH2_MSG_NEWKEYS sent
debug1: expecting SSH2_MSG_NEWKEYS
debug1: SSH2_MSG_NEWKEYS received
debug1: rekey after 134217728 blocks
debug1: pubkey_prepare: ssh_get_authentication_socket: No such file or directory
debug1: SSH2_MSG_EXT_INFO received
debug1: kex_input_ext_info: server-sig-algs=<ssh-ed25519,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,rsa-sha2-512,rsa-sha2-256,ssh-dss>
debug1: SSH2_MSG_SERVICE_ACCEPT received
debug1: Authentications that can continue: publickey
debug1: Next authentication method: publickey
debug1: Offering public key: RSA ***
C:\\Users\\liwen/.ssh/id_rsa
debug1: Server accepts key: pkalg ssh-rsa blen 279
debug1: Authentication succeeded (publickey).
Authenticated to github.com ([13.250.177.223]:22).
debug1: channel 0: new [client-session]
debug1: Entering interactive session.
debug1: pledge: network
debug1: client_input_channel_req: channel 0 rtype exit-status reply 0
Hi helloliwen! You've successfully authenticated, but GitHub does not provide shell access.
debug1: channel 0: free: client-session, nchannels 1
Transferred: sent 2560, received 2228 bytes, in 0.6 seconds
2
~~~

#### 4.创建仓库

　　新建一个名为`你的用户名.github.io`的仓库，比如说，如果你的github用户名是test，那么你就新建`test.github.io`的仓库（必须是你的用户名，其它名称无效），将来你的网站访问地址就是 http://test.github.io 了，是不是很方便？

　　由此可见，每一个github账户最多只能创建一个这样可以直接使用域名访问的仓库。

几个注意的地方：

1. 注册的邮箱一定要验证，否则不会成功；
2. 仓库名字必须是：`username.github.io`，其中`username`是你的用户名；
3. 仓库创建成功不会立即生效，需要过一段时间，大概10-30分钟，或者更久，我的等了半个小时才生效；

　　创建成功后，默认会在你这个仓库里生成一些示例页面，以后你的网站所有代码都是放在这个仓库里啦。

![](http://ww1.sinaimg.cn/large/75a4a8eegy1g3vvgg8qtyj20rs0hgjrq.jpg)

### 四、Hexo博客安装使用

#### 1.安装hexo

（1）首先需要知道两个配置文件，需要特别注意的地方是，冒号后面必须有一个空格，否则可能会出问题。

- Hexo配置文件：**hexo/_config.yml**
- NeXT主题配置：**hexo/themes/next/_config.yml**

（2）安装hexo

~~~shell
npm install hexo-cli -g  
~~~

（3）选择一个目录作为hexo站点目录，然后进入目录，执行以下命令初始化：

~~~shell
hexo init
~~~

hexo会自动下载一些文件到这个目录，包括node_modules，目录结构如下图：

![](http://image.liuxianan.com/201608/20160818_115922_773_1148.png)

（4）生成并启动服务

~~~shell
hexo g #生成 或 hexo generate  
hexo s #启动本地服务器 或者 hexo server，这一步之后就可以通过http://localhost:4000查看了
~~~

（5）更新hexo

~~~shell
npm update -g hexo
~~~

（6）Windows下npm安装Hexo失败的解放方案

因为国外源网速不好的原因，安装hexo失败，可以采用如下方案：

```shell
# 添加淘宝源
npm install -g cnpm --registry=https://registry.npm.taobao.org
# nrm类似包管理器
cnpm install nrm -g
nrm ls
# 使用淘宝
nrm use taobao
npm install -g hexo-cli
```

参考：[(node.js)使用淘宝镜像安装hexo失败](<http://www.codes51.com/itwd/1327882.html>)

#### 2.安装主题

（1）安装主题NexT（当然还有很多其他主题，可以去选择自己喜欢的主题：[官方主题](https://hexo.io/themes/)，本人选择NexT）

~~~shell
git clone https://github.com/iissnan/hexo-theme-next themes/next
~~~

（2）启用主题

打开Hexo配置文件：hexo/_config.yml，修改

~~~shell
theme: next
~~~

（3）设置语言

hexo/_config.yml

~~~shell
language: zh-Hans
~~~

（4）更新主题

cd 到主题文件夹，执行命令（需要隐藏的.git文件夹没有被删除）

~~~shell
git pull
~~~

#### 3.创建博客及常用命令

~~~java
hexo new "文章名" #新建文章
hexo new page "页面名" #新建页面   
~~~

那么`hexo new 'postName'`命令和`hexo new page 'postName'`有什么区别呢？

```
hexo new page "my-second-blog"
```

生成如下：

![img](http://image.liuxianan.com/201608/20160823_184852_854_6502.png)

最终部署时生成：`hexo\public\my-second-blog\index.html`，但是它不会作为文章出现在博文目录。

常用命令及缩写

~~~shell
hexo cl = hexo clean	# 清除缓存
hexo n = hexo new		# 新建文章
hexo g = hexo generate	# 生成静态页面至public目录
hexo s = hexo server	# 启动服务
hexo d = hexo deploy	# 部署到GitHub
hexo h = hexo help  	# 查看帮助
hexo v = hexo version  	#查看Hexo的版本
#会根据gulpfile.js中的配置，对public目录中的静态资源文件进行压缩。
hexo g && gulp
~~~

组合命令：

~~~shell
hexo cl && hexo g && gulp && hexo d
hexo s -g #生成并本地预览
hexo d -g #生成并上传
~~~

#### 4.部署

　　上传之前：在上传代码到github之前，一定要记得先把你以前所有代码下载下来（虽然github有版本管理，但备份一下总是好的），因为从hexo提交代码时会把你以前的所有代码都删掉。

首先安装扩展文件

~~~shell
npm install hexo-deployer-git --save   
~~~

其次需要配置Hexo配置文件：hexo/_config.yml

~~~xml
#正确写法
deploy:
    type: git
    repo: git@github.com:cczeng/cczeng.github.io.git  #这里的网址填你自己的，中间有空格要注意
    branch: master   

#错误写法
deploy:
  type: github
  repository: https://github.com/liuxianan/liuxianan.github.io.git
  branch: master
~~~

接下来就是使用Hexo部署到我们的Github仓库上

~~~shell
hexo cl && hexo g && hexo d
~~~

接下来等待几分钟就可以打开浏览器，输入：https://username.github.io就可以看到博客了。

#### 5.常见问题

（1）如何让博文列表不显示全部内容：在合适的位置加上`<!--more-->`即可

（2）电脑重装了系统/多台电脑写博客？那就赶紧戳这里：[使用hexo，如果换了电脑怎么更新博客？](<https://www.zhihu.com/question/21193762>)

（3）想要给网站添加图片？方式一：使用图床。国内的有：**微博图床**、**阿里云OSS**、**腾讯云COS**、**七牛云**。具体可以查看这里：[嗯，图片就交给它了](<https://sspai.com/post/40499>)。方式二：在根目录 **source** 下建立一个文件夹，加入取名叫upload-images，把图片放在这个文件夹下，然后在博客中连接就是：/upload-images/图片名，执行hexo g的时候此文件夹自动生成到public中。

### 五、Hexo配置

#### 1.基本信息配置

基本信息包括：博客标题、作者、描述、语言等等。打开**_config.yml**，找到Site模块

```
title: 标题
subtitle: 副标题
description: 描述
author: 作者
language: 语言（简体中文是zh-Hans）
timezone: 网站时区（Hexo 默认使用您电脑的时区，不用写）
```

其他配置可参考[站点配置](<https://hexo.io/zh-cn/docs/configuration.html>)

#### 2.设置头像及网站的icon

首先把图片放在**source/images**目录下，并修改配置文件**themes/next/_config.yml**

~~~shell
avatar: /images/avatar.jpg
favicon: /images/favicon32.ico
~~~

#### 3.Next主题样式设置

我们百里挑一选择了Next主题，不过Next主题还有4种风格供我们选择，打开 **themes/next/_config.yml** 找到Scheme Settings

```
# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
#scheme: Muse
#scheme: Mist
scheme: Pisces
#scheme: Gemini
```

4种风格大同小异，本人用的是Pisces风格，你们可以选择自己喜欢的风格。

#### 4.菜单设置

刚开始默认的菜单只有首页和归档两个，修改菜单设置文件： **themes/next/_config.yml**

```
menu:
  home: / || home                          //首页
  archives: /archives/ || archive          //归档
  categories: /categories/ || th           //分类
  tags: /tags/ || tags                     //标签
  #about: /about/ || user                  //关于
  #schedule: /schedule/ || calendar        //日程表
  #sitemap: /sitemap.xml || sitemap        //站点地图
  #commonweal: /404/ || heartbeat          //公益404
```

需要哪个菜单取消注释就好了。关于后面的格式，以`archives: /archives/ || archive`为例：
`||` 之前的`/archives/`表示标题“归档”，关于标题文字可以去`themes/next/languages/zh-Hans.yml`中参考或修改。
`||`之后的`archive`表示图标，可以去[Font Awesome](https://link.jianshu.com/?t=http%3A%2F%2Ffontawesome.io%2Ficons%2F)中查看或修改，Next主题所有的图标都来自Font Awesome。

#### 5.侧栏设置

侧栏设置包括：侧栏位置、侧栏显示与否、文章间距、返回顶部按钮等等。打开 **themes/next/_config.yml** 找到`sidebar`字段

```
sidebar:
# Sidebar Position - 侧栏位置（只对Pisces | Gemini两种风格有效）
  position: left        //靠左放置
  #position: right      //靠右放置

# Sidebar Display - 侧栏显示时机（只对Muse | Mist两种风格有效）
  #display: post        //默认行为，在文章页面（拥有目录列表）时显示
  display: always       //在所有页面中都显示
  #display: hide        //在所有页面中都隐藏（可以手动展开）
  #display: remove      //完全移除

  offset: 12            //文章间距（只对Pisces | Gemini两种风格有效）
  b2t: false            //返回顶部按钮（只对Pisces | Gemini两种风格有效）
  scrollpercent: true   //返回顶部按钮的百分比
```

#### 6.添加标签页面

新建页面：

  ```
  hexo new page tags
  ```

设置页面（编辑 **source/tags/index.md**）：

  ```
  ---
  title: tags
  date: 2018-09-12 10:30:31
  type: "tags"
  comments: false
  ---
  ```

修改菜单（编辑 **themes/next/_config.yml**）：

  ```
  menu: 
  	tags: /tags
  ```

#### 7.添加分类页面

新建页面：

  ```
  hexo new page categories
  ```

设置页面（编辑 **source/categories/index.md**）：

  ```
  ---
  title: categories
  date: 2018-09-12 10:32:08
  type: "categories"
  ---
  ```

修改菜单（编辑 **themes/next/_config.yml**）：

  ```
  menu:
    categories: /categories/
  ```

使用：

~~~xml
---
title: jQuery对表单的操作及更多应用
date: 2017-05-26 12:12:57
categories: 
	- web前端 #一级分类
	- jQuery #二级分类
---
~~~

scaffolds目录下，是新建页面的模板，执行新建命令时，是根据这里的模板页来完成的，所以可以在这里根据你

自己的需求添加一些默认值。打开scaffolds/post.md文件，在tages:上面加入categories:，保存后，之后执行

`hexo new 文章名`命令生成的文件，页面里就有`categories:`项了。

~~~
title: {{ title }}
date: {{ date }}
categories: 
tags: 
keywords: 
description: 
~~~

#### 8.修改二级分类符号

二级分类使用

```markdown
categories: 
- 笔记
- 题解
- t
```

**themes\next\layout\_macro\post.swig**

~~~
{% if cat_length > 1 and loop.index !== cat_length %}
    {{ __('symbol.comma') }}
{% endif %}
~~~

__('symbol.comma')就是二级分类所使用的符号，具体定义在**themes\next\languages\zh-Hans.yml**

~~~
symbol:
  comma: '， '
  period: '。 '
  colon: '：'
~~~

#### 9.站内搜索功能

- hexo-generator-searchdb

安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：

```
$ npm install hexo-generator-searchdb --save
```

编辑站点配置文件，新增以下内容到任意位置：

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

- hexo-generator-search

安装 hexo-generator-search 插件

```shell
$ npm install hexo-generator-search –save
```

配置站点文件_config.yml:

```
# 站内搜索
search:
    path: search.xml
    field: post
```

配置主题文件_config.yml:

```
local_search:
    enable: true
```

#### 10.修改字体大小和字体

- 字体大小

修改文件：**\themes\next\source\css\ _variables\base.styl**

~~~shell
$font-size-base
~~~

- 字体

全局字体：**\themes\next\_config.yml**

~~~shell
family: Lato
~~~

字体文件：**\themes\next\source\css\_variables\base.styl**

~~~shell
$font-family-chinese = "PingFang SC", "Microsoft YaHei"
$font-family-base = $font-family-chinese, sans-serif
$font-family-base = get_font_family('global'), $font-family-chinese, sans-serif if get_font_family('global')
~~~

参考：[Hexo博客之改字体](http://prozhuchen.github.io/2015/10/05/Hexo_blog_7/)

#### 11.设置文章字体的颜色、大小

如果想设置某一句的颜色或大小，只需用html语法写出来就行了

```html
接下来就是见证奇迹的时刻
<font color="#FF0000"> 我可以设置这一句的颜色哈哈 </font> 
<font size=6> 我还可以设置这一句的大小嘻嘻 </font> 
<font size=5 color="#FF0000"> 我甚至可以设置这一句的颜色和大小呵呵</font> 
```

#### 12.文字居中显示

```html
<center>这一行需要居中</center>
```

#### 13.显示文章更新时间

　　在文章列表中我们一般都能看的文章的发布时间。对于一些文章来说，比如涉及到文章中的内容过期，或者软件的升级等等，我们都会进行一些修改。这种情况下，我们就像把文章的更新日期也显示处理，也能让读者看的我们写的之前的文章也是有更新的，不会过时的。

**显示更新日期**

　　在 `Next` 主题下添加显示更新时间非常简单，找到**themes/next/_config.yml**的 `post_meta`部分：

```
# Post meta display settings
post_meta:
  item_text: true
  created_at: true
  updated_at: false
  categories: true
```

　　将 `updated_at: false` 修改为 `updated_at: true` 即可。通过 `hexo s -g` 预览，可以看到已经自动添加上了更新日期。

**自定义显示更新日期**

　　对于某些特殊的文章，我们也想能够自定义这个更新的日期。当然，更改起来也非常的简单，Hexo默认就支持更新日期的配置。在每一篇文章的 `Front-matter` 部分，只要添加 `updated` 参数即可。

```
---
date: 2017-05-24 22:07:58
updated: 2017-12-01 10:35:18
---
```

#### 14.去掉文章目录标题的自动编号

　　我们自己写文章的时候一般都会自己带上标题编号，但是默认的主题会给我们带上编号，很是别扭，如何去掉呢？打开**themes/next/_config.yml**，找到

```shell
# Table Of Contents in the Sidebar
toc:
  enable: true

  # Automatically add list number to toc.
  number: false

  # If true, all words will placed on next lines if header width longer then sidebar width.
  wrap: false
```

#### 15.使用gulp压缩资源

在站点执行以下命令

```shell
$ npm install gulp -g
$ npm install gulp-htmlclean gulp-htmlmin gulp-minify-css gulp-uglify gulp-imagemin --save
```

然后查看gulp的安装版本

```shell
$ gulp -v
CLI version: 2.2.0
Local version: 4.0.2
```

如果gulp是3.X的版本，由于函数的写法不同，所以以前的部分博客使用了以下写法，导致报错：

```shell
// 执行 gulp 命令时执行的任务
gulp.task('default', [
    'minify-html', 'minify-css', 'minify-js'
]);
```

错误：AssertionError: Task function must be specified。

gulp4.x本部请在在博客根目录新建**gulpfile.js**文件来编写gulp task对应的函数：

```js
var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');

// 压缩html
gulp.task('minify-html', function() {
    return gulp.src('./public/**/*.html')
        .pipe(htmlclean())
        .pipe(htmlmin({
            removeComments: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
        }))
        .pipe(gulp.dest('./public'))
});
// 压缩css
gulp.task('minify-css', function() {
    return gulp.src('./public/**/*.css')
        .pipe(minifycss({
            compatibility: 'ie8'
        }))
        .pipe(gulp.dest('./public'));
});
// 压缩js
gulp.task('minify-js', function() {
    return gulp.src('./public/js/**/*.js')
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
});
// 压缩图片
gulp.task('minify-images', function() {
    return gulp.src('./public/images/**/*.*')
        .pipe(imagemin(
        [imagemin.gifsicle({'optimizationLevel': 3}),
        imagemin.jpegtran({'progressive': true}),
        imagemin.optipng({'optimizationLevel': 7}),
        imagemin.svgo()],
        {'verbose': true}))
        .pipe(gulp.dest('./public/images'))
});
// 默认任务
gulp.task('default', gulp.parallel(
    'minify-html','minify-css','minify-js','minify-images'
));
```

其中：`gulp.parallel()`是gulp4中的新写法。

生成博文是执行 hexo g && gulp 就会根据 gulpfile.js 中的配置，对 public 目录中的静态资源文件进行压缩。

参考：

[运行gulp项目报错：AssertionError: Task function must be specified。](<https://www.jianshu.com/p/c30ff8592421>)

[利用gulp对Hexo博客压缩并一键之部署](<https://www.jakehu.me/2018/hexo-gulp/>)

[hexo 优化之——使用 gulp 压缩资源](<https://todebug.com/use-gulp-with-hexo/>)

#### 16.设置一键部署

在package.json中加入如下script

```js
"scripts": {

  "push": "hexo cl && hexo g && gulp && hexo d"

}
```

然后在部署的时候只需要运行

```shell
$ npm run push
```

#### 17.文章置顶

　　Hexo博客中，默认的情况是按照时间倒序来排列的，即新发布的文章排在前面。虽然有一种很简单的方法，就是更改文章的发布时间到一个“未来”的时间点，这样虽然能让文章一直置顶，但是给人的体验和感觉是非常不好的。今天介绍一种非常简单而且体验上也非常好的方法。

**安装node插件**

```
$ npm uninstall hexo-generator-index --save
$ npm install hexo-generator-index-pin-top --save
```

**添加标记**

在需要置顶的文章的 `Front-matter` 中加上 `top: true`（top 的值可以是 true，也可以是 n，n 越大代表级别越高） 即可。比如：

```
---
top: true
---
```

**设置置顶标志**

打开：**/themes/next/layout/_macro/post.swig**目录下的文件，定位到 `<div class="post-meta">` 标签下，插入如下代码：

```
{% if post.top %}
  <i class="fa fa-thumb-tack"></i>
  <font color=7D26CD>置顶</font>
  <span class="post-meta-divider">|</span>
{% endif %}
```

#### 18.鼠标点击小红心的设置

　　将 [love.js](https://github.com/Neveryu/Neveryu.github.io/blob/master/js/src/love.js) 文件添加到**\themes\next\source\js\src**文件目录下。修改**\themes\next\layout\\_layout.swing**文件， 在文件的后面、标签之前添加以下代码：

```
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/love.js"></script>
```

#### 19.背景的设置

　　将 [particle.js](https://github.com/Neveryu/Neveryu.github.io/blob/master/js/src/particle.js)文件添加到**\themes\next\source\js\src**文件目录下。修改**\themes\next\layout\\_layout.swing**文件， 在文件的后面、标签之前添加以下代码：

```
<!-- 背景动画 -->
<script type="text/javascript" src="/js/src/particle.js"></script>
```

#### 20.开启阅读进度记录

**themes/next/_config.yml**

~~~shell
# Automatically scroll page to section which is under <!-- more --> mark.
# 自动将页面滚动到<!-- more -->标记下的地方。
scroll_to_more: true

# Automatically saving scroll position on each post/page in cookies.
# 自动保存每篇文章或页面上一次滚动的地方。
save_scroll: true

# Automatically excerpt description in homepage as preamble text.
# 自动在首页对文章进行摘要描述作为前言文本。
excerpt_description: true

# Automatically Excerpt. Not recommend.
# Please use <!-- more --> in the post to control excerpt accurately.
# 不推荐使用自动摘要。
# 请在文章中使用<!-- more -->标志来精确控制摘要长度。
auto_excerpt:
  enable: true
  length: 200
~~~

#### 21.添加文章字数统计

一般为了让读者大概估计阅读文章的时间，有的文章在头部会显示总的字数统计。

**启用字数统计**

首先安装一个依赖插件：

```
npm i --save hexo-wordcount
```

然后修改**themes/next/_config.yml**中的 `post_wordcount` 部分：

```
# Post wordcount display settings
# Dependencies: https://github.com/willin/hexo-wordcount
post_wordcount:
  item_text: true    	//底部是否显示“总字数”字样
  wordcount: false   	//文章字数统计
  min2read: false    	//文章预计阅读时长（分钟）
  totalcount: false  	//网站总字数，位于底部
  separated_meta: true 	//是否将文章的字数统计信息换行显示
```

#### 22.使用LeanCloud添加文章阅读次数统计

参考：[为NexT主题添加文章阅读量统计功能](https://notes.doublemine.me/2015-10-21-为NexT主题添加文章阅读量统计功能.html#配置LeanCloud)

2019年6月20日，[LeanCloud](https://leancloud.cn/)主站访问异常，统计的api访问失效：`https://cdn1.lncld.net/static/js/av-core-mini-0.6.4.js`，导致博客加载非常缓慢。最后替换域名为：`https://c.lcfile.com/static/js/av-core-mini-0.6.4.js`，把js下载到本地，按照参考博客更改配置，博客加载缓慢问题才得以解决。如果觉得出现这种问题非常麻烦，可以使用不蒜子统计文章阅读次数。

官方说明：

我们监测到从今天（06/20）下午开始各个地区陆续出现部分网络无法解析华北节点的 api.leancloud.cn 以及 *.lncld.net 域名的问题。通过和我们的域名注册商阿里云沟通，得知他们接到有关部门行政命令将一批域名设置为 ClientHold 状态，其中包括 leancloud.cn 和 lncld.net，但是没有可执行的其它信息可以提供给我们。目前我们仍在和阿里云沟通中。

参考：[关于 LeanCloud 国内域名解析问题的情况更新（6 月 21 日）](https://blog.avoscloud.com/6841/)

解决：[Hexo阅读量api.leancloud.cn解析失败](https://blog.ifiveplus.com/Hexo%E9%98%85%E8%AF%BB%E9%87%8Fapi-leancloud-cn%E8%A7%A3%E6%9E%90%E5%A4%B1%E8%B4%A5.html)

#### 23.使用不蒜子统计访问次数

站点访问计数有名的就是[不蒜子 - 极简网页计数器](<https://busuanzi.ibruce.info/>)，使用起来非常方便。

**主题集成步骤**

其实，next主题已经集成不蒜子统计工具。但是因为主题使用的旧的域名解析，需要更换过来。

1. 更换域名。打开**themes/next/layout/_third-party/analytics/busuanzi-counter.swig**，更换域名：

`<script async src="https://dn-lbstatics.qbox.me/busuanzi/2.3/busuanzi.pure.mini.js"></script>`

更换为：

`<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>`

2. 更改配置

打开主题配置文件**themes/next/_config.yml**，修改

~~~shell
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: false
  site_uv_header: <i class="fa fa-user"></i> 访客数
  site_uv_footer: 人
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: <i class="fa fa-eye"></i> 总访问量
  site_pv_footer: 次
  # custom pv span for one page only
  page_pv: true
  page_pv_header: <i class="fa fa-file-o"></i>
  page_pv_footer: 次阅读
~~~

**官网安装步骤**

1. 安装脚本。打开 **themes/next/layout/_partial/footer.swig**，添加脚本：

```
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js">
</script>
```

2. 显示站点总访问量

**themes/next/layout/_partial/footer.swig**

要显示站点总访问量，复制以下代码添加到你需要显示的位置。有两种算法可选：

算法a：pv的方式，单个用户连续点击n篇文章，记录n次访问量。

```
<span id="busuanzi_container_site_pv">
    本站总访问量<span id="busuanzi_value_site_pv"></span>次
</span>
```

算法b：uv的方式，单个用户连续点击n篇文章，只记录1次访客数。

```
<span id="busuanzi_container_site_uv">
  本站访客数<span id="busuanzi_value_site_uv"></span>人次
</span>
```

3. 显示单页面访问量

要显示每篇文章的访问量，复制以下代码添加到你需要显示的位置。

算法：pv的方式，单个用户点击1篇文章，本篇文章记录1次阅读量。

```
<span id="busuanzi_container_page_pv">
  本文总阅读量<span id="busuanzi_value_page_pv"></span>次
</span>
```

备注：代码中文字是可以修改的，只要保留id正确即可。

#### 24.绑定域名

[使用hexo+github搭建免费个人博客详细教程](<https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html>)

#### 25.SEO优化

　　SEO优化对于网站是否能被搜索引擎快速收录有很大帮助，因此适当做一些SEO还是有必要的。但是请注意，因为github是不允许百度的spider爬取github上的内容的，所以如果想让你的站点被百度收录，只能使用自己购买的域名。谷歌对此没有限制。

**首先修改站点URL**

**_config.yml**

~~~shell
url: https://helloliwen.github.io
~~~

**添加 sitemap 插件**

安装 hexo-generator-sitemap 插件：

```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```

配置（编辑 **_config.yml**）：

```
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```

注意：这个地方的空格要符合语法规范！

- 提交sitemap。参考next主题官方解答：[添加 Google Webmaster tools 验证](https://github.com/iissnan/hexo-theme-next/wiki/添加-Google-Webmaster-tools-验证)

- 配置成功后，hexo编译时会在hexo站点根目录生成sitemap.xml和baidusitemap.xml。其中sitemap.xml适

  合提交给谷歌搜素引擎，baidusitemap.xml适合提交百度搜索引擎。

- 其次，在robots.txt中添加下面的一段代码：

  ```
  Sitemap: <your-domain-name>/sitemap.xml
  Sitemap: <your-domain-name>/baidusitemap.xml
  ```

- 参考这篇文章：[hexo干货系列：（六）hexo提交搜索引擎（百度+谷歌）](http://www.cnblogs.com/tengj/p/5357879.html) 提交sitemap.xml

**添加蜘蛛协议 robots.txt**

新建 **source/robots.txt**：

```
User-agent: *
Disallow: /CNAME
Disallow: /README

Allow: /
Allow: /about/
Allow: /archives/
Allow: /categories/
Allow: /tags/

Allow: /css/
Allow: /images/
Allow: /js/
Allow: /lib/

Sitemap: <your-domain-name>/sitemap.xml
```

**Hexo NexT主题首页title的优化**

更改文件：**\themes\next\layout\index.swig**，将下面代码

```
{% block title %} {{ config.title }} {% endblock %}
```

改成

```
{% block title %} {{ config.title }} - {{ theme.description }} {% endblock %}
```

这时候你的首页标题会更符合`网站名称 - 网站描述`这习惯。

进阶，做了[seo](http://www.arao.me/tags/seo/)优化，把关键词也显示在Title标题里，可改成

```
{% block title %} {{ theme.keywords }} - {{ config.title }} - {{ theme.description }} {% endblock %}
```

注意：别堆砌关键字，整个标题一般不超过80个字符，可以通过chinaz的seo综合查询检查。

**其他SEO优化**

　　SEO优化应该说是一个收益延迟的行为，可能你做的优化短期内看不到什么效果，但是一定要坚持，SEO优化也是有很深的可以研究的东西，从我们最初的网站设计，和最基础的标签的选择都有很大的关系，网站设计就如我们刚刚说的，要让用户点击三次可以到达网站的任何一个页面，要增加高质量的外链，增加相关推荐（比如说我们经常见到右侧本站的最高阅读的排名列表），然后就是给每一个页面加上keyword和描述在代码中，我们应该写出能让浏览器识别的语义化HTML，这样有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；并且对外链设置nofollow标签，避免spider爬着爬着就爬出去了（减少网站的跳出率），并且我们要尽量在一些比较大的网站增加我们站点的曝光率，因为spider会经常访问大站，比如我们在掘金等技术社区发表文章中带有我们的站点，这样spider是很有可能爬到我们中的站点的，so....

- 网站**外链**的推广度、数量和质量

- 网站的**内链**足够强大

- 网站的**原创**质量

- 网站的**年龄**时间

- 网站的**更新频率**（更新次数越多越好）

- 网站的**服务器**

- 网站的**流量**：流量越高网站的权重越高

- 网站的**关键词排名**：关键词排名越靠前，网站的权重越高

- 网站的**收录**数量：网站百度收录数量越多，网站百度权重越高

- 网站的浏览量及深度：**用户体验**越好，网站的百度权重越高

参考：

[HEXO SEO 高级优化](http://www.langzi.fun/HEXO-SEO 高级优化.html)

[hexo高阶教程：SEO优化、代码同时托管github和coding、多终端编辑hexo博客、使用gulp压缩你的代码、增加七牛图床](<https://juejin.im/post/590b451a0ce46300588c43a0>)


#### 26.添加链接持久化

　　SEO搜索引擎优化认为，网站的最佳结构是**用户从首页点击三次就可以到达任何一个页面**，但是我们使用hexo编译的站点打开文章的url是：sitename/year/mounth/day/title四层的结构，这样的url结构很不利于SEO，爬虫就会经常爬不到我们的文章，于是，我们可以将url直接改成sitename/title的形式，并且title最好是用英文。

　　hexo 默认的链接是http://xxx.yy.com/2013/07/14/hello-world这种类型的，这源于站点配置文件config.yml里的配置: permalink: :year/:month/:day/:title/。这种默认配置的缺点就是当我们创建的博文名包含中文的名的时候，url 链接地址经常会变成一串很长的难以理解的字符串，不利于博文的链接分享，以及搜索引擎搜索，另外就是年月日都会有分隔符。我们可以让 url 链接持久化来解决这个问。

（1）安装hexo-abbrlink插件

~~~shell
$ npm install hexo-abbrlink –save
~~~

（2）修改站点配置文件**_config.yml**：permalink: post/:abbrlink.html

添加 abbrlink:

~~~shell
permalink: post/:abbrlink.html  # :year/:month/:day/:title/     # 文章的永久链接格式
permalink_defaults:     # 永久链接中个部分的默认值
# abbrlink config 需安装插件hexo-abbrlink
abbrlink:
  alg: crc32  # 算法： crc16(default) and crc32
  rep: hex    # 进制： dec(default) and hex
~~~

#### 27.添加评论系统

推荐LeanCloud+Valine

[在 NexT 中使用 Valine 评论系统](https://cloud.tencent.com/developer/article/1578662)

[Hexo-NexT 配置 Valine](https://tding.top/archives/ed8b904f.html)

[Hexo 集成 Valine 评论系统](https://www.jianshu.com/p/b9e73c881729)

[Hexo博客(14)添加来必力评论系统](<http://masikkk.com/article/hexo-14-livere-comment/>)

#### 28.开启打赏功能

编辑 **themes/next/_config.yml**：

```
reward_comment: 坚持原创技术分享，您的支持将鼓励我继续创作！
wechatpay: /images/wechatpay.jpg
alipay: /images/alipay.jpg
```

### 六、其他

#### 1.自己安装插件一览

~~~shell
$ npm list --depth 0
hexo-site@0.0.0 D:\java\hexo
+-- gulp@4.0.2
+-- gulp-htmlclean@2.7.22
+-- gulp-htmlmin@5.0.1
+-- gulp-imagemin@5.0.3
+-- gulp-minify-css@1.2.4
+-- gulp-uglify@3.0.2
+-- hexo@3.7.1
+-- hexo-abbrlink@2.0.5
+-- hexo-autonofollow@1.0.1
+-- hexo-deployer-git@0.3.1
+-- hexo-generator-archive@0.1.5
+-- hexo-generator-baidu-sitemap@0.1.5
+-- hexo-generator-category@0.1.3
+-- hexo-generator-index@0.2.1
+-- hexo-generator-index-pin-top@0.2.2
+-- hexo-generator-searchdb@1.0.8
+-- hexo-generator-sitemap@1.2.0
+-- hexo-generator-tag@0.2.0
+-- hexo-renderer-ejs@0.3.1
+-- hexo-renderer-marked@0.3.2
+-- hexo-renderer-stylus@0.3.3
`-- hexo-server@0.3.3
~~~

更新插件

~~~shell
npm update
~~~

#### 2.关于npm

npm小知识

　　npm（node package manager）nodejs的包管理器，用于node插件管理（包括安装、卸载、管理依赖等）。使用npm安装插件：`npm install <name> [g] [--save -dev]`

- `<name>`:node 插件名称
- `-g`:全局安装，会在node安装的根目录下载对应的包，在计算机的任何文件都可以使用该插件，默认的node安装目录是：`C:\Users\Administrator\AppData\Roaming\npm`;如果不带该属性，将会安装在当前目录，下载安装包的位置是当前目录的`node_modules`文件夹
- `--save`：将配置信息保存在node项目配置文件`package.json`中
- `-dev`：保存至`package.json`的devDependencies节点，如果没有该属性，该插件将会被保存至dependencies节点，devDependencies和dependencies有什么区别呢？其实从名字就应该可以看出来两者的区别，devDependencies中dev是development（开发）的缩写，dependencies是依赖的意思。所以 dependencies 是程序正常运行所需要安装的依赖，而devDependencies是开发所需要的依赖，比如一些单元测试的包~
- 为什么要保存至package.json？因为我们使用node的时候需要很多的包，所以我们将我们的配置信息，也就是我们需要包的名称等其他信息保存至一个文件中，如果说其他开发者就可以直接使用一个命令就可以安装和我们相同的配置，这个命令就是`npm install`，就可以下载`package.json` 下所有需要的包。`npm install --production`则只下载dependencies下的包

使用npm卸载插件：`npm unstall <name> [-g] [--save-dev]`

- 在npm中要卸载插件不是将文件夹删除就可以了，因为你的配置信息还在package中，所以要使用`npm unstall <name> [-g] [--save-dev]` 命令
- 删除全部插件:`rimraf node_modules`（首先你需要先安装rimraf 插件）

更新npm插件：`npm update <name> [g] [--save-dev]`

使用cnpm

　　什么是cnpm呢，大家都知道，由于不可描述原因，我们访问国外的资源有时候的速度，大家懂的，所以淘宝除了一个npm镜像，服务器就在中国。c可以理解为China（应该可以这样理解吧）,cnpm使用方法和npm完全相同，只需将npm全部换成cnpm就可以。本文都是使用的npm，如果想要尝试cnpmde的麻烦自行替换~

> 这是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。

cnpm 官网地址：[npm.taobao.org；](https://link.juejin.im?target=http%3A%2F%2Fnpm.taobao.org；)
安装命令为`npm install cnpm -g --registry=https://registry.npm.taobao.org`

> 注意：安装完后最好查看其版本号`cnpm -v`或关闭命令提示符重新打开，安装完直接使用有可能会出现错误；

#### 3.参考

* 官网

[Hexo](<https://hexo.io/zh-cn/>)

[NexT](<http://theme-next.iissnan.com/>)

- 博客搭建

[git使用ssh密钥](http://liujinkai.com/2015/09/18/git-use-ssh/?utm_source=tuicool&utm_medium=referral)

[github设置添加SSH](https://www.cnblogs.com/ayseeing/p/3572582.html)

[使用hexo+github搭建免费个人博客详细教程](<https://www.cnblogs.com/liuxianan/p/build-blog-website-by-hexo-github.html>)

[我是如何利用Github Pages搭建起我的博客，细数一路的坑](https://www.cnblogs.com/jackyroc/p/7681938.html)

[Hexo搭建博客教程](https://thief.one/2017/03/03/Hexo搭建博客教程/)

* 主题配置

[Hexo 使用入门](http://cqwdc.com/post/1476ebdb.html)

[Hexo的Next主题详细配置](<https://www.jianshu.com/p/3a05351a37dc>)

[动动手指，NexT主题与Hexo更搭哦（基础篇）](<http://www.arao.me/2015/hexo-next-theme-optimize-base/>)

[hexo之next主题优化整理](<http://michael728.github.io/2015/11/30/hexo-next-optimize/>)

* SEO优化

[让Google搜索到搭建在Github Pages上的博客](<https://jactor-sue.github.io/zh-CN/how-blog-on-githubpages-can-be-searched-by-google/>)

[动动手指，不限于NexT主题的Hexo优化（SEO篇）](<http://www.arao.me/2015/hexo-next-theme-optimize-seo/>)

- Markdow语法

[Markdown——入门指南](<https://www.jianshu.com/p/1e402922ee32/>)

[Markdown语法汇总](<https://www.jianshu.com/p/45faddb1526d>)

<center style="font-weight:bold">（完）</center>
