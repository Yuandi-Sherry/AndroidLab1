# AndroidLab1
# Lab1 - 基本UI界面设计  实验报告

## 实验目的

1.熟悉 Android Studio 开发工具操作
2.熟悉 Android 基本 UI 开发，并进行 UI 基本设计

## 实验内容

实现一个Android应用，界面如下：

（假装有图）

##### 具体说明

1. 该界面为应用启动后看到的第一个界面
2. 只用一个ConstraintLayout 实现整个布局

##### 标题和图片

1. 标题字体大小20sp，与顶部距离20dp，居中
2. 图片与标题的间距为20dp，居中

##### 输入框

1. 整体距屏幕右边间距20dp，上下两栏间距20dp，内容（包括提示内容）如图所示，内容字体大小18sp
2. 学号对应的EditText 只能输入数字
3. 密码对应的EditText 输入方式为密码

##### 按钮

1. 两个单选按钮整体居中，字体大小18sp，间距10dp，默认选中的按钮为第一个
2. 两个按钮整体居中，与上方控件间距20dp，按钮间的间距10dp，文字大小18sp
3. 按钮背景框左右边框与文字间距10dp，上下边框与文字间距5dp，圆角半径10dp，背景色为#3F51B5

## 实验过程

首先在strings.xml文件中定义UI界面中所有可能出现的字符串，sysu.jpg拖入mipmap文件夹中。

### 标题和图片的实现

标题为<TextView>标签类型

字体大小采用textSize属性设置，与顶部距离采用layout_marginTop属性。

> 注意：为适应不同的分辨率，字体的单位为sp，其他单位为dp

借鉴`Hello World`的与左右边框对齐的居中方法使得标题和图片居中

```xml
    app:layout_constraintLeft_toLeftOf="parent"
    app:layout_constraintRight_toRightOf="parent"
```

图片为<ImageView>标签类型

用src属性对文件夹中的图片进行引用，与标题的距离和剧中方法与标题中一致。

### 输入框的实现

其中“学号：”，“密码：”使用了<TextView>类型，其居中、对齐、间距、字体大小等的设置方法和标题类似。

这一部分的重点在于EditText的实现。

#### 宽度自动填充

观察样例会发现两个输入栏的宽度都是从'：'开始到屏幕右边缘结束的，课上04的PPT中讲过使用`android:layout_width="0px"`属性进行设置。

#### 提示文字

类似于html中的placeholder属性，当输入为空的时候显示，有输入时消失，PPT某一页的演示中出现了hint这一属性，因而使用`android:hint="@string/inputId"`即可实现。

#### 输入字符类型限制

由于要求2中提出学号只能接收数字的输入，[这篇博客](https://blog.csdn.net/brycegao321/article/details/52277255)中介绍了五种限制输入的方法，目前使用了第二种能够在xml中不需要java定义的方法。即在<EditText>中加入，其中引号中是可以接收的字符。

```
android:digits="0123456789"
```

#### 密码隐藏

要求3中要求输入方式为密码，设置`android:inputType="textPassword"`就可以将密码隐藏了。

### 按钮实现

这里的实现主要由三部分组成：RadioGroup（包含两个单选RadioButton），登录Button和注册Button. 目前还没找到类似html中div的组织方式，所以下面的按钮在没有Group包裹的情况下当作两个单独部分实现。

#### Radio Group中Button的横向排列

在<RadioGroup>标签中添加`android:orientation="horizontal"`属性。

#### 默认选择第一个

要求1中默认选择第一个Radio，在实验过程中找到了checked属性，但是设置`android:checked="true"`的时候发现了如果选择下一个，却无法将默认取消的情况。解决方法比较奇特，需要将默认选中的按钮加上一个id标志其唯一性就好了。

#### 两个按钮整体居中

由于两个Button并没有形成一个Button Group，所以无法实现二者相对于屏幕居中。因此我选择了Guideline的方式，将Guideline设置在正中间，两个按钮以`5dp`向它左右看齐。

##### Guideline居中的设置方法

在Guideline的标签中加入`app:layout_constraintGuide_percent="0.5"`，注意这里引号内数字的范围是[0.0, 1.0]，我之前设置50%是失败了的。

#### 设置Button样式

要求3中要求了Button的样式，这里需要在res/drawable中添加一个xml文件，并且以<shape>标签为基础添加标签进行设置。具体代码如下：

```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <solid android:color="@color/buttonColor"/>
    <corners android:radius="10dp"/>
    <padding android:left="10dp"
        android:right="10dp"
        android:top="5dp"
        android:bottom="5dp"/>
</shape>
```

如果需要更多的Button样式可以参考[这篇博客](https://www.jianshu.com/p/e5e8a98fc5d9)，里面有详细的介绍。

## 实验结果

经过上述过程，这个实验就完成了，效果如下：

（假装有图）
