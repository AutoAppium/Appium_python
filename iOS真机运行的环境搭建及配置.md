# iOS真机运行的环境搭建及配置
  
  ## 1. 安装前提
  ### 硬件：
  Mac电脑一台<br>
  IOS手机一部<br>

  ### 软件：
  1. 操作系统： Mac OS 10以上
  2. python3.4及以上 https://www.python.org/downloads/(配置环境变量）
  3. pycharm 2017.1及以上版本（Community版本和Professional版本都可以）
    https://www.jetbrains.com/pycharm/download/previous.html
  4. SDK/jdk已安装并配置好环境变量，参考Andorid安装步骤
  
  上述软件都准备好后，则进入安装appium步骤。
  ## 2. 安装步骤：

### 安装依赖
  1. 安装最新的brew
  - 如果没有安装过Homebrew,先安装homebrew/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"         
  2. 安装最新的nodejs
  - brew install node，由于新版的node已经集成了npm，所以node安装成功时npm也一并安装好了。同样可以通过输入 "npm -v" 来测试是否成功安装.
      
  3. 安装ios相关依赖库：
      - libimobiledevice
$ brew install libimobiledevice –HEAD #和iOS通讯使用，获取重要更新如果没有安装 libimobiledevice，会导致Appium无法连接到iOS的设备Error: No available formula with the name "–head" 用上面的命令遇到error后用下面的命令安装libimobiledevice brew install -s --HEAD libimobiledevice ideviceinstaller
      - carthage
ios10+以上要安装carthage，ios-deploy，真机需要安装xcpretty：$ brew install carthage

      - ideviceinstaller$ brew install ideviceinstaller   #安装app使用，只在ios9可用。      
      - xcpretty
$ gem update –system #最好用最新版本的gem这里请翻墙一下 2.6.3$ sudo gem install xcpretty 安装xcpretty，经常安装失败，没反应，但是大家耐心等待吧，如果时间较长的话，建议大家切换个目录重新安装。# 确保只有 gems.ruby-china.org$ gem sources --add https://gems.ruby-china.org/ --remove https://rubygems.org/$ gem sources -lhttps://gems.ruby-china.org
      - ios-deploy
$ npm install -g ios-deploy如果要在iOS10+的系统上使用appium，则需要安装ios-deploy安装iOS-deploy若遇到以下错误: tool 'xcodebuild' requires Xcode, but active developer directory '/Library/Developer/CommandLineTools' is a command line tools instance重置Xcode路径，再执行打包命令.（找到Xcode的路径）：$ sudo xcode-select -switch /Applications/Xcode.app/Contents/Developer(你的xcode路径)ios-deploy可以用来安装卸载ios应用cnpm有个问题，就是安装的node_module会全部放在当前路径下。cnpm这工具是马云为了国内局域网用户做的一款替代npm的工具(关键字：墙)，安装好了以后可以用cnpm代替npm 所以我们使用cnpm的时候，需要切换到/usr/local/lib(node模块默认安装路径)$ cd /usr/local/lib$ cnpm install -g ios-deploy
      
### 安装Appium
      
  4. 安装Appium
      - -> 直接下载dmg文件安装Appium Desktophttps://github.com/appium/appium-desktop/releases/tag/v1.6.x      - -> 命令行安装appiumGit的方式安装需要先装git：$ brew install git安装前把历史版本卸载掉：$ npm uninstall -g appium（不卸载安装的话可能会出现错误）新建一个文件夹：cd Appium, 下载最新appium，输入以下命令：$ git clone https://github.com/appium/appium.git进入子目录cd appium，安装appium(为了避免权限问题报错用以下命令）：$ sudo npm install —unsafe-perm=true安装之后要与系统相关联： $ sudo npm linkNotes: desktop的版本，会有一些问题。个人建议使用命令行操作appium。==注意==：下载途中很有可能遇到卡住的情况，是因为墙的缘故，所以我们可以连上vpn进行安装。所以大家一定要耐心安装，记得随时切换vpn。2个关键点： 一个是安装appium-automator2相关的apk，一个是selendorid相关jar的时候会比较卡，这时候可以疯狂切换vpn注意事项： 以上内容都不要在root用户下安装，默认不是root用户。终端命令的每一行的最左侧会显示用户，不是root就行。若出现权限问题，进入root用户将文件权限更改下。然后退出root用户继续安装即可chmod -R 777 pathForFile 使用此命令修改文件夹的权限。- 若遇到问题：cwd错误执行以下命令：$ sudo npm cache clean -f$ sudo npm install -g n（note： n 是node的版本管理工具。）
      
  5. 检查是否安装成功需要用appium-doctor
      先后用以下命令检查是否安装完成$ npm install -g appium-doctor$ appium-doctor      


### 安装WDA
  6. Xcode最新版本下载安装在最新的Mac系统下
Xcode等应用的旧版本的下载地址：下载完之后手动解压，安装。https://developer.apple.com/download/more/ 

  7. 安装appium-xcuitest-driver依赖
 参考：
 

### 安装python-Appium核心库
  8. Appium Python client安装
$ pip install Appium-Python-Client
也可直接使用pycharm安装Appium-Python-Client和selenium。完成后可以看到对应的版本号<br>
  
  9. 生成在真机上运行的包：
如果需要使用打包好的ipa包或者app包来进行安装，则需要用源码来打包成ipa进行安装。
如果知道bundle ID，可以直接下载安装好对应bundle ID的包, 直接进行启动app。


### 启动Appium，真机运行
  10. AppiumDesktop运行程序1）运行Appium-Desktop，开启start server2）连接IOS手机<br>3）点击start new session4）在 Desired Capabilities 中输入相关的参数后点击Start Session5）运行成功后，会弹出一个控制界面，在该界面中可以控制手机上正在运行的程序6）点击界面上方中心的录制按钮，可以将你对手机端的操作代码化

### 脚本运行
 1）启动Appium Desktop，开启start server<br>
 2）连接IOS手机<br>
 3）编写客户端代码<br>
  - 假设我们的代码放在目录/Desktop/AppiumDemo 中。<br>
 4）创建文件demo_appium.py , 编辑内容：<br>
```python
  #coding=utf-8
  from appium import webdriver
  desired_caps = {}
  desired_caps['platformName'] = ‘IOS’
  desired_caps['platformVersion'] = ’10.2.6’
  desired_caps['deviceName'] = ‘iphone6S’
  desired_caps[‘udid’] = ‘yourphonesudid’
  desired_caps[‘bundleID’] = ‘com.app.bundleid’
  desired_caps['automationName'] = ‘XCUITest’
  desired_caps[‘app’] = ‘path/to/your/app’
  driver = webdriver.Remote('http://localhost:4723/wd/hub', desired_caps)
  driver.find_element_by_xpath(‘//XCUIElementTypeStaticText[@name=“test”]’).click()
  driver.quit()
```
5）运行<br>
打开命令行，cd到/Desktop/AppiumDemo中，运行 python demo_appium.py, 正常情况可以看到手机按照代码控制。<br>
