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
      
    5. 下载安装Appium
      下载地址：http://appium.io/downloads.htmlom
      - 需要配置环境变量 D:\Program Files (x86)\Appium\node_modules\.bin;
      - 配置好后，启动cmd，
      - 输入node -v，查看node安装版本
      - 输入appium-doctor检查appium的安装环境是否成功,出现'All checks were successfully.' 就安装成功了。
  
    6. 选择Python版本的Lib: Appium-Python-Client-0.22.tar.gz
    7. 由于Appium依赖于Selemium,所以还要下载 Selemium Lib: selenium-2.53.2.tar.gz   https://pypi.python.org/pypi/selenium
 
 ### 启动Appium，真机运行
    1) 启动Appium
    打开命令行，输入appium， 显示成功启动：
    2）连接Android手机
    3）编写客户端代码
    假设我们的代码放在目录E:\Test\AppiumDemo 中。首先把 Appium-Python-Client-0.22.tar.gz 里面的 appium 目录解压到AppiumClientPython 中， 把 selenium-2.53.2.tar.gz里面的 selenium 目录解压到AppiumClientPython中。
    4）创建文件demo_appium.py , 编辑内容：
      ```
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
