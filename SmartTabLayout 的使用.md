---
title: SmartTabLayout 的使用
tags: tab,viewpager,adapter
grammar_cjkRuby: true
---


SmartTabLayout是第三方库,用于标题的切换操作

使用方法:
1.导入库
     ①可以直接导入包中的libary Module ,然后在添加依赖:Module dependency
	 ②或者导入arr文件,先在project的build.gradle中加上本地依赖
	 

``` stylus
allprojects {
    repositories {
        jcenter()
        flatDir {
            dirs 'libs'
        }
    }
}
```
然后在自己的Module的build.gradle中添加以下代码

``` stylus
//compile(name:aar'的文件名',ext:'aar')
compile(name:'smartTabLayout',ext:'aar')
```

2.导入成功后,直接使用控件,并配置属性,这是基本用的属性配置,还有很多可以从github上搜索

``` stylus
<com.ogaclejapan.smarttablayout.SmartTabLayout
            android:id="@+id/viewPagerTab"
            android:layout_width="match_parent"
            android:layout_height="40dp"
            app:stl_defaultTabTextColor="@color/tab_text_normal"
            app:stl_defaultTabTextHorizontalPadding="12dp"
            app:stl_defaultTabTextSize="16sp"
            app:stl_dividerThickness="0dp"
            app:stl_indicatorColor="@color/item_divider"
            app:stl_indicatorInterpolation="linear"
            app:stl_indicatorThickness="2dp"
            app:stl_underlineThickness="1dp"/>

<android.support.v4.view.ViewPager
            android:id="@+id/viewpager"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>
```

3.要使用SmartTabLayout需要与ViewPager同用并要进行绑定

``` stylus
private void setViewPager() {
		//获取数据
        String[] titleNameArray = getApplication().getResources().getStringArray(R.array.main_titles);
        mMainViewPagerAdapter = new MainViewPagerAdapter(getSupportFragmentManager(),titleNameArray);
        mViewPager.setAdapter(mMainViewPagerAdapter);
		//绑定Tab控件和ViewPager
        mViewPagerTab.setViewPager(mViewPager);
    }
```

4.要设定Tab的标题要在adapter里重写一个方法

``` stylus
@Override
    public CharSequence getPageTitle(int position) {

        return mTitleNameArray[position];
    }
```

5.完成
效果图如下
![enter description here][1]


  [1]: ./images/GIF.gif "GIF"