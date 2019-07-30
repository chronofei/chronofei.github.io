---
title: 玩转Hexo
date: 2019-05-29 09:10:01
categories: 技术总结
tags: 
 - hexo
 - git
 - github
---


## 安装Hexo

#### 安装Node.js

* Nodejs的安装建议参考[官网](https://nodejs.org/en/) 。官网中给出几种安装方式，可以根据需要选择。

#### 安装Git

* Linux(Ubuntu, Debian):
``` bash
$ sudo apt-get install git
```

#### 安装Hexo

* 用npm安装hexo
``` bash
$ npm install -g hexo-cli
```
 注：关于Hexo的入门教程可以参考[官网文档](https://hexo.io/zh-cn/)。


## 常用Hexo命令

### Hexo子命令

* init
```bash
$ hexo init [destination]
```
 在指定的文件夹或当前文件夹（destination没有指定）下新建一个Hexo网站。

* new
```bash
$ hexo new [layout] <title>
```
 新建一篇博客。如果没有指定layout，则使用_config.yml中的default_layout参数代替。如果标题中包含空格，则使用引号（单引号或者双引号）引起来。
```bash
$ hexo new "Hello World"
```

* generate
```bash
$ hexo generate
```
 根据配置生成静态网页文件。

* publish
```bash
$ hexo publish [layout] <filename>
```
 发表草稿

* server
```bash
$ hexo server
```
 启动服务器。默认情况下，访问网址为：`http://localhost:4000/`

* deploy
```bash
$ hexo deploy
```
 将网站部署到托管平台


* clean
```bash
$ hexo clean
```
 清除缓存文件（db.json）和已生成的静态文件（publish）。在某些情况下（尤其是更换主题后），如果发现对站点的更改无论如何也不生效时，可以运行该命令。

* list
```bash
$ hexo list <type>
```
 列出网站资料。

* version
```bash
$ hexo version
```
 显示Hexo版本。


注：以上命令部分有相应的简写命令及选项参数，可以通过`hexo help`命令查看。



### 命令选项

* 安全模式
```bash
$ hexo --safe
```
 在安全模式下，不会载入插件和脚本。在安装新插件遭遇问题时，可以尝试以安全模式重新执行。

* 调试模式
```bash
$ hexo --debug
```
 在终端中显示调试信息并记录到debug.log文件中。碰到问题时，可以尝试用调试模式重新执行一次，并提交调试信息到[Github](https://github.com/hexojs/hexo/issues/new)上。

* 简洁模式
```bash
$ hexo --slient
```
 隐藏终端信息。

* 自定义配置文件路径
```bash
$ hexo --config custom.yml
```
 自定义配置文件的路径，执行后将不再使用\_config.yml。

* 显示草稿
```bash
$ hexo --draft
```
 显示source/\_draft文件夹中的草稿文章。

* 自定义CWD
```bash
$ hexo --cwd /path/to/cwd
```
 自定义当前工作目录的路径。



## Hexo标准文件

执行初始化命令`hexo init [destination]`时，需要在一个空文件夹中，否则会报错。成功执行此命令后，会在文件夹中生成一系列Hexo标准文件:

* \_config.yml
 网站配置信息，可以在此文件中配置大部分参数。
* package.json
 应用程序信息。
* scaffolds
 模板文件夹。新建文章、草稿、网页时，Hexo会根据scaffold来建立。
* source
 存放用户资源。
* themes
 主题文件夹，网页主题主要存储在此文件夹下。Hexo会根据主题生成静态页面。



## 配置Git

### 注册GitHub
* Git是最好用的分布式版本控制系统，它的一大优势就是为用户提供了免费的代码托管平台——[GitHub](https://github.com/)。
* 在GitHub的首页，可以免费注册。Username为用户名、Email为用户登陆邮箱、Password为登陆密码。
* 对于Git的学习可以参考[廖雪峰](https://www.liaoxuefeng.com/wiki/896043488029600)老师的教程。

### 创建Repository
* 创建个人GitHub帐号并登陆后，在网页右上角有一加号图标，点击并选择 `New repository`。
* 在Repository name处填写 Username.github.io。其中Username为注册GitHub帐号时填写的用户名。
* 点击` Create repository` 完成repository创建
* 注意：
 * 用户使用GitHub托管代码时，可以任意指定 Repository name，但是，用于托管Hexo静态网页时，则必须为Username.github.io。
 * 不要选择 Initialize this repository with a README。

### 配置SSH keys
* 运行` cd ~/.ssh `命令检查电脑上有没有SSH Key，如果返回“No such file or directory”说明电脑上没有SSH Key
* 运行`ssh-keygen -t rsa -C "email@example.com"`创建新的SSH密钥。回车后系统会提示输入密码，不用理会，直接四次回车完成创建。创建完成后，会在本地主文件目录下生成.ssh目录，目录下有三个文件：id\_rsa、id\_rsa.pub、known\_hosts。
* 进入你的GitHub主页面，网页右上角用户图标，点击选择`Settings`，网页左侧选择 `SSH and GPG keys`，点击`New SSH key`，将本地`~/.ssh/id_rsa.pub`文件里面的内容复制到`Key`框中，在`Title`框中选择填写对key的描述，最后点击`Add SSH key`。

### 测试
运行以下命令：
```bash
$ ssh -T git@github.com
```
得到如下反馈信息：
```
The authenticity of host 'github.com (207.97.227.239)' can't be established.RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.Are you 
sure you want to continue connecting (yes/no)?
```
选择`yes`
```
Hi Username! You've successfully authenticated, but GitHub does not provide shell access.
```
说明配置成功！

### 设置用户信息
关于Git的配置可以参考[Pro Git](https://git-scm.com/book/zh/v1/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE)。此处仅介绍用户配置：
```bash
$ git config --global user.name "Username"
$ git config --global user.email email@example.com
```




## 在GitHub上部署Hexo网页

* 安装Git插件[hexo-deployer-git](https://github.com/hexojs/hexo-deployer-git)。
```bash
$ npm install hexo-deployer-git --save
```

* 修改配置文件。
```
deploy:
	type: git
	repo: <repository url> 库地址
	branch: [branch] 分支名称
	message: [message] 自定义提交信息
```

* 部署Hexo网页到GitHub上
```bash
$ hexo clean
$ hexo generate
$ hexo deploy
```

* 访问个人博客
 网页部署到GitHub上以后，就可以通过浏览器访问 https://Username.github.io 查看自己博客了。






## 源文件管理

* Git管理Hexo文件
 将网页部署到GitHub后，进入GitHub的相应Repository，可以看到GitHub中仅有Hexo生成的静态网页，而Hexo的源码文件则没有部署。由于缺失Hexo源文件，导致无法实现多台电脑同步部署网页。因此需要考虑其他方式，来实现Hexo源文件的托管。最简单的方式就是在GitHub上新建一个Repository，用来托管Hexo源文件，当需要在其他电脑中修改Blog时，只需要在该Repository中clone源文件，修改后部署网页，再提交源文件。这种方式较为实用，但作为程序员，有点侮辱智商。推荐使用在原Repository（Username.github.io）中新建分支的方式。
```bash
$ mkdir ~/example  新建演示文件夹
$ cd ~/example 
$ git init 使用Git初始化文件夹
$ mkdir hexo 新建文件夹，用于存放hexo源文件
$ cd hexo
$ hexo init 使用hexo初始化文件夹
$ ... 随心所欲执行用户想要的命令。想要托管源文件时，最后离开该文件夹时，建议执行下hexo clean命令，清楚缓存文件。
$ ... 该文件夹下也有.gitignore文$ 件用于忽略非托管文件
$ cd ..
$ git branch hexo 新建分支
$ git checkout hexo 进入分支
$ git add .
$ git commit -m "hello world"
$ git remote add origin git@github:Username/Username.github.io.git 
$ git push origin hexo 此处要提交hexo分支
```

* 本地分支管理
 执行`git init`后默认只有一个mast分支，而GitHub中Username.github.io仓储库的mast分支用来部署Hexo的静态网页，因此托管Hexo源文件需要新建一个分支，此时不需要在GitHub网页上新建，仅需要在本地新建一个hexo分支，然后push到GitHub远程仓库中。
* Github设置主分支
 虽然将Hexoi源文件托管到GitHub仓库中，然而，在其他电脑上执行`git clone git@github.com:Username/Username.github.io.git`命令时，默认clone GitHub中的Default branch，而Repository的默认default branch为master，因此需要在GitHub的Username.github.io Repository中，选择 Settings ，左侧选择 Branches，修改Default branch为hexo。这样在本地clone Repository时，则会将hexo分支的内容clone到本地。
* 尝试clone源文件
 在本地执行clone命令，并进入hexo文件夹下，执行hexo子命令，发现如下错误提示。
```
ERROR Local hexo not found in ~/Username.github.io/hexo
ERROR Try running: 'npm install hexo --save'
```
 按照提示重新安装npm，同时需要部署网页时，同样需要重新安装Git插件。
```bash
$ npm install hexo --save
$ npm install hexo-deployer-git --save
```


注：Hexo源文件的管理可以参考[多台电脑使用Hexo](https://www.jianshu.com/p/4bcf2848b3fc)。




## 更换主题


* 选择主题
对于博客主题，个人感觉Hexo的默认主题 landscape 不太美观，因此想要换掉。对于主题的挑选可以去[Hexo官网](https://hexo.io/zh-cn/index.html)去找，基本每个主题都有对应的GitHub地址和安装方式。还可以参考知乎上的回答——[有哪些好看的 Hexo 主题？](https://www.zhihu.com/question/24422335)


* 安装主题
 1. 下载主题——可以参考Hexo的[GitHub](https://github.com/iissnan/hexo-theme-next)主页面 
  ```bash
  $ cd hexo
  $ ls
  _config.yml  node_modules  package.json  public  scaffolds  source  themes
  $ git clone https://github.com/iissnan/hexo-theme-next themes/next
  ```
 2. 启用NexT主题
  clone完Next主题后，打开站点配置文件\_config.yml，找到`theme`字段，将其值更改为`next`。
 3. 验证主题是否启用
   运行以下命令：
   ```bash
   $ hexo clean
   $ hexo generate
   $ hexo server
   ```
   启动服务时，也可以进入调试模式`hexo s --debug`，访问`http://localhost:4000`，确保站点正常运行。


* 配置
  可分别在站点配置文件和主题配置文件中对博客进行配置，相应配置选项可分别在相应配置文件中找到相应配置字段进行设置。参考[Hexo使用攻略-添加分类及标签](https://linlif.github.io/2017/05/27/Hexo%E4%BD%BF%E7%94%A8%E6%94%BB%E7%95%A5-%E6%B7%BB%E5%8A%A0%E5%88%86%E7%B1%BB%E5%8F%8A%E6%A0%87%E7%AD%BE/), 添加“分类”和“标签”选项：
  * 生成“分类”页并添加type属性
    执行命令
    ```bash
    $ hexo new page categories
    ```
    成功后提示：
    ```
    INFO  Created: ~/Documents/blog/source/categories/index.md
    ```
    按照路径打开index.md文件，添加 type: "categories" 到内容中，保存并关闭。
  * 在hexo/source/\_posts文件夹下打开一个.md文件，并在文章的Frond-master部分添加categories属性。
  * 添加“标签”选项：添加标签选项的步骤的添加分类的步骤相同，在相应操作下将categories替换为tags即可。


* 注意事项
  注：因为NexT主题为一独立项目，因此，在hexo上层目录中执行`git add .`命令时，并不会提交NexT主题目录下的更改，
当向远程仓储库提交原代码时，在远程仓储库的origin/hexo/themes/next目录下什么都没有，针对这种情况，本博将在提交
代码前，将next整个目录压缩成一个.zip文件，然后在hexo上层目录中执行`git add .`时，则可以提交相应的更改。当在远程将源文件clone到本地时，再解压缩就可以了。
