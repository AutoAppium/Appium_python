# 一、windows下Python+Appium自动化环境安装步骤
  windows下只能做android的手机自动化，ios手机的自动化需要用到xcode等依赖ios系统的工具，如果实在想用windows做自动化可以搭建虚拟机来做，不过虚拟机对windows电脑的性能要求较高，否则会很卡。
  ## 1. 安装前提
  ### 硬件：
  windows电脑一台<br>
  Android手机一部<br>
  ### 软件：
  1. 操作系统： win7，win10等
  2. python3.4及以上 https://www.python.org/downloads/(配置环境变量）
  3. pycharm 2017.1及以上版本（Community版本和Professional版本都可以）
    https://www.jetbrains.com/pycharm/download/previous.html
  4. 安装JDK，配置环境变量：JAVA_HOME - D:\Program Files\Java\jdk1.8.0_121
    CLASSPATH - %JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
    PATH - %JAVA_HOME%\jre\bin;%JAVA_HOME%\bin
  
  上述软件都准备好后，则进入搭建步骤。
  ## 2. 安装步骤：
  1. 下载安装Android SDK
      - 下载地址：http://developer.android.com/sdk/index.html
      
  2. 配置SDK：
      - 新建ANDROID_HOME  D:\ProgramFiles (x86)\Android\android-sdk，
      - 在PATH中添加：%ANDROID_HOME%\platform-tools;%ANDROID_HOME%\tools;
      
  3. Install Android SDK Packages
      - 进去 android-sdk 文件夹下，打开 SDK Manager. D:\Program Files (x86)\Android\android-sdk\SDK Manager.exe
      - 建议勾上所有最近版本的SDK Tools, Platform Tools以及几个之前版本的Build Tools. 最新的5个APIs. 如果你的安卓设备是个更老版本的，或者要测得app只支持某一个更老版本的Android，还要下载更老的Android版本。如果硬盘不是问题的话，安装越多的package/versions会比较好。
      - 选择每一个分支并点击Accept License，所有的package都是勾上的状态，然后点击Install
      - 等待所有的package下载安装完成。
      - 安装Intel Hardware Accelerated Execution Manager为了避免Android虚拟设备创建过程中发生错误。
      下载地址：https://software.intel.com/en-us/android/articles/intel-hardware-accelerated-execution-manager-end-user-license-agreement 
      下载后解压并执行intelhaxm-android.exe文件 
      
  4. 下载安装Nodejs
      - 下载地址：https://nodejs.org/en/
      - 需要配置环境变量，在PATH中添加：D:\Program Files\nodejs;
      - 输入node -v，查看node安装版本
      
  5. 下载安装Appium
      下载地址：http://appium.io/downloads.html
      安装appium的2种方法：
      1. Appium Desktop:
      - 下载安装好后，配置环境变量
      - 配置好后，启动cmd
      - 安装appium-doctor: npm install -g appium-doctor
      - 输入appium-doctor检查appium的安装环境是否成功,出现'All checks were successfully.' 就安装成功了。
      - 如果安装的是desktop版本的appium，用命令行也可以启动appium，即允许以下js文件：
        C:\Program Files (x86)\Appium\resources\app\node_modules\appium\build\lib\main.js
      - cmd 命令：
        cd C:\Program Files (x86)\Appium\resources\app\node_modules\appium\build\lib
        node main.js
      
      2. Appium Server： 
      - 安装appium server命令行：
      npm install -g appium@1.8.1 （此方法需要翻墙，安装appium-chromedriver时）
      - 更新命令：npm install appium -g --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
      - 直接在cmd终端输入appium即可启动appium server
      
  6. 选择Python版本的Lib: Appium-Python-Client-0.22.tar.gz
  7. 由于Appium依赖于Selemium,所以还要下载 Selemium Lib: selenium-2.53.2.tar.gz   https://pypi.python.org/pypi/selenium
 
 ## 3. 启动Appium，真机运行
 1）启动Appium<br>
  打开命令行，输入appium， 显示成功启动。<br>
 2）连接Android手机<br>
 3）编写客户端代码<br>
  - 假设我们的代码放在目录E:\Test\AppiumDemo 中。首先把 Appium-Python-Client-0.22.tar.gz 里面的appium目录解压到AppiumDemo中， 把 selenium-2.53.2.tar.gz里面的selenium目录解压到AppiumDemo中。<br>
  - 也可直接使用pycharm安装Appium-Python-Client和selenium。完成后可以看到对应的版本号<br>
 4）创建文件demo_appium.py , 编辑内容：<br>
```python
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
```
5）运行<br>
打开命令行，cd到E:\Test\AppiumDemo中，运行 python demo_appium.py, 正常情况可以看到手机按照代码控制，打开计算器，逐个点击按钮完成计算。<br>


