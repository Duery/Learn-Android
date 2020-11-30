# Android软件开发期末复习

“少欲则心静，心静则事简单”

## 1.Android系统的体系结构

##### 1.2.1Android系统简介

Android是一个运行在Linux内核上面的轻量级操作系统。

采用速度更快的Dalvilk虚拟机（支持多进程与内存管理、低功耗支持等）。

集成了基于开源Wdbkit引擎，以及轻量级的数据管理系统。

##### 1.2.3AndroidSDK简介

Android SDK包含了大量的类库和开发工具，程序开发者可以直接调用这些API函数。

Dalvik支持的文件是特殊的，它需要将普通的Java的class文件用AndroidSDK中的dx工具转换为。dex格式的文件。但这些转换是透明的，编程人员无需处理。

## 2.创建第一个Android应用程序

##### 2.3.1java文件夹

一个android应用程序的程序逻辑以及功能代码都是在“java”文件夹下面的。

java文件夹：app/src/main/java(程序启动类主activity）

##### 2.3.2res文件夹

res文件夹是所有应用程序的资源文件夹。

drawtable和minimap存放照片格式的文件夹

layout主要存放界面布局xml文件

**res文件夹：app/src/main/res/layout(xml布局)，**

values文件夹中包含了所有xml格式的参数描述文件。stylesa.xml（样式资源描述文件）,arrays.xml（数组资源描述文件）。

app/src/main/res/values（资源描述文件）

2.3.3应用配置文件AndroidManifest.xml

它是应用程序的重要组成文件，提供了Android系统所需要关于该应用程序的所有必要信息，**即在该应用程序的任何代码运行之前系统所必须拥有的信息**。

|  XML标签  | 说明 |
| ---- | ---- |
| <manifest> | 包含了包名、软件的版本号、版本名称等属性。其中包名是应用程序唯一标识。 |
| <application> | 声明每一个应用程序的组件及其属性 |
| <uses-premisssion> | 声明该应用程序该拥有如何的权限，以便访问API的被保护部分 |
| <activity> | 声明Activity组件 |

## 3.Activity的界面布局

##### 3.1.1.Android应用的基本控件

1、activity

（1）一个Activity通常就是一个单独的屏幕（窗口）。

（2）Activity之间通过Intent进行通信。

（3）**android应用中每一个Activity都必须要在AndroidManifest.xml配置文件中声明，否则系统将不识别也不执行该Activity**。

2、service

（1）service用于在后台完成用户指定的操作。service分为两种：

（a）started（启动）：当应用程序组件（如activity）调用startService()方法启动服务时，服务处于started状态。

（b）bound（绑定）：当应用程序组件调用bindService()方法绑定到服务时，服务处于bound状态。

**音乐播放器就要用到service控件，在后台运行没有界面，但是功能和activity一样。Service组件通常用于为其他组件提供后台服务或监控其他组件的运行状态。**

3、content provider 

（1）android平台提供了Content Provider使一个应用程序的指定数据集提供给其他应用程序。其他应用可以通过ContentResolver类从该内容提供者中获取或存入数据。

（2）只有需要在多个应用程序间共享数据是才需要内容提供者。例如，通讯录数据被多个应用程序使用，且必须存储在一个内容提供者中。它的好处是统一数据访问方式。

（3）ContentProvider实现数据共享。ContentProvider用于保存和获取数据，并使其对所有应用程序可见。这是不同应用程序间共享数据的唯一方式，因为android没有提供所有应用共同访问的公共存储区。

4、broadcast receiver

（1）广播是一种广泛运用在应用程序之间的传输信息机制。而BroadcastReceiver是用来接受并响应广播消息的组件。

**内容提供者的激活：当接收到ContentResolver发出的请求后，内容提供者被激活。而其它三种组件activity、服务和广播接收器被一种叫做intent的异步消息所激活。**

##### 3.1.3Activity的生命周期

![Android开发复习笔记](/Users/ouyanghongjia/Documents/Android开发复习笔记.gif)

Resume：重新开始，继续。

Foreground：前景，这里指前台。

主要步骤有其二：

（1）：当其他activity在当前activity前面的时候，会进入到Onpause，若当前内存不够用的时候改进程会被killed，如果该activity被切换到前台上，会调用resume方法。

（2）：当这个activity长时间不被可见化的时候，就会进入stop方法，如果在stop方法下面，当前内存不够用的时候进程就会直接被杀死，如果该进程被切换到前台上面，就会进入OnRestart方法从而进入OnStart方法。（Resume方法在OnStart方法后面）

**3.1.4 activity的启动模式**

所有的Activity的模式都是由堆栅来进行管理 ”后进先出“

Activity的启动模式有4种：standard，singleTop，singleTask，singleInstance

**3.1.5 context及其在activity中的应用**

context是描述一个应用程序环境的上下文信息，是访问全局信息（如字符串资源，图片资源等等）的接口。

**3.2.1 view类和viewgroup类**

view是Android平台上表示用户界面的基本单元如：TextView，Button，CheckBox等等，VIew是所有可视化控件的基类

viewgroup类是view类的子类，但是与view类不同的是viewgroup可以充当其他控件的容器。

**3.2.2 XML布局及其加载**

xml界面的布局分为两种：

（1）、在XML文件中设置，设置之后在对应的java文件中oncreate（）中声明

`setcontent（R.ID.XX)`

（2）、直接在java中声明，这里不常用我就不写啦。

**3.2.4资源的管理与使用**

1、R.java文件：是由Android studio自动生成的，提供了对Android资源的全局索引，最好不要修改，修改后地址错位导致报错。“R.资源类型.资源名称.

2、图片资源的管理和使用：一般把图片文件放进：mipmap文件夹或者drawable文件夹。一般放入mipmap占用资源小，不同设备上面的自适应比较好。

**3.4.1线性布局LinearLayout**

顾名思义，所有控件排列方式是线性的。

布局方向是由属性Android：orientation的值来决定的

`Android:orientation=vertical` 垂直排列

`Android:orientation=horizontal` 水平排列



