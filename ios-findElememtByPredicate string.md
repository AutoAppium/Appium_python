# iOS 定位方式 iOSNsPredicateString 详解

## 前言

由于使用id、className、AccessibilityId定位方式较为简单，多数情况下，在同一个页面，都不是唯一存在的，不能识别一个元素。而 xpath定位方式在 xcui 底层原生不支持，由 appium 额外支持的，定位速度很慢，而且有时候定位不到元素的情况存在。综上所述，在 iOS 的 UI 自动化中，使用原生支持的iOSNsPredicateString定位方式是最好，支持也是最好的。
定位方式

仅支持 iOS 10或以上（底层需要使用 XCUITest 框架），可支持元素的单个属性和多个属性定位，推荐使用。一个元素有这些属性：type、value、name、label、enabled、visible，有些元素的属性只有以上的部分属性，如下图所示，可根据这些属性进行元素定位。
inspector

## 元素属性的介绍

type:元素类型，与className作用一致，如：XCUIElementTypeStaticText
value: 一般不用
name:元素的文本内容，可用作 AccessibilityId定位方式，如：测试420班级群
label:绝大多数情况下，与 name 作用一致
enabled:元素是否可点击，一般值为true或者false
visible:元素是够可见，一般值为true或者false

## 定位方式

元素的定位方式都是一个属性+运算符+值形式存在

### 比较运算符：>,<,==,>=,<=,!=
可用于数值和字符串的比较，
如：name>100 或name == '测试'

### 范围运算符：IN,BETWEEN
可用于数值和字符串的范围核对
如：name BETWEEN {3,10}，name IN {'Alan','May'}

### 字符串相关：CONTAINS、BEGINSWITH、ENDSWITH
包含某个字符串，如：label CONTAINS '测试'
以某个字符串开头，如：label BEGINSWITH '420'
以某个字符串结束，如：label ENDSWITH '班级群'
PS：在三个关键字后加上[c]不区分大小写，可用于字母的校验；[d]不区分发音符号，即没有重音符号($、#、%等)；[cd]即不区分大小写，也不区分发音符号，如：name CONTAINS[c] ABcd和name CONTAINS abcd、name CONTAINS ABCD是等同的，注意后面两个没带[c]的不相等

### 通配符：LIKE
通配符也接受[cd]，?代表一个字符，*代表多个字符
如：一个元素的label属性为

label LIKE '420测试班级群'
label LIKE '420测?班级群'
label LIKE '420??班级群'
label LIKE '42？测试班？群'
label LIKE '*试班级群'
label LIKE '420测试班*'
label LIKE '42*级群'
label LIKE '4*试*群'

以上这么多种文本都可以被识别为同一个元素。

### 正则表达式：MATCHES
如：以4开头，以群结束，

label MATCHES '^4.+群$'

PS：具体正则表达式语法，请百度一下，你就知道

## 以一种属性定位元素

可以用元素的属性：type、value、name、label、enabled、visible，进行定位：

type == XCUIElementTypeStaticText,
label CONTAINS '测试'
label LIKE '*试班级群'
enabled == true
visible == false

## 以两种或两种以上属性定位元素

就是以上单个属性定位用符号AND连接起来即可。如：

type == XCUIElementTypeStaticText AND label CONTAINS '测试
type == XCUIElementTypeStaticText AND label CONTAINS '测试' AND enabled == true

