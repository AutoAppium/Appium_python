# 一、windows下Python+Appium自动化环境安装步骤
  windows下只能做android的手机自动化，ios手机的自动化需要用到xcode等依赖ios系统的工具，如果实在想用windows做自动化可以搭建虚拟机来做，不过虚拟机对windows电脑的性能要求较高，否则会很卡。
  ## 1. 安装前提
  ### 硬件：
    windows电脑一台
    Android手机一部
  ### 软件：
    1. 操作系统： win7，win10等
    2. python3.4及以上 https://www.python.org/downloads/(配置环境变量）
    3. pycharm 2017.1及以上版本（Community版本和Professional版本都可以）
    https://www.jetbrains.com/pycharm/download/previous.html
    4. 安装JDK，配置环境变量：JAVA_HOME - D:\Program Files\Java\jdk1.8.0_121
    CLASSPATH - %JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
    PATH - %JAVA_HOME%\jre\bin;%JAVA_HOME%\bin
  
  上述软件都准备好后，则进入搭建步骤。
  ### 2. 安装步骤：
    1. 下载安装Android SDK
      下载地址：http://developer.android.com/sdk/index.html
      
    2. 配置SDK：
      # 新建ANDROID_HOME  D:\ProgramFiles (x86)\Android\android-sdk，
      # 在PATH中添加：%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools;
      
    3. Install Android SDK Packages
      # 进去 android-sdk 文件夹下，打开 SDK Manager. D:\Program Files (x86)\Android\android-sdk\SDK Manager.exe
      # 建议勾上所有最近版本的SDK Tools, Platform Tools以及几个之前版本的Build Tools. 最新的5个APIs. 如果你的安卓设备是个更老版本的，或者要测得app只支持某一个更老版本的Android，还要下载更老的Android版本。如果硬盘不是问题的话，安装越多的package/versions会比较好。
      # 选择每一个分支并点击Accept License，所有的package都是勾上的状态，然后点击Install
      # 等待所有的package下载安装完成。
      # 安装Intel Hardware Accelerated Execution Manager为了避免Android虚拟设备创建过程中发生错误。
      下载地址：https://software.intel.com/en-us/android/articles/intel-hardware-accelerated-execution-manager-end-user-license-agreement 
      下载后解压并执行intelhaxm-android.exe文件 
      
    4. 下载安装Nodejs
      # 下载地址：https://nodejs.org/en/
      # 需要配置环境变量，在PATH中添加：D:\Program Files\nodejs;
      
    5. 下载安装Appium
      下载地址：http://appium.io/downloads.htmlom
      # 需要配置环境变量 D:\Program Files (x86)\Appium\node_modules\.bin;
      # 配置好后，启动cmd，
      # 输入node -v，查看node安装版本
      # 输入appium-doctor检查appium的安装环境是否成功,出现'All checks were successfully.' 就安装成功了。
  
    6. 选择Python版本的Lib: Appium-Python-Client-0.22.tar.gz
    7. 由于Appium依赖于Selemium,所以还要下载 Selemium Lib: selenium-2.53.2.tar.gz   https://pypi.python.org/pypi/selenium
 
 ### 启动Appium，真机运行
    1) 启动Appium
    打开命令行，输入appium， 显示成功启动：
    2）连接Android手机
    3）编写客户端代码
    假设我们的代码放在目录E:\Test\AppiumDemo 中。首先把 Appium-Python-Client-0.22.tar.gz 里面的 appium 目录解压到AppiumClientPython 中， 把 selenium-2.53.2.tar.gz里面的 selenium 目录解压到AppiumClientPython中。
    4）创建文件demo_appium.py , 编辑内容：
      #coding=utf-8
      from appium import webdriver
      desired_caps = {}
      desired_caps['platformName'] = 'Android'
      desired_caps['platformVersion'] = '6.0.1'
      desired_caps['deviceName'] = 'Mi Max'
      desired_caps['appPackage'] = 'com.android.calculator2'
      desired_caps['appActivity'] = '.Calculator'
      driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)
      driver.find_element_by_name("1").click()
      driver.find_element_by_name("+").click()
      driver.find_element_by_name("6").click()
      driver.find_element_by_name("=").click()
      driver.quit()
    5）运行
    打开命令行，cd到E:\PythonTest\AppiumClientPython 中，运行 python hello_appium.py, 正常情况可以看到手机按照代码控制，打开计算器，逐个点击按钮完成计算。


# 二、IOS下Appium自动化环境安装步骤
  ## 1. 安装前提

  ### 硬件：
    IOS手机一部
    Macbook笔记本一台

  ### 软件：
    1. OS：MacOS Sierra10.13以上
    2. 

  ## 2. Android测试安装步骤

  ## 3. IOS真机测试安装步骤 
  git快速入门-笔记(MD格式)
http://www.php.cn/code/9058.html
git是一种版本控制器。原来就是针对linux系统。
下载安装
- https://git-scm.com/download/
- Git Bash git命令行界面
- Gi GUI 图形界面操作
- **Ubuntu，debian系统**：sudo apt-get install git
- **centos，Redhat系统**：yum install git

