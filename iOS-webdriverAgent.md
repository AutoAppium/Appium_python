# 下载好最新的WebDriverAgent
git clone https://github.com/facebook/WebDriverAgent

1. 进入下载后的WebDriverAgent文件：<br>
cd …/…/WebDriverAgent

2. 创建文件：WebDriverAgent.bundle<br>
mkdir -p Resources/WebDriverAgent.bundle

3. 运行./Scripts/bootstrap.sh(连VPN)<br>
sh ./Scripts/bootstrap.sh -d<br>
在运行sh ./Scripts/bootstrap.sh -d <br>

- 执行一次后‘-d’参数加上后面再用的话可能没反应，需要重新下载WebDriverAgent再来一遍了：再次运行sh ./Scripts/bootstrap.sh -d 不报错就ok

4. 用Xcode打开WebDriverAgent.xcodeproj：<br>
进入WebDriverAgent目录，找到WebDriverAgent.xcodeproj，双击打开，默认就是用Xcode打开的。

5. 编译WebDriverAgentLib<br>
打开Xcode->References输入appleID和密码（公司的开发者帐号，可以找开发要）可以看到team里的人员。进入Xcode，首先要切换到WebdriverAgentLib，General -> Signing:<br>
 钩上自动查找并选择刚才输入的Apple ID的组, 修改bundleID<br>
编辑如下内容，facebook改成(跟证书一致的bundleID)然后点击左上角那个播放按钮进行编译。若果编译的过程中有语法错误，应该是11步没有安装好<br>

6. 配置Build Settings<br>
查找test，并修改bundleID，查找sign确保Any iOS SDK = IOS Developer<br>


7. 编译WebDriverAgentRunner<br>
切换到WebDriverAgentRunner<br>
首先，编辑general，和上面大同小异，也是要勾选自动签名和选择开发者帐号。<br>
接着，Build Settings下编辑Basic和Combined里的内容：bundle ID，signing。<br>

配置好后点击编译按钮，是build succeed的就可继续进行，否则请回去重新配置环境。<br>
备注：如果需要跑测试则将UnitTests，IntegrationTests, IntegrationApp分别修改以上几个位置的bundle ID， signing下的apple id

8. 启动WebDriverAgent服务<br>
连接一个ios模拟器点Product->Test会自动跑里面的测试。测试pass<br>
*****手机和MAC都在同一个网段下，且都能连接外网*******<br>
*****真机要开启开发者模式*******<br>
连接并选择真机的iOS设备，在终端下输入下面的命令就进入开发者模式了。
$ DevToolsSecurity –enable<br>

关闭Xcode，进入WebDriverAgent 文件夹，<br>

cd /usr/local/lib/node_modules/appium/node_modules/appium-xcuitest-driver/WebDriverAgent

*****获取手机的udid*****<br>
 idevice_id -l<br>
然后安装这个webdriverAgent到手机上，记得替换uuid。Build the project:<br>

xcodebuild -project WebDriverAgent.xcodeproj -scheme WebDriverAgentRunner -destination 'id=7xxxxbbbb' test <br>
这时候可以看到手机上多了一个WebdriverAgent的app<br>
运行成功时，在控制台应该可以打印出一个Ip地址和端口号<br>

- 2017-12-21 17:48:28.668160+0800 WebDriverAgentRunner-Runner[1792:946737] Continuing to run tests in the background with task ID 1<br>
Test Suite 'All tests' started at 2017-12-21 17:48:29.366<br>
Test Suite 'WebDriverAgentRunner.xctest' started at 2017-12-21 17:48:29.367<br>
Test Suite 'UITestingUITests' started at 2017-12-21 17:48:29.367<br>
Test Case '-[UITestingUITests testRunner]' started.<br>
    t =     0.00s Start Test at 2017-12-21 17:48:29.369<br>
    t =     0.00s Set Up<br>
2017-12-21 17:48:29.395509+0800 WebDriverAgentRunner-Runner[1792:946737] Built at Dec 21 2017 12:41:55<br>
2017-12-21 17:48:29.442673+0800 WebDriverAgentRunner-Runner[1792:946737] <br>ServerURLHere->http://111.111.1.111:8100<-ServerURLHere

9. 检查是否成功
在网址上输入http://(iP地址):(端口号)/status，如果网页显示了一些json格式的数据，说明运行成功。<br>

10. WebDriverAgent放到Appium目录下
将WebDriverAgent文件夹覆盖到appium的下面WebDriverAgent目录<br>
进入WebDriverAgent文件夹<br>
cd /usr/local/lib/node_modules/appium/node_modules/appium-xcuitest-driver/WebDriverAgent<br>
（如果WebDriverAgent 所在路径和此不同，请自行查找）<br>


参考官网：[Setting up iOS Real Devices Tests with XCUITest](https://github.com/appium/appium-xcuitest-driver/blob/master/docs/real-device-config.md)
