---
layout: post
title: SuperFamily使用说明
categories: Android
description: 主要说明superfamily组件的使用
keywords: SuperButton ,SuperConstraintLayout ,SuperFrameLayout ,SuperLinearLayout ,SuperRelativeLayout
---
# 有重大更新啦！！！

### 引入

[ ![Download](https://api.bintray.com/packages/androidman/maven/superfamily/images/download.svg?version=2.1.0) ](https://bintray.com/androidman/maven/superfamily/1.2.0/link)

```
implementation 'top.androidman:superfamily:2.1.0'
```
[Github传送门](https://github.com/ansnail/superfamily)

### 写在前面

在版本1.0发布后，superbutton受到了大家的喜爱，作者在项目开发中，写按钮也越来越自如。不过在使用过程中也发现了一些问题总结如下：
1. 需要在比较复杂的布局中使用渐变背景
2. 需要在比较复杂的布局中使用圆角
3. 按钮需要支持边框虚线
4. 需要在比较复杂的布局中使用阴影
5. 按钮没有默认点击效果
6. 没有动态设置方法

等等需求

### 解决办法一

由于存在以上问题，所以在使用过程中作者采取了一些折中的手段：
1. 比如把superbutton放在布局的最下面，这样看上去就能解决背景是渐变背景的问题
2. 自己给superbutton设置pressed_color，让按钮具有点击效果
3. 自己写shape给按钮设置虚线边框

但是这个不能从根本上解决问题，所以作者决心从根本上解决这些问题

### 新的思考

一个复杂的布局根布局一般是ConstraintLayout、 FrameLayout、LinearLayout或者RelativeLayout，如果把superbutton的能力如果能赋给这些布局，那么我们在写一个复杂的布局时就能轻而易举的实现所有superbutton的背景效果。所以作者对superbutton的能力进行了抽取，让ConstraintLayout、 FrameLayout、LinearLayout和RelativeLayout都具备了superbutton除了文字和图标设置以外的所有能力。这也是作者把项目名修改为superfamily的原因，作者的愿景是希望做一个易用的库，让写布局变得更简单。

### 阴影具体的实现

在实现阴影的过程中，作者参考了cardview阴影的具体实现，在5.0以后由于Android原生支持了elevation,但是设置阴影的具体实现在native代码里面，所以暂时没有找到比较好的设置方法。所以作者换了个思路，暂时阴影实现都使用5.0以下的实现方式，但是5.0以下版本阴影会占用view自身的空间，所以使用时需要注意使用padding，让布局显示正常。

### SuperFamily成员
- SuperButton 
- SuperConstraintLayout
- SuperFrameLayout
- SuperLinearLayout
- SuperRelativeLayout


#### <font color="red">SuperFamily成员拥有一些公共属性，即都具有的属性，效果展示如下</font>

#### 效果演示

圆角|颜色渐变|默认点击效果|圆形
:---:|:---:|:---:|:---:
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200110235232.png" width="200" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200111001246.png" width="200"/>|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113231146.gif" width="200" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113232057.gif" width="200" />
有边框布局|带阴影的布局|Selector
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113233646.png" width="200"/>|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113234919.png" width="200" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114003639.gif" width="200" />

##### 这些效果是所有的布局都具有的通用属性，分别解释如下(以SuperRelativeLayout为例)：

#### 0x1 圆角
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200110235232.png" width="300" />

##### 代码
```
<top.androidman.SuperRelativeLayout
    android:layout_width="match_parent"
    android:layout_height="100dp"
    android:layout_margin="10dp"
    app:background_normalColor="@color/normal_color"
    app:corner="35dp" />
```
##### 属性解释
- 单独设置左下角角度<br>
    app:corner_leftBottom="0dp"
- 单独设置左上角角度<br>
    app:corner_leftTop="5dp"
- 单独设置右上角角度<br>
    app:corner_rightTop="22dp" 
- 单独设置右下角角度<br>
    app:corner_rightBottom="0dp"
- 按钮四个角的圆角角度<br>
    app:corner="10dp"
    
<font color="red">注意：单独设置角度会覆盖corner属性</font>

#### 0x2 颜色渐变

##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200111001246.png" width="300" />

##### 代码
```
<top.androidman.SuperRelativeLayout
    android:layout_width="match_parent"
    android:layout_height="100dp"
    android:layout_margin="10dp"
    app:background_colorOrientation="left_right"
    app:background_endColor="@color/end_color"
    app:background_startColor="@color/start_color"
    app:corner="35dp" />
```
##### 属性解释
- 开始颜色<br>
    app:background_startColor="@color/color_14c7de"
- 结束颜色<br>
    app:background_endColor="@color/color_red"
- 颜色渐变方向<br>
    app:background_colorOrientation="right_left"
    - top_bottom <br>从上到下
    - bottom_top <br>从下到上
    - left_right <br>从左到右
    - right_left <br>从右到左
    - tr_bl <br>从右上到左下
    - bl_tr <br>从左下到右上
    - br_tl <br>从右下到左上
    - tl_br <br>从左上到右下

<font color="red">注意：当设置颜色渐变时，background_normalColor将失效</font>

#### 0x3 默认点击效果
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113231146.gif" width="300" />

##### 代码
```
<top.androidman.SuperRelativeLayout
    android:layout_width="match_parent"
    android:layout_height="100dp"
    android:layout_gravity="center"
    android:layout_margin="10dp"
    app:background_normalColor="@color/green"
    app:corner="35dp"
    app:open_pressed_effect="true">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="开启点击效果"
        android:textColor="@color/color_white"
        android:textSize="22dp" />
</top.androidman.SuperRelativeLayout>
```
##### 属性解释
- 开启默认点击效果<br>
    app:open_pressed_effect="true"
    
<font color="red">注意：open_pressed_effect属性默认值是false，没有开启点击效果</font>

#### 0x4 形状
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113232057.gif" width="300" />

##### 代码
```
<top.androidman.SuperRelativeLayout
    android:layout_width="200dp"
    android:layout_height="200dp"
    android:layout_gravity="center"
    android:layout_margin="10dp"
    app:background_normalColor="@color/green"
    app:shape="circle">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="开启点击效果"
        android:textColor="@color/color_white"
        android:textSize="22dp" />
</top.androidman.SuperRelativeLayout>
```
##### 属性解释
- 形状，默认为矩形，可以设置为圆形<br>
    app:shape="circle"


#### 0x4 边框
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113233646.png" width="300" />

##### 代码
```
<top.androidman.SuperRelativeLayout
    android:layout_width="match_parent"
    android:layout_height="100dp"
    android:layout_margin="10dp"
    app:background_normalColor="#FDEDED"
    app:border_color="@color/color_14c7de"
    app:border_dashGapWidth="5dp"
    app:border_dashWidth="10dp"
    app:border_width="1dp"
    app:corner="35dp"
    app:corner_leftTop="0dp" />
```
##### 属性解释
- 边框宽度<br>
    app:border_width="2dp"
- 边框颜色<br>
    app:border_color="@color/color_red"
- 边框虚线宽度<br>
    app:border_dashWidth="5dp"
- 边框虚线间隙值<br>
    app:border_dashGapWidth="5dp"

### 0x5 带阴影的布局
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200113234919.png"/>

##### 代码
```
<top.androidman.SuperRelativeLayout
    android:layout_width="match_parent"
    android:layout_height="200dp"
    android:layout_margin="10dp"
    app:background_normalColor="@color/color_14c7de"
    app:corner="10dp"
    app:shadow_endColor="#00FFFFFF"
    app:shadow_size="10dp"
    app:shadow_startColor="@color/start_color" />
```
##### 属性解释
    
- 阴影开始颜色<br>
    app:shadow_startColor="@color/color_text_grey"
- 阴影开始颜色<br>
    app:shadow_endColor="@color/color_grey_divider_line"
- 阴影尺寸<br>
    app:shadow_size="10dp"

<font color="red">注意：需要这三个属性同时设置，阴影效果才会展示，当设置阴影时不支持设置shape相关属性，border相关属性，另外需要注意，阴影的尺寸会占用组件的大小，所以在设置阴影的时候需要注意</font>

### 0x6 Selector
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114003639.gif"/>

##### 代码
```
<top.androidman.SuperRelativeLayout
    android:layout_width="match_parent"
    android:layout_height="200dp"
    android:layout_margin="10dp"
    app:background_normalColor="@color/color_14c7de"
    app:background_pressedColor="@color/end_color"
    app:corner="10dp" />
```
##### 属性解释
- 当按钮点下时会显示设置的颜色效果<br>
    app:background_pressedColor="@color/color_accent"

### 二、SuperButton的独有属性
#### 效果演示

基本使用|带图标的按钮|没有文字的按钮
:---:|:---:|:---:
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114235503.png" width="300" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114234439.png" width="300"/>|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114235016.png" width="300" />

### 代码解释

#### 0x1 基本使用
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114235503.png"/>

##### 代码
```
<top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    app:background_normalColor="@color/color_accent"
    app:corner="10dp"
    app:text="@string/poetry_1"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
- 按钮文字<br>
    app:text="床前明月光"
- 按钮文字颜色 <br>
    app:textColor="@color/color_white"
- 按钮文字大小<br>
    app:textSize="22sp" 
- 按钮背景颜色<br>
    app:background_normalColor="@color/color_accent"

#### 0x2 带图标的按钮
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114234439.png"/>

##### 代码
```
<top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    app:background_normalColor="@color/color_red"
    app:corner="20dp"
    app:icon="@mipmap/icon_like"
    app:iconAuto="true"
    app:iconHeight="40dp"
    app:iconOrientation="right"
    app:iconPadding="20dp"
    app:iconWidth="40dp"
    app:text="图标在右边"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
- 图标<br>
    app:icon="@mipmap/icon_like"
- 图标在文字的方向(left、right、top、bottom)<br>
    app:iconOrientation="right"
- 图标的宽<br>
    app:iconWidth="40dp"
- 图标的高<br>
    app:iconHeight="40dp"
- 图标距文字距离<br>
    app:iconPadding="20dp"
- 根据文字大小缩放图标，默认为false<br>
    app:iconAuto="true"

<font color="red">注意：iconWidth和iconHeight属性要同时设置才生效，并且设置这两个属性的时候iconAuto属性会无效</font>

#### 0x3 没有文字的按钮
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200114235016.png"/>

##### 代码
```
<top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    app:background_normalColor="@color/color_red"
    app:corner="20dp"
    app:icon="@mipmap/icon_like"
    app:iconHeight="40dp"
    app:iconOrientation="right"
    app:iconPadding="20dp"
    app:iconWidth="40dp" />
```

<font color="red">注意：只设置图标不设置文字即可，由于shape是通用属性，所以按钮也可以设置</font>


### 三、SuperLine
##### 效果展示
![](https://ansnail.oss-cn-beijing.aliyuncs.com/superfamily/20200107232035.png)

##### 代码演示(上面从上到下，为了效果把直线宽设置为5dp)
```
<top.androidman.SuperLine
    android:layout_width="match_parent"
    android:layout_height="5dp"
    android:layout_margin="15dp"
    app:line_color="@color/color_start" />

<top.androidman.SuperLine
    android:layout_width="match_parent"
    android:layout_height="5dp"
    android:layout_margin="15dp"
    app:line_endColor="@color/color_end"
    app:line_startColor="@color/color_start" />

<top.androidman.SuperLine
    android:layout_width="match_parent"
    android:layout_height="5dp"
    android:layout_margin="15dp"
    app:line_endColor="@color/color_end"
    app:line_startColor="@color/color_start"
    app:line_dashGapWidth="5dp"
    app:line_dashWidth="10dp" />

<top.androidman.SuperLine
    android:layout_width="match_parent"
    android:layout_height="5dp"
    android:layout_margin="15dp"
    app:line_color="@color/color_start"
    app:line_dashGapColor="@color/color_accent"
    app:line_dashGapWidth="5dp"
    app:line_dashWidth="10dp" />

<top.androidman.SuperLine
    android:layout_width="5dp"
    android:layout_height="200dp"
    android:layout_margin="15dp"
    app:line_color="@color/color_start"
    app:line_dashGapColor="@color/color_accent"
    app:line_dashGapWidth="5dp"
    app:line_dashWidth="10dp" />
```
##### 属性介绍
- 线条方向,两个取值vertical和horizontal<br>
    app:orientation="vertical"
- 设置直线颜色<br>
    app:line_color="@color/color_start"
- 直线开始颜色<br>
    app:line_endColor="@color/color_end"
- 直线结束颜色<br>
    app:line_endColor="@color/color_end"
- 虚线宽度<br>
    app:line_dashWidth="10dp"
- 虚线间隙宽度<br>
    app:line_dashGapWidth="5dp"
- 虚线间隙的颜色<br>
    app:line_dashGapColor="@color/color_accent"

    
<font color="red">注意：superline会根据直线的宽和高自动计算直线的方向，所以正常可以不用设置orientation属性</font>

### 四、写在后面

如果以前用过superbutton的小伙伴会发现，新版本里面的属性有了一些变化，不过作者已经兼容了全部旧有属性所以大家可以放心使用，下面是部分新旧属性对照，希望小伙伴开始使用新属性

|旧属性|新属性|作用|
|--|--|--|
|color_normal|background_normalColor|正常背景颜色
|color_pressed|background_pressedColor|按压时的背景颜色
|color_start|background_startColor|开始颜色
|color_end|background_endColor|结束颜色
|color_direction|background_colorOrientation|颜色方向
|corner_left_top|corner_leftTop|左上角圆角半径
|corner_left_bottom|corner_leftBottom|左下角圆角半径
|corner_right_top|corner_rightTop|右上角圆角半径
|corner_right_bottom|corner_rightBottom|右下角圆角半径




### 背景
按钮应该是我们的App里面最普遍的组件之一了，特别常用。    
通常我们写一个按钮的套路很简单也很固定。大概分为以下几个步骤：

1. 在xml布局里面按照设计稿的尺寸位置写一个Textview
2. 按照设计稿规定的颜色和圆角在drawable目录下创建一个shape文件
3. 将这个shape文件作为Textview的背景

这样一个很标准的按钮就诞生了，然后就可以继续愉快的开发了。这本来没有什么问题，也比让UI妹纸切图高级了很多，但是随着开发的进行你会发现，UI妹纸的想法很多，不同的界面有各种不同圆角和不同背景颜色的按钮，这个时候你需要把上面的三个步骤再进行N次。

最后你会发现你的drawable目录下有各种各样的按钮背景资源，难以管理。特别是假如有的按钮要求有点击效果时需要使用selector，这个时候可能就会产生三个文件用来满足需求，所以总得来说很繁琐。

### 想法
基于以上原因以及按钮使用的普遍程度，感觉很有必要写一个使用简单且能满足日常各种需求的按钮。我们先梳理下按钮需要达到的效果：

1. 使用简单(即可以利用属性对按钮进行各种设置)
2. 可以支持设置按钮文字、按钮文字颜色、按钮文字大小
3. 可以支持统一设置圆角大小，也可以单独设置按钮每个圆角的大小
4. 可以支持设置按钮背景颜色
5. 可以支持selector
6. 可以支持圆形按钮
7. 可以支持渐变色按钮，可以支持各个方向设置渐变色
8. 可以支持设置带边框的按钮，可以设置边框的颜色和宽度
9. 可以支持设置按钮是否可以点击
10. 可以设置带图标的按钮，支持自定义按钮大小，和自动缩放，图标支持设置在文字上下左右四个方向，支持自定义文字距离图标的距离

### 注意

从1.2版本开始引入了默认点击效果，如果不想使用可以用“close_default_pressed”属性关闭掉，如果对默认点击效果的颜色不满意，可以通过“color_default_pressed”属性，设置需要的点击颜色效果

### 引入

[ ![Download](https://api.bintray.com/packages/androidman/maven/superbutton/images/download.svg?version=1.2.0) ](https://bintray.com/androidman/maven/superbutton/1.2.0/link)

```
implementation 'top.androidman:superbutton:1.2.0'
```
[Github传送门](https://github.com/ansnail/SuperButton)

### 实现效果（目前最低版本支持到16）

基本使用|单独设置每个圆角|Selector|圆形按钮
:---:|:---:|:---:|:---:
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711155020.png" width="200" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711171924.png" width="200"/>|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172054.gif" width="200" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172121.png" width="200" />
渐变背景的按钮|有边框按钮|按钮不可点击|带图标按钮
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172358.png" width="200" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172416.png" width="200"/>|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172439.png" width="200" />|<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172519.png" width="200" />
带阴影的按钮|边框带虚线的按钮||
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190724003633.png" width="200" />|||

### 代码解释

#### 0x1 基本使用
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711155020.png"/>

##### 代码
```
 <top.androidman.SuperButton
        android:layout_width="match_parent"
        android:layout_height="60dp"
        android:layout_margin="20dp"
        app:color_normal="@color/color_accent"
        app:corner="10dp"
        app:text="@string/poetry_1"
        app:textColor="@color/color_white"
        app:textSize="22sp" />
```
##### 属性解释
- 按钮文字<br>
    app:text="床前明月光"
- 按钮文字颜色 <br>
    app:textColor="@color/color_white"
- 按钮文字大小<br>
    app:textSize="22sp" 
- 按钮背景颜色<br>
    app:color_normal="@color/color_accent"
    
### 0x2 单独设置每个圆角
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711171924.png"/>

##### 代码
```
 <top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    app:color_normal="@color/color_6596ff"
    app:corner="40dp"
    app:corner_left_bottom="0dp"
    app:text="单独设置左下角为0dp"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
- 单独设置左下角角度<br>
    app:corner_left_bottom="0dp"
- 单独设置左上角角度<br>
    app:corner_left_top="5dp"
- 单独设置右上角角度<br>
    app:corner_right_top="22dp" 
- 单独设置右下角角度<br>
    app:corner_right_bottom="0dp"
- 按钮四个角的圆角角度<br>
    app:corner="10dp"
    
<font color="red">注意：单独设置角度会覆盖corner属性</font>
    
    
### 0x3 Selector
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172054.gif"/>

##### 代码
```
 <top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    android:onClick="test"
    app:color_normal="@color/color_accent"
    app:color_pressed="@color/color_ffB419"
    app:corner="10dp"
    app:text="点击会变色哦"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
- 当按钮点下时会显示设置的颜色效果<br>
    app:color_pressed="@color/color_accent"

    
### 0x4 圆形按钮
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172121.png"/>

##### 代码
```
 <top.androidman.SuperButton
    android:layout_width="160dp"
    android:layout_height="160dp"
    android:layout_margin="20dp"
    android:onClick="test"
    app:color_normal="@color/color_accent"
    app:drawable_middle="@mipmap/icon_like"
    app:drawable_middle_height="50dp"
    app:drawable_middle_width="50dp"
    app:shape="CIRCLE" />
```
##### 属性解释
- 按钮上只有图标没有文字<br>
    app:drawable_middle="@mipmap/icon_like"
- 按钮上图标高度<br>
    app:drawable_middle_height="50dp"
- 按钮上图标宽度<br>
    app:drawable_middle_width="50dp"
    
<font color="red">注意：当设置此属性时，文字的相关属性将会失效</font>


### 0x5 渐变背景的按钮
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172358.png"/>

##### 代码
```
 <top.androidman.superbutton.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    app:color_direction="RIGHT_LEFT"
    app:color_end="@color/color_14c7de"
    app:color_start="@color/color_red"
    app:corner="20dp"
    app:text="从右到左渐变"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
- 开始颜色<br>
    app:color_start="@color/color_14c7de"
- 结束颜色<br>
    app:color_end="@color/color_red"
- 颜色渐变方向<br>
    app:color_direction="RIGHT_LEFT"
    - TOP_BOTTOM <br>从上到下
    - BOTTOM_TOP <br>从下到上
    - LEFT_RIGHT <br>从左到右
    - RIGHT_LEFT <br>从右到左
    - TR_BL <br>从右上到左下
    - BL_TR <br>从左下到右上
    - BR_TL <br>从右下到左上
    - TL_BR <br>从左上到右下

<font color="red">注意：当设置颜色渐变时，color_normal，color_pressed设置将失效</font>

### 0x6 有边框按钮
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172416.png"/>

##### 代码
```
 <top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    app:border_color="@color/color_red"
    app:border_width="2dp"
    app:color_normal="@color/color_accent"
    app:corner="10dp"
    app:text="@string/poetry_1"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
- 边框宽度<br>
    app:border_width="2dp"
- 边框颜色<br>
    app:border_color="@color/color_red"
- 边框虚线宽度<br>
    app:border_dash_width="5dp"
- 边框虚线间隙值<br>
    app:border_dash_gap="5dp"

### 0x7 按钮不可点击
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172439.png"/>

##### 代码
```
<top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    android:onClick="test"
    app:button_click_able="false"
    app:color_normal="@color/color_accent"
    app:corner="10dp"
    app:singleLine="false"
    app:text="app:button_click_able=false\n也可以代码设置"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
    
- 按钮是否可以点击，默认为true可以点击<br>
    app:button_click_able="false"
- 按钮文字是否单行，默认为true单行<br>
    app:singleLine="false"
    
<font color="red">注意：按钮提供有方法对点击事件进行控制，请参考高级使用里面相关方法</font>

### 0x8 带图标按钮
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190711172519.png"/>

##### 代码
```
<top.androidman.superbutton.SuperButton
    android:layout_width="match_parent"
    android:layout_height="60dp"
    android:layout_margin="20dp"
    app:color_normal="@color/color_red"
    app:corner="20dp"
    app:drawable_padding="20dp"
    app:drawable_right="@mipmap/icon_like"
    app:text="图标在右边"
    app:textColor="@color/color_white"
    app:textSize="22sp" />
```
##### 属性解释
    
- 图标在文字右边<br>
    app:drawable_right="@mipmap/icon_like"
- 图标在文字左边<br>
    app:drawable_left="@mipmap/icon_like"
- 图标在文字上边<br>
    app:drawable_top="@mipmap/icon_like"
- 图标在文字下边<br>
    app:drawable_bottom="@mipmap/icon_like"
- 图标距文字距离<br>
    app:drawable_padding="20dp"
- 根据文字大小缩放图标，默认为true,当为false时显示原图标大小<br>
    app:drawable_auto="true"

### 0x9 带阴影的按钮
##### 效果
<img src="https://ansnail.oss-cn-beijing.aliyuncs.com/superbutton/20190724003633.png"/>

##### 代码
```
<top.androidman.SuperButton
    android:layout_width="match_parent"
    android:layout_height="100dp"
    android:layout_margin="20dp"
    app:color_normal="@color/color_accent"
    app:color_shadow_end="@color/color_grey_divider_line"
    app:color_shadow_start="@color/color_text_grey"
    app:corner="10dp"
    app:shadow_size="10dp"
    app:text="Shadow"
    app:textColor="@color/color_white"
    app:textSize="22dp" />
```
##### 属性解释
    
- 阴影开始颜色<br>
    app:color_shadow_start="@color/color_text_grey"
- 阴影开始颜色<br>
    app:color_shadow_end="@color/color_grey_divider_line"
- 阴影尺寸<br>
    app:shadow_size="10dp"

<font color="red">注意：需要这三个属性同时设置，阴影效果才会展示，当设置阴影时不支持设置shape相关属性，border相关属性，另外需要注意，阴影的尺寸会占用组件的大小，所以在设置阴影的时候需要注意</font>


### 按钮支持的所有属性
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="SuperButton">
        <!--默认配置-->
        <attr name="text" format="reference|string" />
        <!--按钮文字颜色-->
        <attr name="textColor" format="reference|color" />
        <!--按钮文字大小-->
        <attr name="textSize" format="dimension" />
        <!--文字是否单行，默认单行-->
        <attr name="singleLine" format="boolean" />

        <!--默认背景颜色-->
        <attr name="color_normal" format="reference|color" />
        <!--按压时的背景颜色-->
        <attr name="color_pressed" format="reference|color" />

        <!--图片在文字左边-->
        <attr name="drawable_left" format="reference|color" />
        <!--图片在文字右边-->
        <attr name="drawable_right" format="reference|color" />
        <!--图片在文字上边-->
        <attr name="drawable_top" format="reference|color" />
        <!--图片在文字下边-->
        <attr name="drawable_bottom" format="reference|color" />
        <!--图片距文字的距离-->
        <attr name="drawable_padding" format="dimension" />
        <!--图标根据文字大小自动缩放图标-->
        <attr name="drawable_auto" format="boolean" />

        <!--只有图片的情况,此时会忽略文字，即便设置-->
        <attr name="drawable_middle" format="reference|color" />
        <!--图片在中间时宽-->
        <attr name="drawable_middle_width" format="dimension" />
        <!--图片在中间时高-->
        <attr name="drawable_middle_height" format="dimension" />

        <!--形状-->
        <attr name="shape" format="enum">
            <!--圆形-->
            <enum name="CIRCLE" value="1" />
            <!--矩形-->
            <enum name="RECT" value="2" />
        </attr>

        <!--按钮背景是渐变色时设置-->
        <!--开始颜色-->
        <attr name="color_start" format="color" />
        <!--结束颜色-->
        <attr name="color_end" format="color" />
        <!--颜色方向-->
        <attr name="color_direction" format="enum">
            <!--从上到下-->
            <enum name="TOP_BOTTOM" value="0x1" />
            <!--从右上到左下-->
            <enum name="TR_BL" value="0x2" />
            <!--从右到左-->
            <enum name="RIGHT_LEFT" value="0x3" />
            <!--从右下到左上-->
            <enum name="BR_TL" value="0x4" />
            <!--从下到上-->
            <enum name="BOTTOM_TOP" value="0x5" />
            <!--从左下到右上-->
            <enum name="BL_TR" value="0x6" />
            <!--从左到右-->
            <enum name="LEFT_RIGHT" value="0x7" />
            <!--从左上到右下-->
            <enum name="TL_BR" value="0x8" />
        </attr>

        <!--按钮圆角，如果单独设置会覆盖此设置-->
        <attr name="corner" format="dimension" />
        <!--左上角圆角半径-->
        <attr name="corner_left_top" format="dimension" />
        <!--左下角圆角半径-->
        <attr name="corner_left_bottom" format="dimension" />
        <!--右上角圆角半径-->
        <attr name="corner_right_top" format="dimension" />
        <!--右下角圆角半径-->
        <attr name="corner_right_bottom" format="dimension" />

        <!--边框宽度-->
        <attr name="border_width" format="dimension" />
        <!--边框颜色-->
        <attr name="border_color" format="color" />
        <!--按钮是否可以点击-->
        <attr name="button_click_able" format="boolean" />

    </declare-styleable>
</resources>

```

### 高级应用
1. 想修改按钮相关调用如下方法：
```
    /**
     * 修改文字
     */
    superButton.setText(CharSequence text);

    /**
     * 修改文字颜色
     */
    superButton.setTextColor(@ColorInt int textColor);

    /**
     * 修改按钮背景颜色
     */
    superButton.setColorNormal(@ColorInt int colorNormal);

```

2. 如果想同时改变按钮的颜色和点击状态可以调用这个方法，注意，当按钮在不可点击状态恢复成可点击状态时，需要调用此方法同时修改颜色值，否则按钮依然是不可点击时的颜色，不过可以点击
```
    /**
     * 设置按钮颜色以及是否可以点击
     * 不影响color_pressed的值
     *
     * @param color           设置按钮的color_normal值
     * @param buttonClickable 设置按钮是否可点击
     */
    superButton.setButtonClickable(@ColorInt int color, boolean buttonClickable)
```

3. 如果只是想设置按钮不可点击，不需要改变按钮颜色，可以使用如下方法
```
    /**
     * 设置按钮是否可以点击
     */
    superButton.setButtonClickable(boolean buttonClickable);
```

### 未来展望

现在已经把按钮阴影加入进来，这个按钮的使用也更加方便啦！ 
大家有好的想法和需求，欢迎大家提issue。

### GitHub传送门

[客官点这里](https://github.com/ansnail/SuperButton)