git使用前配置
- git config --global user.name 你的名字 #是谁
- git config --global user.email 你的email #怎么联系

代码管理
创建版本库
- cd e:/
- mkdir test
- git init #版本库初始化，会生产.git

**注意：**
- 不要把仓库建在中文目录下
- .git是个隐藏目录，不要随意修改

添加(提交)新建文件
在上面创建本地库e:/test下
创建文件，比如：index.php
- git status 查看仓库状态
- git add index.php
把index.php从**工作区**提交到暂存区
- git status
**每次提交操作后，都要查看状态**
- git commit -m "提交文件说明"
把index.php提交到**版本库**
分区操作及状态变化
- 分区：工作区(开发)-->暂存区-->版本库
- 状态：红色显示文件--> 绿色 -->没有显示
- 操作：-----git add 文件--git commit -m "说明"

```
graph LR
A[工作区] --git add--> B[暂存区]
B --git commit -m -->C[版本库]
```

修改文件
- 修改文件的提交和新增文件提交操作流程是一样的

删除文件
- git rm foo.php
#文件已经提交到版本库的文件删除
- git commit -m “删除r.txt”
#删除文件提交确认

远程仓库 管理
码云 https://git.oschina.net
github https://github.com
所有git模式的在线网站都适用
create a new repository on the command line，远程提交
- echo "# test" >> README.md
- git init
- git add README.md
- git commit -m "first commit"
- git remote add origin https://github.com/xxx/test.git
- git push -u origin master

push an existing repository from the command line， 远程提交
- git remote add origin https://github.com/xxx/test.git
- git push -u origin master

团队合作开发
在线设置 参与者 collaborators

default branch
- **The default branch is considered the “base” branch in your repository,
against which all pull requests and code commits are automatically made,
unless you specify a different branch.**
- 译文：默认的分支被认为是存储库中的“基础”分支，所有的拉请求和代码提交都是自动生成的，
除非您指定了一个不同的分支。

#### Protected branches
- Protect branches to disable force pushing, prevent branches from being deleted,
and optionally require status checks before merging.
- 保护分支以禁用强制推送，防止分支被删除，并且在合并之前需要进行状态检查。
#### 将远程服务器仓库更新过的代码拉到本地仓库
- git pull origin master (origin需要定义)

### git的特点
#### 分布式版本控制器
- 每台电脑就是一台服务器
- 使用可以不用联网(联网是为了相互同步)
#### 工作区和版本区
```
graph LR
A[工作区] --git add--> B[暂存区]
B --git commit -m -->C[版本库]
```
#### 改动日志
- git log #查看详细日志
- git log --pretty=oneline #单行查看日志

#### 版本切换
- git reflog #查看版本变化
- git reset --hard HEAD^ 切换到前1版本
- git reset --hard HEAD@{3} 切换到指定版本
- git reset --hard 988dea2 切换到指定版本

### 分支管理
- master即为代码的主干分支,这里代码不要轻易修改,尽量修改分支,然后合并到master;

#### 查看分支
- git branch #查看所有分支
* master #带*的分支为当前分支;
- git branch dev #创建dev分支

#### 切换分支
- git checkout dev #切换到dev分支
切换分支的新增和修改文件,必须进行添加git add和提交git commit -m;
- git branch #再次查看分支
- git checkout master #再切换到master

#### 合并分支
- git checkout mater #切换到主分支
- git merge dev #合并dev分支到当前master主干分支
- 合并分支可能会有特定文件的CONFLICT(content)冲突提示; 并显示自动合并失败
(automatic merge failed) 如果多个分支修改了同一个文件,合并后, 该文件可能存在冲突,
手动修改一下文件即可

### 远程仓库
(方便操作,实际上可以直接使用远程库地址)
#### 查看远程仓库
- 查看远程仓库:git remote
- 查看仓库地址: git remote -v

#### 添加远程库别名
- git remote add <远程库名> <远程仓库地址>
- 如: git remote add origin https://git.oschina.net/xxx/test.git
#远程库名一般叫origin,但并非强制,可以自定义

#### 删除远程库别名
- git remote remove <远程库名>
- 如:git remote remove origin

#### 修改远程库别名
- git remote rename <旧名称> <新名称>

### 公钥登陆
push本地仓库到远程时,总要输入用户名/密码,很不方便. 配置公钥,可以避免平方输入用户名和密码.
1. 配置ssh格式的远程仓库地址
-git remote add 远程仓库名 远程仓库地址
-git remote add gitaddr git@git.oschina.net:xxx/test.git
2. 创建ssh key
ssh-keygen -t rsa -C "youremail@example.com", 把邮件地址换成自己的邮件地址,一直回车,
不用输入密码,完成后,可以在用户主目录里找到.ssh目录,内有id_rsa和id_rsa.pub两个文件.
id_rsa是私钥,id_rsa.pub是公钥.
这两把钥匙是成对的,可以让分别持有私钥和公钥的双方相互认识.
3. 把公钥放在服务器
用记事本打开id_rsa.pub,复制公钥内容.
登陆git.oschina.net,ssh公钥处填入公钥并保存.
这样可以免密码.
