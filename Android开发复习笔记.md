# Android软件开发期末复习

“少欲则心静，心静则事简单”

## 1.Android系统的体系结构

##### 1.2.1Android系统简介

Android是一个运行在Linux内核上面的轻量级操作系统。

采用速度更快的Dalvilk虚拟机（支持多进程与内存管理、低功耗支持等）。

集成了基于开源Wdbkit引擎，以及轻量级的数据管理系统。

##### 1.2.3AndroidSDK简介

Android SDK包含了大量的类库和开发工具，程序开发者可以直接调用这些API函数。

Dalvik它需要将普通的Java的class文件用AndroidSDK中的dx工具转换为。dex格式的文件。但这些转换是透明的，编程人员无需处理。

## 2.创建第一个Android应用程序

##### 2.3.1java文件夹

一个android应用程序的程序逻辑以及功能代码都是在“java”文件夹下面的。

java文件夹：app/src/main/java(程序启动类主activity）app/src/main/java/res/layout minimal,drawtable

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

![Android开发复习笔记](/Users/ouyanghongjia/Documents/Android应用开发/Android开发复习笔记.gif)

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

**3.4.4表格布局TableLayout**

一般在<TableLayout></TableLaout>标签中去定义TableRow元素，每个TableRaw代表一个行，在TableRow中可以添加子元素，子元素为一列。并且TableRow中可以有空的单元格，**行号和列号是从零开始的。**

##### 3.4.5 帧布局 FrameLayout

采用帧布局的时候，子元素只能放置在父容器的左上角。后放置的元素遮挡之前放置的元素。该布局在运行时所有的元素都自动地对其到父容器的左上角。

## 4、常用界面控件及其应用

##### 4.2.1基于监听接口的时间处理方式

| 监听器                     | 说明                             |
| -------------------------- | -------------------------------- |
| View.OnclickListener       | 被点击的时候调用                 |
| View.onLongClickListener   | 当前view被长按的时候             |
| View.onFocusChangeListener | 当焦点变化                       |
| View.OnkeyListener         | 当前组件获得焦点，或者被用户按下 |
| Vew.onTouchListener        | 比较繁琐！！！                   |

实现方法

**1、定义Activity时实现接口**

**2、定义内部类实现接口**

**3、通过匿名内部类实现接口**(有误)

##### 4.3.1 TextView

这个感觉不用多说，用来显示文字，常用与EditText前面。作为文本输入的一个提示。

##### 4.3.2 EditText

Edit Text是TextView的子类，所以TextView的方法同样适用于EditText，获取输入内容用`getText（）`来实现

##### 4.3.4 Toast

一个用来提示信息的机制

调用Toast静态方法来makeText或make（）

`Toast.makeText(getApplicationContext(),"Your Texts",显示时长);`

然后再调用show（）方法。

还有一种最常用的直接是

`Toast.makeText(getApplicationContext(),"Your Texts",显示时长).show();`

##### 4.4.1RadioButton 和RadioGroup

一般来说RadioGroup和RadioButton都是组合在一起用的，当我们设置完xml文件后如何去调用内

可以在activity中获取组件后然后使用setOncheckedchangeListener来对整个RadioGrop来进行监听，最后只需要当前的checkedid和RadioButton按钮对上我们就可以选中RadioButton了。

##### 4.4.2 CheckBox(复选框)

与单选按钮类似，通常需要监听处理CheckBox对象的CheckedChange事件。也是调用CheckBox的`setOncheckedchangeListener()`方法。

#### 4.5ListView

listview是一个比较常用的功能，可以按照设定的规则自动的填充并展示一组列表的信息，并且能够根据数据的长度来自动适应并展示，如果能容过多，会自己出现滚动条。

那如何设置ListView呢，一般要三要素：

1⃣️ListView的一个控件实例化对象

2⃣️一个Adapter（适配器）一般有三种：ArrayAdapter、SimpleAdapter、SimpleCursorAdapter这三种，ArrayAdapter最简单，但是一般通常用SimpleAdapter可自定义程度高

3⃣️数据可以进行映射的数据

Listview基本的使用步骤：

定义列表项布局文件或者使用自定义布局
构建Adapter对象
ListView调用setAdapter方法绑定Adapter
事件监听

**最简单的例子**

```java
protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_list);
        ListView listView = findViewById(R.id.simpleListView);
        // 代码中使用Adapter
        ArrayAdapter<String> arrayAdapter = new ArrayAdapter<>(
                this,
                R.layout.support_simple_spinner_dropdown_item,
                getResources().getStringArray(R.array.auto));
        listView.setAdapter(arrayAdapter);
}
```

注意：如果使用SimpleAdapter的时候需要自定义一个布局文件用来指示我们应该怎么样的显示listview名为：list_item.xml

#### 4.6 下拉列表选择框Spinner

Spinner的实现分为两种一种是静态一种是动态的

**静态实现**
arrays.xml：增加选项列表数组
XML布局：设置Spinner控件的**android:entries**属性引用数组
代码：获取Spinner控件，并绑定OnItemSelectedListener事件

**动态实现**

定义列表项布局文件或者使用自定义布局
构建Adapter对象
ListView调用setAdapter方法绑定Adapter
事件监听

## 5、对话框、菜单和状态消息栏消息

##### 5.1.1提示对话框AlterDialog

简单定义：

对话框是一种显示于Activity之上的界面元素，是作为Activity的一部分被创建和显示的。
当显示对话框时，当前Activity失去焦点而由对话框负责所有的交互。

| **方法名称**             | **描述**                         |
| ------------------------ | -------------------------------- |
| **setTitle**             | **设置警告窗体标题**             |
| **setIcon**              | **设置图标**                     |
| **setMessage**           | **设置警告内容正文**             |
| **setItems**             | **设置对话框显示一个列表**       |
| **setSingleChoiceItems** | **设置对话框显示一个单选列表**   |
| **setMultiChoiceItems**  | **设置对话框显示一个复选框列表** |
| **setView**              | **给对话框设置自定义样式**       |
| **setNegativeButton()** | **添加Negative按钮** |
| **setNeutralButton()** | **添加Neutral按钮** |
| **create()**        | **创建对话框**   |
| **show()**          | **显示对话框**   |

一般是在一个点击事件时候去创建AlterDialog

创建方法：`AlerDialog.Builder myDialog = new AlertDialog .Builder(MainActivity.this);`

创建AlerDialog.bullder对象

##### 5.1.2 DatePickerDialog和TimePickerDialog

```java
protected void showDatePickDlg() {
    Calendar calendar = Calendar.getInstance();//设置系统时间
    DatePickerDialog datePickerDialog = new DatePickerDialog(MainActivity.this, new DatePickerDialog.OnDateSetListener() {
        public void onDateSet(DatePicker view, int year, int monthOfYear, int dayOfMonth) {
            birthEditText.setText(year+"-"+monthOfYear+"-"+dayOfMonth);
        }
    }, calendar.get(Calendar.YEAR), calendar.get(Calendar.MONTH), calendar.get(Calendar.DAY_OF_MONTH));
    datePickerDialog.show();
}
```

之后在activity中添加

```java
birthEditText.setOnFocusChangeListener(new View.OnFocusChangeListener() {
    @Override
    public void onFocusChange(View v, boolean hasFocus) {
        if (hasFocus) {
            showDatePickDlg();
        }
    }
```

就可以实现简单的一个生日选择啦

##### 5.2菜单

“两个菜单的区别，选项和上下文”

选项菜单：在Android3.0之前的设备上，这是常规的菜单，在3.0及其以上版本的设备上，选项被转移到溢出菜单中

选项菜单：

![image-20201202193525452](/Users/ouyanghongjia/Library/Application Support/typora-user-images/image-20201202193525452.png)

选项菜单就是在屏幕的右上角溢出菜单中。

上下文菜单（Context Menu）

上下文菜单是长按界面中的视图控件出现的菜单，类似于右键

##### 5.3状态消息 Notification

状态栏通知主要涉及两个类：Notification和NotificationManager类别。

`NotificationManager是一个系统Service，必须通过getSystemService()方法来获取。`
`NotificationManagernm=(NotificationManager)getSystemService(NOTIFICATION_SERVICE);`
`Notification：是具体的状态栏通知对象，可以设置icon、文字、提示声音、振动等等参数。`

## 6.Fragment及其应用

##### 6.1.1Fragment的基本概念

Fragment非常类似于Activity，可以包含布局，但通常是嵌套在Activity中使用的。

Fragment是Activity界面中的一部分或者是一种行为，可以把多个Fragment组合到一个Activity中来，也可以在多个Activity中重用一个Fragment。

Fragment的生命周期和Activity的生命周期息息相关。

这是官方文档给出的生命周期：

![fragment_lifecycle](/Users/ouyanghongjia/Documents/Android应用开发/fragment_lifecycle.png)

在Activity执行了OnCreate（）方法后，系统才会创建与之相关并加载的Fragment。然后Fragment会调用onAttach（）方法去与Activity与Fragment的关联，这时候Fragment才会加载OnCreate方法然后去创建UI也就是createview（）方法之后在ActivityCreate（）调用然后就和之前的Activity的生命周期大致相同，

![activity_fragment_lifecycle](/Users/ouyanghongjia/Documents/Android应用开发/activity_fragment_lifecycle.png)

## 8.Service与BroadcastReceiver

##### 8.1.1 Intent（字面意思“想要”“意图”之意）

```java
intent = new Intent(MainActivity.this,  MainMenu.class);
startActivity(intent);
```

这个就是一个很经典的转换activity的指令用于Mainactivity和MainMenu两个activity之间的切换

在Android系统中，Intent提供了一种通用的消息机制，它让在用户的应用程序之间来传递Intent来执行动作和产生事件。

一般的Intent的主要用途如下：

（1）启动其他activity就如同我们之前举例子那样。

（2）启动Service

（3）发送广播消息，应用程序和Android系统都可以使用Intent来发送广播消息，如网络连接的变化、电池电量的变化等等之类的。

##### 8.1.3 Intent的解析

Intent主要分为两大类：显式、隐式，接下来让我来简单的来说一说这两个类别结合老师的PPT

**首先是显式** ：显式Intent在构建的时候需要对对象有一个制定的对象，一开始构建的时候就需要去指定该对象是谁，所以一般用于**应用程序内部**来传递消息

**其次是隐式**：隐式在构建的时候不会去关心是谁去收到消息，不会希望谁来得到这个消息

隐式Intent不使用组件名称定义需要激活的目标组件，它更广泛地用于在**不同应用程序之间传递消息**

##### 8.3 利用隐式Intent来启动另外一个组件

有时需要将想启动的组件描述信息放置到Intent里面，而不明确指定需要打开那个组件的时候。例如一个第三方的组件，它只需要去描述自己在什么情况下面被执行了，如果用户组件描述的消息与第三方描述的消息相互匹配，那么这个组件就被启动了。

```java
Uri myuri =Uri.parse("http//www.baidu.com");

Intent myintent =new Intent(Intent.ACTION_VIEW,myuri);

startActivity(myintent)
```

这是点击按钮时候出现百度网页的一个小代码

**但是需要在AndroidManifest.xml文件中去访问Internet权限**

##### 8.4 利用Intent在组件之间来传递消息（重要）

 用Intent来传递消息一般用两种分别是：putExtra（）和putExtras（） //Extra：额外的事物

**这是用PutExtra（）的方法来传递数据**

```java
String data="Hi, OtherActivity";
Intent intent=new Intent(MainActivity.this,OtherActivity.class);
intent.putExtra("extra_data ", data );
startActivity(intent);
```

```java
//获取Intent对象
Intent intent=getIntent();
//获取传递过来的String类型的数据
String data=intent.getStringExtra("extra_data ");
Toast.makeText(OtherActivity.this,"传递的内容：" + data, Toast.LENGTH_LONG).show();
```

首先我们要创建完intent过后，需要向intent里面putExtra，以**键-值**的方式来放，之后我们在下一个activity来接受的时候用getStringExtra来接受只需要加**键名**就可以比如这的`intent.getStringExtra("extra_data ")`

**用PutExtras（）的方法来传递数据**
**Bundle(一捆)主要用于传递数据**；
保存的数据是以`key-value(键值对)`的形式存在的
Bundle经常使用在Activity之间或者线程间传递数据，传递的数据可以是基本数据类型和类
Bundle提供了各种常用类型的`putXxx()/getXxx()方法`，用于读写基本类型的数据，比如`putString()、putInt()、getString()、getInt()`等方法

```java
//实例化bundle对象
Bundle bundle = new Bundle();
//向bundle对象添加数据
bundle.putString("name", "张三" );
bundle.putInt("age", 20);
Intent intent = new Intent(MainActivity.this,OtherActivity.class);
//向intent对象bundle
intent.putExtras(bundle);
startActivity(intent);
```

这是第二个页面

```java
//获取bundle对象
Bundle bundle = getIntent().getExtras();
//通过key为获取value·
String name=bundle.getString("name");
int age=bundle.getInt("age");
Toast.makeText(OtherActivity.this,"传递的内容：name=" + data
+ ",age=" + age, Toast.LENGTH_LONG).show();
```

两个activity之间呢我们都需要去实体化这个bundle，之前我们通过intent.putExtras(bundle)来添加，我们的字符是添加在bundle里面的，之后呢我们直接用bundle来get我们的东西。

##### 8.5 Service

**如何启动Service？**

![image-20201204144859573](/Users/ouyanghongjia/Library/Application Support/typora-user-images/image-20201204144859573.png)

两种方法：一种starservice（），和bindservice（）去启动我们的Server。默认情况下面，service是在应用程序的主线程中启动的。

如果用stearservice来启动服务的时候，启动之后如果再次调用，就不需要onCreate方法了只需要调用onStartCommand（）方法。

两种方法停止service   stopservice（）和onUnbindService（）

##### 8.3.4 将Service绑定到Activity

启动Service 

```java
Intent intent = new Intent(MyServiceActivity.this, MyService.class);
 startService(intent);
```

关闭Service

```java
Intent intent = new Intent(MyServiceActivity.this, MyService.class);
stopService(intent);
```

SQLliteOpenhple（构造方法、OnCreate、OnUpgrade）通过（getReadableDatabase、getWritableDatabase）来实例化 SQLiteDatabase、Cursor（访问数据）

