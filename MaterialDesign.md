---
title:  MaterialDesign 
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


#Material Designer风格介绍
***

android 自推出以来，一直没有固定的风格，于是国内的产品与设计师大量的抄袭了IOS的风格，但是有些风格是不应该在android 手机上面出现的，因此android开发者被抄袭风格弄的苦不堪言。为了统一风格，Google I/O 2014 推出了一个Material Designer的风格，建议android应用都按照这个风格进行开发，Material Designer 除了有一部分是UI的规定外，也提供了很多绚丽的效果，下面我们就来看看什么是Material Designer

## 什么是 Material Design 

Material Design 是一种独一无二的底层系统，在这个系统的基础之上，构建跨平台和超越设备尺寸的统一体验。遵循基本的移动设计定则，同时支持触摸、语音、鼠标、键盘等输入方式。

![image](http://images.cnitblog.com/blog/651487/201411/071155051599008.png)

Material Design 有以下的特点：

1. 实体感的操作
2. 鲜明、形象的视觉效果
3. 有意义的动画效果

![image](http://images.cnitblog.com/blog/651487/201411/071159412687690.gif)

![image](http://images.cnitblog.com/blog/651487/201411/071155348625400.gif)

## Material Design 样式
### Material Designer 新增如下样式 

- @android:style/Theme.Material 
- @android:style/Theme.Material.Light
- @android:style/Theme.Material.Light.DarkActionBar

![image](http://images.cnitblog.com/blog/651487/201411/071616273627473.png)

5.0以后的版本我们可以根据样式内部的颜色值进行修改相应的内容的颜色

![image](http://images.cnitblog.com/blog/651487/201411/071629282842265.png)

我们可以在style文件中修改需要显示的样式

     <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">

        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        
     </style>

除了上面的方式以外，我们还有其他的方式来修改对应的颜色，注意以下的方法只在5.0以上的手机上能够生效

        Window window = getWindow();
        window.setStatusBarColor(ContextCompat.getColor(this, R.color.colorBlue));
        window.setNavigationBarColor(ContextCompat.getColor(this, R.color.colorGreen));

### 视图高度

我们在之前的开发中，知道了android 的坐标系，屏幕的左上角是坐标系的原点，代表 x y 分别是(0,0).在21版本以后，所有的控件还多了一个属性z。我们看看下图。

![](http://i.imgur.com/CmK7GHP.png)

也就是布局不是我们看到的平面了，控件还包括了Z坐标的值。

    android:translationZ
    setTranslationZ

![](http://i.imgur.com/kXEmUxS.png)

在设置了后面这个控件的z轴后

![](http://i.imgur.com/JdQaCAT.png)

![](http://i.imgur.com/I5WY5Mr.png)

我们看到已经更改了显示的顺序，就像图层一样。

除此之外android还提供了一个api用来设置控件的阴影，注意使用这个api要提供一个背景给控件才能生效。

     android:elevation

注意这些api都是21版本以上的才有，注意好版本适配

### 波纹触摸反馈

![image](http://images.cnitblog.com/blog/651487/201411/071159412687690.gif)

android 在5.0以后提供了一个触摸反馈的效果给开发者，开发者能够很轻松的实现以上的效果。触摸反馈分成两组：
​    
- 1 波纹无边界的 ?android:attr/selectableItemBackground

- 2 波纹带边界的 ?android:attr/selectableItemBackgroundBorderless

默认5.0以上的Button都提供了波纹的触摸反馈效果

因为这个效果只在5.0以上的手机有效果，所以我们需要适配不同版本的手机，新建一个适配21版本的layout

![](http://i.imgur.com/ML81oQz.png)

创建两个同名的布局文件，分别放置在layout与layout-21文件夹下

![](http://i.imgur.com/6QFyyvA.png)

布局文件如下

![](http://i.imgur.com/wgAeioW.png)

![](http://i.imgur.com/VOzIXua.png)

![](http://i.imgur.com/3KOo4Tc.png)

### ?与@的区别
我们一般获取某个资源，如图片、文字等，我们常常使用的@符号，如下面的例子获取黑色的颜色。
​          
          <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="has border"
            android:textColor="@android:color/black"
            android:textSize="22sp" />

但是我们如果有以下的需求，为了和当前的系统主题保持一致，我们常常需要获取当前应用主题与系统主题的一些属性，这些属性是会根据主题的变化发生变化，所以我们不能使用@符号取，@符号是取某个固定的值。在这种情况下面，我们需要使用?，?符号代表在当前的主题下面去获取值。

一般有两种，一种是获取当前应用的属性值?attr/，一种是获取当前系统主题的值?android:attr/

下面我们来尝试获取当前应用的属性

1 新建一个属性文件

![](http://i.imgur.com/yn0wZMc.png)

2 定义一个颜色的属性

![](http://i.imgur.com/zYxT9iG.png)

3 选择应用的样式

![](http://i.imgur.com/4GPn66p.png)
![](http://i.imgur.com/MRTzUZE.png)

4 使用应用的样式

![](http://i.imgur.com/BmzVUZe.png)

5 效果如下图

![](http://i.imgur.com/NeHfB1b.png)

## Material design 控件

  Material design 除了提供了一些样式之外，更提供了非常多使用的控件，为开发者提供了非常多的便利。

### CardView
CardView 是MD提供的一种带圆角、阴影的容器。效果如下图：

![image](http://www.jcodecraeer.com/uploads/20151025/1445743798116099.png)

CardView是google在suppurt包提供的，如果我们需要使用这个控件，我们需要增加这个控件的依赖。为项目增加依赖的方式有两种：

- 1 使用Gradle依赖
- 2 在本地找到相应版本的aar包，绑定

注意CarView的版本必须和v7包的版本一致。如下图：

![](http://i.imgur.com/VrQfsdA.png)

本地的资源包目录如下

![](http://i.imgur.com/9qLH00t.png)

使用的方法很简单,首先需要在xml文件中使用CardView

     <android.support.v7.widget.CardView
        android:layout_width="300dp"
        android:layout_height="300dp">
        
     </android.support.v7.widget.CardView>

CardView有以下特殊的属性:(需要导入自定义命名空间  xmlns:app="http://schemas.android.com/apk/res-auto")

- app:cardElevation：控件的阴影大小 
- app:cardCornerRadius：控件的圆角大小
- app:cardBackgroundColor：控件的背景颜色

![](http://i.imgur.com/ROUHERR.png)

###  TextInputLayout 

   android 在旧版本就提供了输入控件EditText，输入控件能够很好的满足我们的需求，但是
   进阶的输入控件，提供更加友善的界面.TextInputLayout可以作为EditText的父控件，能够将提示上浮，并自带文本字数控制的功能.<p>

![](http://i.imgur.com/Ar2sg2j.png)

   常用属性如下：

- app:hintAnimationEnabled 是否开启提示的动画
- app:counterEnabled 是否开启计数功能
- app:counterMaxLength 最多能够输入的字数总数
- android:hint 提示语


  常用的方法如下：<p>
   setError 设置错误提示语

1 使用TextInputLayout作为父控件包裹普通的EditText,并为这个控件设置相应的属性

![](http://i.imgur.com/Xkl84yE.png)

2 为TextInputLayout设置提示错误语

![](http://i.imgur.com/7XIaubu.png)

3 根据需求需要更改提示语与错误提示语的UI

    //修改提示语的样式 
    <style name="TextLabel" parent="TextAppearance.Design.Hint">
        <item name="android:textSize">33sp</item>
    </style>
    
    //修改错误提示语的样式 
    <style name="myError" parent="TextAppearance.Design.Error">
        <item name="android:textSize">33sp</item>
        <item name="android:textColor">@android:color/holo_red_dark</item>
    </style>

设置提示语的样式
​    
![](http://i.imgur.com/RM8qsKf.png)

！！！！注意，TextInputLayout有一个Bug，这个Bug在统计字数时超出个数时会抛出。建议使用统计字数功能的需要在style文件中加入这句话。

![](http://i.imgur.com/k8sHKCQ.png)

###  NestedScrollView

   android 在旧版本提供了一个控件ScrollView ,能够将内部的很长的控件滚动显示，但是我们在实际开发中难免会碰到这样的需求，如在一个ScrollView中，增加一个能够滚动的区域(如下图一)。或在一个列表控件（ListView RecyerView）中，除了能够上下滚动外，也可以对内部的某个滚动(如下图二)。在以前，我们要实现这样的功能需要重写触摸事件的传递。现在Material Design提供了一个进阶版本的ScrollView给我们使用。<p>


   ![](http://i.imgur.com/nepkusF.gif)

   ![](http://i.imgur.com/UuGRW0r.gif)


1 在ScrollView中插入NestedScrollView

   ![](http://i.imgur.com/FHVIq8i.png)

2 在列表中使用NestedScrollView

   ![](http://i.imgur.com/mg8jRMk.png)

###  FloatActionButton

 android 在 Material Designer 中提供了一种漂浮的按钮，我们可以使用这个控件开发出很酷炫的效果,如下图：

   ![](http://i.imgur.com/XDxWBWy.png)


 常用的属性：

- android:src 中间的icon
- app:backgroundTint 背景的颜色
- app:rippleColor 点击时的颜色
- app:borderWidth 应该设置为0，否则会在4.1会显示为正方形，而在5.0以后没有阴影效果
- app:fabSize 控件的大小，有两个值 normal和mini
- app:layout_anchor 设置FloatActionButton相对于那个控件
- app:elevation 默认显示的阴影的大小


 ![](http://i.imgur.com/3NqtnSG.png)


###  ToolBar

  google在旧版本推出过一个控件ActionBar,但是ActionBarzhi只能固定在顶部，不能灵活使用，所以google推出了一个ToolBar来替换ActionBar,我们可以配合一些新的控件实现很多酷炫的效果。下图是ToolBar内部显示的内容

  ![image]( http://www.jcodecraeer.com/uploads/20141118/1416285884351.png)

  在xml中使用ToolBar  

  ![](http://i.imgur.com/33PJclw.png)

  设置ToolBar的显示的属性

  ![](http://i.imgur.com/A5sDVDl.png)
​         
###  Snackbar 

   Toast是我们在日常开发中经常使用的控件，简单易用，但是现在有这样的需求，需要与Toast交互，比如登陆失败了，弹出Toast后，点击Toast能够重新登陆，但是就目前的Toast来说是无法解决这种问题的。因此google提供了一个新的控件给开发者，Snackbar。Snackbar除了有Toast的功能外，还具备了Toast不具备的交互功能。

 1 生成一个 Snackbar

    make(View view, CharSequence text, int duration)    
    //view 某一个控件，系统通过这个控件向上寻找到根控件，把SnackBar显示出来
    //text Snackbar的提示语
    //duration Snackbar的显示时长 （LENGTH_LONG、LENGTH_SHORT、LENGTH_INDEFINITE）


 2 设置Snackbar的点击方法

    setAction(CharSequence text, final OnClickListener listener)    
​    

   ![](http://i.imgur.com/yPR4vF7.png)

###  CoordinatorLayout

   目前市面上常常能够看到一些很炫的UI效果，比如说，顶部显示一个图片，底部是一个列表，当滚动到顶部时，顶部的图片发生折叠。这种效果需要多个控件进行配合。<p>
   CoordinatorLayout 是这样一种控件，他能够根据一种机制，协调两个控件的操作。如滑动列表，顶部的图片也跟着压缩。

   ![](http://i.imgur.com/Xdhvqdo.png)

   ![](http://i.imgur.com/goggL0G.png)

   ![](http://i.imgur.com/T1Y1dI5.png)

   AppBarLayout继承自LinearLayout，布局方向为垂直方向。它内部有个机制就是当某个可滚动View的滚动手势发生变化时，他内部的控件也发生相应的变化。

   如这个例子内部可滚动的控件是RecyclerView,于是我们给这个RecyclerView指定一个 app:layout_behavior="@string/appbar_scrolling_view_behavior" appbar_scrolling_view_behavior 对应的类是android.support.design.widget.AppBarLayout$ScrollingViewBehavior,描述了RecyclerView与AppBarLayout之间的依赖关系。RecyclerView的任意滚动事件都将触发AppBarLayout或者AppBarLayout里面view的改变。

   那当RecyclerView滚动时，AppBarLayout的子View会发生什么变化呢，我们可以通过app:layout_scrollFlags这个参数来进行设置

-  scroll：值设为scroll的子控件会与滚动控件一起发生移动
-  enterAlways： 先滚动子控件，在滚动可滚动的控件
   - enterAlwaysCollapsed：当滚动View向下滑动时，先enterAlways，当View的高度达到最小高度时，View就暂时不去往下滚动，直到滚动View滑动到顶部不再滑动时，View再继续往下滑动，直到滑到View的顶部结束。
   - exitUntilCollapsed：当滚动View向上滑动时， View先缩小到最小尺寸前，滚动View都不会滚动。
   - snap: 子控件滚动到一定位置的时候，自动显示和隐藏。

    因为我们现在做的只是拉升 ，我们来实现之前说的效果

    ![](file://///Users/kay/Desktop/mdImage/93.png)

    CollapsingToolbarLayout，这个类能够给我们提供ToolBar折叠的效果，我们给它设置滚动的效果.<p>
    我们在CollapsingToolbarLayout放置了一个ImageView，为这个ImageView指定了视差滚动效果，什么叫视差滚动效果，就是滚得比其他控件稍微慢一点。
   ​    
        app:layout_collapseMode="parallax"
     
  而ToolBar我们不希望能够滚动，我们就给它设置

        app:layout_collapseMode="pin"

最后加上FloatActionBar

 ![](http://i.imgur.com/gY3i1KY.png)

最终效果

 ![](http://i.imgur.com/S1BfnTz.png)

 ![](http://i.imgur.com/dEaNDRH.png)

 我们还可以给这个加个标题

 ![](http://i.imgur.com/G8FfxLY.png)

 ![](http://i.imgur.com/EF1rpfL.png)

 ![](http://i.imgur.com/uHaAHDh.png)

我们刚刚做出来这个效果，但是我们还是不知道为什么会能产生这样的效果，我们来分析一下CoordinatorLayout,还记得我们之前给RecyleView配置了layout_behavior。之前我们告诉大家，这个是当一个控件的位置，大小发生变化的时候，相应的控件的也会发生变化。

我们来写一个最简单的behavior。编写一个与另一个控件一起动的TextView

 首先，我们先写一个布局，这个页面包含一个ImageView与一个TextView。

 ![](http://i.imgur.com/rEqzJkd.png)

 ![](http://i.imgur.com/R4UmmF1.png)

 我们现在写的布局两个控件是不会联动的，这个时候，我们需要使用CoordinatorLayout提供的behavior，告诉CoordinatorLayout如何联动两个控件。

 ![](http://i.imgur.com/86q7ZTz.png)

 ![](http://i.imgur.com/zice2kt.png)

 在布局中声明相应的动作

 ![](http://i.imgur.com/mhNYa6y.png)

我们再来写一个behavior，behavior除了可以监控控件的位置改变，还可以监控滚动控件的状态。

上面是一个很简单的behavior。下面我们再写一个稍微复杂一点的behavior

 ![](http://i.imgur.com/bxJjkkd.png)

 ![](http://i.imgur.com/Z5YIXU0.png)

 我希望做这样一个效果，当内容滑动到顶部时，显示顶部的图片。当内容滑下来时候，显示标题

 ![](http://i.imgur.com/XDfJeEJ.png)

 ![](http://i.imgur.com/DaWE9dK.png)

 ![](http://i.imgur.com/l9k9bVj.png)

 ![](http://i.imgur.com/tr4lK5K.png)

 布局写好了，我来给大家分析一下

 ![](http://i.imgur.com/9od8K4Z.png)

 页面分成3各部分，其中第一个部分就是我们的顶部，根据需求是不是第二部分到达顶部，就显示图片。那我们就可以实现一个behavior

 更改的控件是RelativeLayout,所以在代码中泛型中声明为RelativeLaout,注意要显示实现behavior的默认构造方法

 ![](http://i.imgur.com/ylMZ81C.png)

 重现layoutDependOn方法告诉父控件以哪个控件为参照，我们以最下面的滚动控件作为参考。

 ![](http://i.imgur.com/R9X20OT.png)

 修改onViewChange方法，当控件的位置发生变化的时候，回调这个方法，我们根据滚动控件的位置决定图片是否显示

 ![](http://i.imgur.com/4qnnZBn.png)

最后将这个behavior赋给需要更改的控件

 ![](file://///Users/kay/Desktop/mdImage/154.png)

注意：

如果在5.0以上的手机，注意要给顶部的条设置z轴。 

## Palette

Material Design 建议使用大色块来进行显示需要加重的内容，我们常常需要UI人员进行配合才能实现相应的功能，但是在Material Design中，google提供了一个工具类给我们，让我们可以根据图片获取相应的对应的颜色，能够动态的显示在UI上面。

我们来做一个动态更改标题颜色的界面,界面如下图，每当滑动完成后动态的去获取颜色值，然后进行设置

![](http://i.imgur.com/kBSyv2g.png)

核心的api<p>

（1）根据一张图片生成一个取色器

    //同步的方式生成一个取色器，会卡顿UI 
    Palette.from(BitMap).generate();
    //异步的方式生成一个取色器
    Palette.from(BitMap).generate(PaletteAsyncListener lis)；

（2）获取这个取色器内部的颜色，！！！这些颜色可能为空，使用前需要做非空判断

- Vibrant （有活力）
- Vibrant dark（有活力 暗色）
- Vibrant light（有活力 亮色）
- Muted （柔和）
- Muted dark（柔和 暗色）
- Muted light（柔和 亮色）

 首先先编写UI界面

![](http://i.imgur.com/IkUaq4o.png)

将图片放入我们的资源文件夹内

![](http://i.imgur.com/ZTVNHdg.png)

找到各个控件

![](http://i.imgur.com/yBRyAiP.png)

编写中间的ViewPager的adapter

![](http://i.imgur.com/wvPxhQN.png)

填充Viewpager的数据和页面

![](http://i.imgur.com/5Zh1zmg.png)

编写更改颜色的方法
生成一个取色器，注意取颜色时必须做好非空判断处理

![](http://i.imgur.com/ije2WBX.png)
![](http://i.imgur.com/6oE0Sw5.png)

因为我们需要更新UI，但是这个取色器可能会阻塞UI，所以我们使用一个类，HandleThread,这是一个带Handler的线程，会一直运行直到我们终止它。

![](http://i.imgur.com/7w1ZsOC.png) 

绑定一个Handler

![](http://i.imgur.com/sj3RNZl.png)

因为默认显示第一张图片所以我们在一开始应该生成第一张图片的取色器

![](http://i.imgur.com/4C6VIor.png)

接着我们实现滚动监听

![](http://i.imgur.com/xyxKEmK.png)
![](http://i.imgur.com/EYjnG7B.png)

最后我们必须在退出这个页面后，将这个线程终止

![](http://i.imgur.com/7laO2Pu.png)

## ActivityOptionsCompat 更好的过渡效果
在旧版本里面，我们切换Activity大多都是使用下面这个api
​    
     overridePendingTransition(enterAnim, exitAnim);

这个api是使用动画进行切换，使用简单，但是有一个问题就是，效果太过生硬，所以google在V4 support包内提供了一个向下兼容的类，供我们使用，ActivityOptionsCompat，我们可以使用这个类开发出很绚丽的跳转效果。ActivityOptionsCompat提供了一下几个过渡的效果

### 1 makeCustomAnimation

     makeCustomAnimation (Context context, int enterResId, int exitResId)

类似overridePendingTransition的功能，为两个activity设置了过渡动画，enterResId 是进入activity的动画，exitResId是退出的activity的动画


### 2 makeScaleUpAnimation

      makeScaleUpAnimation (View source, int startX,int startY, int width,int height)  

新的activity产生一个缩放的动画，这个动画的起点是，相对于source这个View 的左上角偏移（startX，startY）位置产生一个动画，新的activity的初始宽度和高度是width 和 height。
![](http://i.imgur.com/tohDbPu.png)

### 3 makeThumbnailScaleUpAnimation

     makeThumbnailScaleUpAnimation(View source,
            Bitmap thumbnail, int startX, int startY) 

 新的activity产生一个缩放的动画，这个动画的起点是，相对于source这个View 的左上角偏移（startX，startY）位置产生一个动画，新的activity的初始宽度和高度是这个bitmap的宽高      

 ![](http://i.imgur.com/GaNche8.png)      

### 4 makeSceneTransitionAnimation     

新的activity产生一个过渡动画，动画由两个页面的相同元素生成，这种效果只支持5.0以上的手机。

 ![](http://i.imgur.com/pZEPDga.png)

 ![](http://i.imgur.com/vc88qCc.png)     
​     
 ![](http://i.imgur.com/cNiSrhX.png)  



    makeSceneTransitionAnimation(Activity activity,
            View sharedElement, String sharedElementName)            
    
    makeSceneTransitionAnimation(Activity activity,
            Pair<View, String>... sharedElements)


 ![](http://i.imgur.com/Ax1ih34.png)

##更简单的动画系统

google 在旧版本的系统中提供了View Animation与Propery Animator,两套动画系统能够使开发者方便的完成动画的显示，但是为了实现一些效果，开发者仍需要编写大量的代码进行完成。因为我们常常使用的位移、隐藏等动画，在5.0版本以后，开发人员只要写好布局，动画系统会自动的把相应的动画显示出来，大大的减少重复的代码开发的工作量。

这个动画系统叫做transition。

### Scene（场景）

android 在transition动画中提出一个概念叫做场景，什么叫做场景？场景就是一个布局或部分布局，我们可以使用场景来创建动画。

下面是我们经常使用的api

1 生成一个Scene

    getSceneForLayout(ViewGroup sceneRoot, int layoutId, Context context)

2 切换一个场景

    //默认的切换的方法
    TransitionManager.go(Scene scene) 
    
    TransitionManager.go(Scene scene, Transition transition)  

3 延迟场景变化，TransitionManager就会根据场景变化自动执行动画
​     
    TransitionManager.beginDelayedTransition(Viewgroup group) 

我们写一个这样的布局，布局顶部是一个FrameLayout，底部是4个按钮

![](http://i.imgur.com/HH5HsPP.png)

![](http://i.imgur.com/VFE3m5k.png)

我们在onCreate方法内部增加一个场景，并执行这个场景。

![](http://i.imgur.com/eN4P0s1.png)

![](http://i.imgur.com/OMy3GaA.png)

效果图如下

![](http://i.imgur.com/UorEL2X.png) 
![](http://i.imgur.com/OIXGVq3.png) 

这四个场景的布局文件如下图，我们稍微把这四个按钮的位置调整一下

![](http://i.imgur.com/PoQCjGM.png) 

为 activity 内的四个按钮设置点击事件，设置完后，我们就能够看到效果了

![](http://i.imgur.com/G68oDA5.png)

我们没有写一句代码就实现了动画，但是现在这个动画的效果还不是我们想要的。我们可以使用另外一个方法来自定义动画。


     TransitionManager.go(Scene scene, Transition transition)  

我们之前使用的动画都是animation 或者 animator两种，还没有见过Transition。

#### Transition（变化）

Transition 是类似于我们常见的动画ViewAnimation一样，是系统为我们提供的改变UI提供的动画。与传统的动画不一样，我们不需要计算相应的起点与终点，系统会根据控件的变化自动的为我们生成相应的动画。我们在使用共享元素切换的时候，能够使用Transition进行切换，常见的Transition：

- Slide   划入
- Explode 爆炸
- Fade    隐藏
- changeBounds 位置与大小变化

我们把上面的点击事件改一下

![](http://i.imgur.com/1DI6inN.png)

Transition不同于我们之前写的动画，之前的动画，我们需要计算控件的开始和结束位置，再为动画设置一定的属性，系统会根据父控件的里面的子控件的变化，自动生成相对应的动画，不需要自己来做。

#### beginDelayedTransition

我们编写下面这个布局

![](http://i.imgur.com/GKqZ6Iu.png)

正常来说我们店家上面这个按钮，下面的TextView出现，就设置显示的属性即可，但是如果想更加美观，只能使用动画了。

![](http://i.imgur.com/1FLGNxz.png) 

上面的代码是使用默认的动画，我们可以使用自定义的动画，比如我在点击按钮的时候，将文本从右边滑入。

![](http://i.imgur.com/ikJBuJ3.png)

#### explose 

接着我们看看下面这个例子

![](http://i.imgur.com/GNeQ5Rm.png)

![](http://i.imgur.com/TcMaMgp.png) 

![](http://i.imgur.com/H0IYky6.png)

![](http://i.imgur.com/j3bwuAl.png)

完成上面的代码后，我们可以看到效果如下

![](http://i.imgur.com/55FXDIP.png)

最后我希望做一个点击后，爆炸的效果，我们需要监听RecyleView的数据变化，当点击后，将RecyleView制空

![](http://i.imgur.com/OLe7Cv1.png)

#### Transition 与 Activity

通常我们会在activity切换的时候使用动画。以前我们使用的 overridePendingTransition(int enterAnim, int exitAnim),但是动画的效果不很好看，在21版本以后我们可以使用transition在Activity切换过程中。

需要使用这些动画的时候，我们必须设置一些配置：

1  新建一个values-v21文件夹

![](http://i.imgur.com/HYjSrtK.png)

2  新建一个style.xml文件

3  在style文件内部增加一个样式

![](http://i.imgur.com/sZpI4TI.png)

只有设置了这个参数后才会生效。除了可以在xml里面设置，我们也可以在代码里面设置

![](http://i.imgur.com/GTYjDsO.png)

我们编写一个这样的布局，当点击中间的按钮后跳转

![](http://i.imgur.com/n2K1MwM.png)

Transition 与 Activity的跳转动画有以下几个

- setEnterTransition 进入的动画
- setExitTransition  退出的动画
- setReturnTransition 返回的动画
- setReenterTransition 重入的动画

![](http://i.imgur.com/j1F3qnL.png)

注意跳转的时候，不能使用旧的startActivity，要使用对的api

#### Transition 与 xml

旧版本的动画都能够使用xml来进行定义，Transition同样可以使用xml定义。

与animation 与animtor不一样，transition是放在独立的文件夹中

![](http://i.imgur.com/eETn90q.png)

![](http://i.imgur.com/D5H8YKz.png)


### 波纹动画

MD动画中又大量波纹动画，我们来看看如何通过代码来实现。注意下面的api是5.0以上的系统提供的，注意好版本判断。

     ViewAnimationUtils.createCircularReveal(View view,int centerX,int centerY,float startRadius, float endRadius)

 view 用来显示圆形动画的控件
 centerX 圆心的坐标X轴
 centerY 圆心的坐标Y轴
 startRadius 动画开始圆形的半径
 endRadius 动画结束时圆形的半径

 接下来我们来做一个最简单的波纹动画的例子,下面是这个例子的布局

![](http://i.imgur.com/4txYA4N.png)

 我们为这个布局设置一个波纹动画。

![](http://i.imgur.com/pnYq19k.png)

#### 波纹动画与过场动画的结合

![image](http://images0.cnblogs.com/blog2015/690927/201506/301311112437897.gif)

自从Material designer 推出以来，各种应用否推出了上面图片的效果，我们今天使用过场动画加波纹动画，能够实现比上面的图片更绚丽的效果。

这个界面是一开始的界面，当点击了按钮后，红色的圆就会飞向下一个activity

![](http://i.imgur.com/mbtgREg.png)

![](http://i.imgur.com/dj6UJ9B.png)

首先我们先写第一个界面

![](http://i.imgur.com/KG4qinz.png)

因为我们要显示一个圆形，所以我们创建一个shape文件

![](http://i.imgur.com/MPTnQe0.png)

因为这个图形到下一个activity也要使用圆形，所以我们得考虑一种通用的解决方案，最好不要创建多张图片。这个时候，md提供了一个新的模式给我们，着色模式。android:tint。使用这个属性会对图案进行着色。

![](http://i.imgur.com/RXjYhXe.png)

![](http://i.imgur.com/I8bt0Fs.png)

布局写好以后，我们开始编写跳转动画的代码。首先设置这个Activity的退出动画的代码

![](http://i.imgur.com/tqmL7lh.png)

编写共享过渡动画，注意，两个同样的元素的transitionName必须一样。

![](http://i.imgur.com/9m6Fh9k.png)

![](http://i.imgur.com/6hMHmxe.png)

接着新建一个Activity，编写布局

![](http://i.imgur.com/aIbpRoY.png)

设置新的activity的进入动画，并设置监听

![](http://i.imgur.com/o7TraMZ.png)

![](http://i.imgur.com/zusJQoy.png)

![](http://i.imgur.com/YbLjVly.png)

### 综合练习 Md版本登陆注册界面
1 新建工程

2 新建一个Activity LoginActivity

3 编写登陆页面的UI

需实现如下的效果

![](http://i.imgur.com/kIyJuNA.png)

引入CardView控件

![](http://i.imgur.com/p10d3Lb.png)

增加头部的标题

![](http://i.imgur.com/f1JqnXJ.png)

增加用户名输入框，使用TextInputLayout包裹，开启动画

![](http://i.imgur.com/k2rn6Nt.png)

增加密码输入框，使用TextInputLayout包裹，开启动画

![](http://i.imgur.com/f15RFXx.png)

增加GO按钮

![](http://i.imgur.com/ebj7qOQ.png)

为GO按钮增加背景

![](http://i.imgur.com/Pgobw9f.png)

增加FloatingActionButton

![](http://i.imgur.com/hMyOQjP.png)

编写完成布局后，显示如下图

![](http://i.imgur.com/nBvUIjz.png)

为了做到切换的效果，我们需要编写一个注册的Activity

![](http://i.imgur.com/wQh5CqJ.png)

编写注册页面的UI

![](http://i.imgur.com/ZXKqG4z.png)

![](http://i.imgur.com/bdZ39D5.png)

![](http://i.imgur.com/5UPTI4N.png)

![](http://i.imgur.com/7DxqU0o.png)

![](http://i.imgur.com/M25L5Ax.png)

![](http://i.imgur.com/50Crn55.png)

![](http://i.imgur.com/4MlgRSS.png)

为了实现叠加的效果，我们必须修改登录页面的样式，为注册页面注册为透明。

![](http://i.imgur.com/98jLyVj.png)

![](http://i.imgur.com/bMtfhew.png)

为了登录界面增加点击效果，取消动画过场效果，使用FloatingActionButton制作共享动画
![](http://i.imgur.com/i0u65dD.png)

为注册页面设置过场动画，ChangeBounds为将FloatingActionButton实现位移动画

![](http://i.imgur.com/8bbDqlb.png)

编写波纹动画，波纹的开始时fab大小，最后变成cradView的高度，当动画结束后，将cardView显示出来。

![](http://i.imgur.com/8vmFqcW.png)

为过场动画增加监听，当过场动画结束后，播放波纹动画

![](http://i.imgur.com/YZXt9lY.png)

![](http://i.imgur.com/cH8YMod.png)

编写波纹消失动画，当动画结束后，cardView隐藏

![](http://i.imgur.com/73bPI8I.png)

重写注册的返回方法

![](http://i.imgur.com/KGlaZXx.png)


### 动态权限申请

在6.0以上的手机，android对权限进行了更加精细的管理。我们除了使用原来的权限申请方法以外，在6.0的系统也要做。

在以前的版本中，如果应用需要使用什么权限，我们将需要的权限在清单文件中配置好。但是在6.0以后，系统对某些敏感的权限做了更细化的管理，应用在使用这些权限的时候必须重新的向用户申请。用户同意后方可使用。

下面的这些权限都是需要动态申请的：

      group:android.permission-group.CONTACTS
    	permission:android.permission.WRITE_CONTACTS
    	permission:android.permission.GET_ACCOUNTS    
    	permission:android.permission.READ_CONTACTS

  	  group:android.permission-group.PHONE
    	permission:android.permission.READ_CALL_LOG
    	permission:android.permission.READ_PHONE_STATE 
    	permission:android.permission.CALL_PHONE
    	permission:android.permission.WRITE_CALL_LOG
    	permission:android.permission.USE_SIP
    	permission:android.permission.PROCESS_OUTGOING_CALLS
    	permission:com.android.voicemail.permission.ADD_VOICEMAIL

  	  group:android.permission-group.CALENDAR
    	permission:android.permission.READ_CALENDAR
    	permission:android.permission.WRITE_CALENDAR

  	  group:android.permission-group.CAMERA
    	permission:android.permission.CAMERA

  	  group:android.permission-group.SENSORS
        permission:android.permission.BODY_SENSORS

  	  group:android.permission-group.LOCATION
    	permission:android.permission.ACCESS_FINE_LOCATION
    	permission:android.permission.ACCESS_COARSE_LOCATION
    
      group:android.permission-group.STORAGE
        permission:android.permission.READ_EXTERNAL_STORAGE
        permission:android.permission.WRITE_EXTERNAL_STORAGE
    
      group:android.permission-group.MICROPHONE
        permission:android.permission.RECORD_AUDIO

  	  group:android.permission-group.SMS
    	permission:android.permission.READ_SMS
    	permission:android.permission.RECEIVE_WAP_PUSH
    	permission:android.permission.RECEIVE_MMS
    	permission:android.permission.RECEIVE_SMS
    	permission:android.permission.SEND_SMS
    	permission:android.permission.READ_CELL_BROADCASTS

申请的步骤如下：

 1 在AndroidManifest.xml中申请你需要的权限，包括普通权限和需要申请的特殊权限。

 2 在应用运行的时候，先去判断当前应用是否获得需要使用的权限。

 3 如果没有获得相应的权限，向系统申请相应的权限。

 4 在页面的回调处进行处理，我们可以得到相应的权限申请的情况。

 核心的api

 ![](http://i.imgur.com/2J14O56.png)

 ![](http://i.imgur.com/bmhdQY6.png)

 请求权限的回调
​     
 ![](http://i.imgur.com/2WoJeHh.png)

 当用户拒绝了一次权限申请后，应用应该为这个申请说明原因

 ![](http://i.imgur.com/mSgRLpt.png)

 我们写一个在6.0系统下申请sd卡读写权限的例子

 首先先写一个保存文件的方法

  ![](http://i.imgur.com/TusbnHh.png)

  ![](http://i.imgur.com/WvR6ngT.png)

 当没有权限的时候我们必须去申请权限

 ![](http://i.imgur.com/TwFAmSb.png)

 ![](http://i.imgur.com/5G5I8C4.png)

 ![](http://i.imgur.com/C4Xbfln.png)

 处理用户的返回，如果用户拒绝了两次，就直接去到系统设置页面

 ![](http://i.imgur.com/CxZoXal.png)

 ![](http://i.imgur.com/MUgBrqX.png)

 注意:

 如果你的应用不想使用动态权限申请，或者说你们工作还没有做好准备的话，建议将build.gradle的targetSdkVersion设置为23以下。

 ![](http://i.imgur.com/CjXBOCc.png)


 小米的手机在动态申请权限和原生的有点不一样，如果被用户拒绝了一次后，shouldShowRequestPermissionRationale 总是返回false，不会给你向用户解释的机会  