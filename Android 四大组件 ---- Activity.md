---
title: Android 四大组件 ---- Activity
tags: Activity
grammar_cjkRuby: true
---


注意:所有的四大组件都必须在AndroidManifest.xml文件中配置

一,创建一个简单的Activity
1.创建一个Class文件并继承Activity

``` stylus
public class SplashActivity extends Activity {
    
}
```


2.重写onCreate方法

``` stylus
protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
```


3.因为每一个Activity对应一个布局,所以要创建一个布局
①在res/layout创建Android XML File
②编辑布局

``` stylus
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="这是测试页面"/>
</LinearLayout>
```


4.返回Activity,在onCreate添加布局:setContentView(R.layout.布局名),绑定这个Activity对应的布局

``` stylus
@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        **setContentView(R.layout.layout_splash);**
    }
```


5.这些都写好后,Activity基本上是完成了,还差最后的一步,就是要在AndroidManifest.xml文件中配置,在application中间添加<activity>

``` stylus
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.simon.baseapplication">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/AppTheme">
        **<activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>**
    </application>

</manifest>
```
说明:
android:label 指定的是活动中标题栏的内容,还会成为启动器(Launcher)中应用程序显示的名称

``` stylus
 <intent-filter>
                <action android:name="android.intent.action.MAIN"/>
                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
```
这个标签里的两个标签作用是把这个Activity当成是程序打开后启动的第一个页面,如果有多个Activity编辑了这两个标签,会弹出一个对话框让你选择启动哪一个Activity

好,配置完毕,可以用模拟器启动了 

![enter description here][1]
![enter description here][2]


二,活动的生命周期
1.活动的生命周期
Activity中定义了7个回调的方法,覆盖了整个活动的生命周期,下面来介绍下:
![enter description here][3]

onCreate():活动被创建时就会被调用.
onStart():由不可见到可见时调用.
onResume():失去焦点,不可点击时调用
onPause():重新获取焦点时调用
onStop():不可见时会调用
onDestroy():被销毁时调用
onRestart();由停止状态到运行状态之前调用

如果活动被回收了,但是页面可能存在临时数据,这时候如果活动被回收了,活动里的数据也就一起被销毁了,这是会严重影响用户体验的
这是就需要使用官方提供的一个方法onSaveInstanceState()回调方法

``` stylus
 @Override
    public void onSaveInstanceState(Bundle outState, PersistableBundle outPersistentState) {
        super.onSaveInstanceState(outState, outPersistentState);
    }
```

2.活动的启动模式
启动模式有4种:standard, singleTop, singleTask, singleInstance
可以在AndroidManifest.xml中通过给<Activity>标签指定Android:launchMode属性来启动
①standard : 每次启动都会创建该活动的一个新的实例.
②singleTop : 如果活动已经处于栈顶,系统将不会再创建一个新的实例,而是会直接使用栈顶的活动;
③singleTask : 每次启动活动的时候系统会首先检查栈中是否有该活动的实例,如果有,系统会直接使用该实例,并把该活动之上的其他活动通通出栈;
④singleInstance :  系统会启动一个新的栈来管理这个活动,不管是哪个应用程序来访问这个活动,都公用的同一个返回栈,解决了共享活动实例的问题.


Activity拓展:
1.隐藏标题栏
如果是继承AppCompatActivity,添加的是supportRequestWindowFeature(Window.FEATURE_NO_TITLE);
``` stylus
 protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        **requestWindowFeature(Window.FEATURE_NO_TITLE);**
        setContentView(R.layout.activity_main);
    }
```

2.使用吐司(Toast)
Toast.makeText(MainActivity.this, "这是一个吐司", Toast.LENGTH_SHORT).show();

3.使用Menu
①在res新建一个menu文件夹
②在menu文件夹创建一个Android Xml File
③编辑布局添加item

``` stylus
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto">

    <item
        android:id="@+id/add_item"
        android:title="Add"/>
    <item
        android:id="@+id/remove_item"
        android:title="Remove"/>

</menu>
```
④回到Activity,重写onCreateOptionsMenu方法

``` stylus
 @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.main,menu);
        return true;
    }
```
⑤菜单响应事件
重写onOptionsItemSelected

``` stylus
 @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        switch (item.getItemId()){
            case R.id.add_item:
                Toast.makeText(MainActivity.this, "添加", Toast.LENGTH_SHORT).show();
                break;
            case R.id.remove_item:
                Toast.makeText(MainActivity.this, "删除", Toast.LENGTH_SHORT).show();
                break;
            default:

        }
        return true;
    }
```
效果:

![enter description here][4]


  [1]: ./images/Activity_2.png "Activity"
  [2]: ./images/Activity2_1.png "Activity2"
  [3]: ./images/0_1314838777He6C.gif "0_1314838777He6C"
  [4]: ./images/Activity3_1.png "Activity3"