# 二、IOS下Appium自动化环境安装步骤
  ## 1. 安装前提

  ### 硬件：
  IOS手机一部<br>
  Macbook笔记本一台<br>

  ### 软件：
  1. OS：MacOS Sierra10以上<br>
  2. Python3以上

  ## 2. Android测试安装步骤
1.安装brew
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"<br>
mac自带了Ruby，网上很多给的安装命令下载的版本较低，使用上面的命令，可以安装最新的brew。<br>
安装成功后，$ brew -v 会显示相应的Homebrew的版本号。<br>
（官方地址：http://brew.sh/index_zh-cn.html）；<br>

2.安装node，appium的解释器
$ brew install node

3.安装appium
  - 通过命令可以下载到最新的appium server版本，命令如下：
$ npm install -g appium
如果遇到权限问题，用以下命令：$ sudo npm install -g appium --unsafe-perm=true --allow-root
  - 可以直接在官网下载appium.dmg安装，http://appium.io/downloads.html
  
4.安装sdk
- 下载sdk安装包解压后找到解压后的路径（配环境变量会用到）：
https://dl.google.com/android/adt/adt-bundle-mac-x86_64-20140702.zip
- 启动SDK Manager（若需要使用android模拟器需要下载android sdk下的一些工具）：
cd /Users/xx/Desktop/autotest/adt-bundle-mac/sdk/
./android sdk

5.安装jdk，记住路径

- jdk下载dmg安装包进行安装：http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html
点击Accept License Agreement按钮，选择Mac版本的jdk进行下载dmg
- 当在Mac下安装完Java运行环境，而又没有添加JAVA_HOME变量的时候，我们如何得到JAVA_HOME变量的路径呢？
直接在home目录下执行命令：$ /usr/libexec/java_home [-V]
即可获得输出：/Library/Java/JavaVirtualMachines/jdk1.8.0_25.jdk/Contents/Home

6. 配置jdk和sdk环境变量(Android)：
MACbook中打开.bash_profile步骤：<br>
1）. 启动终端Terminal<br>
2）. 进入当前用户的home目录, 输入cd ~<br>
3）. 创建.bash_profile,输入touch .bash_profile<br>
4）. 编辑.bash_profile文件,输入open -e .bash_profile<br>
在打开的.bash_profile文件里面输入以下内容，JAVA_HOME，PYTHON，ANDROID_HOME路径需要自己去找。<br>
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home<br>
export PATH=$JAVA_HOME/bin:$PATH<br>
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar<br>
export PATH=/usr/local/Cellar/python3/3.6.1/Frameworks/Python.framework/Versions/3.6/bin:${PATH}<br>
export ANDROID_HOME=/Users/xx/Desktop/autotest/adt-bundle-mac/sdk<br>
export PATH=${PATH}:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools:$ANDROID_HOME/build-tools/23.0.1<br>
5）. 保存文件，关闭.bash_profile<br>
6）. 更新刚配置的环境变量, 输入source .bash_profile<br>

7. appium_doctor检测APPium是否安装成功
未配置appium环境变量，需要进入到对应路径下. <br>
Desktop安装的路径是：/Applications/Appium.app/Contents/Resources/node_modules/appium-doctor<br>
执行命令：node appium-doctor.js,可以看到安装成功<br>

8. Appium Python client及驱动的安装
- 从pip安装：'Appium-Python-Client'.
$ pip install Appium-Python-Client
- 从官网下载源码解压后直接安装：Appium-Python-Client-X.X.tar.gz.
$ tar -xvf Appium-Python-Client-X.X.tar.gz
$ cd Appium-Python-Client-X.X
$ python setup.py install
- 从GitHub上直接安装.
$ git clone git@github.com:appium/python-client.git
$ cd python-client
$ python setup.py install

9. Android真机运行需要driver
$ npm install appium-android-driver<br>

10. 如果安装的dmg Desktop版appum可以直接连接android设备
配置如下：<br>
JSON Representation<br>
{<br>
  "platformName": "ANDROID",<br>
  "platformVersion": “5.1.1”,<br>
  "deviceName": "OPPO A33",<br>
  "app": “/path/for.apk",<br>
  "noReset": true,<br>
  "appPackage": "your.app.package",<br>
  "appActivity": "you.app.package.MainActivity",<br>
  "webdriver": "http://0.0.0.0:4723/wd/hub"<br>
} <br>
点击start session，可以看到手机会启动app<br>

注：检查手机是否连接成功：输入命令$ adb devices<br>
list of devices 不为空，则连接成功。<br>


  ## 3. IOS真机测试安装步骤 
参考：[iOS真机运行的环境搭建及配置.md](https://github.com/AutoAppium/appium_frame/blob/master/iOS%E7%9C%9F%E6%9C%BA%E8%BF%90%E8%A1%8C%E7%9A%84%E7%8E%AF%E5%A2%83%E6%90%AD%E5%BB%BA%E5%8F%8A%E9%85%8D%E7%BD%AE.md)
