---
title: jni的基本使用 
tags: c,jni
grammar_cjkRuby: true
---

# 概述
## 1. 什么是JNI
- JNI java native interface native本地  java本地接口
- 通过JNI可以实现java和本地代码之间相互调用
- jni可以看做是翻译 实际上就是一套协议


## 2. 为什么要用JNI
1. 市场需求
2. 让java代码和底层代码之间互相调用
- java调用底层特殊硬件(调用c语言,车载电脑)
- 效率上c/c++语言效率更高(时间和内存要求严格的场景)
- 复用已经存在的c代码, c语言发展了几十年有很多优秀的代码库(ffmpeg,opencv,7zip)
- java反编译非常容易.c语言反编译不容易.关键业务逻辑需要用c实现.
- 历史遗留问题,复用原来pc端的c代码

# jni的简单使用
工具:eclipse,NDK
1.首先在eclipse中新建一个项目
![enter description here][1]

2.在MainActivity中用native声明一个方法,用native关键字说明其修饰的方法是一个原生态方法,方法对应的实现不是在当前文件,而是在用其他语言（如C和C++）实现的文件中.

``` stylus
public class MainActivity extends Activity {

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
	}

	public native void callC();

}
```

3.在工程目录下创建一个jni文件夹,并创建一个c文件,并在c文件中写c代码    
![enter description here][2]

``` stylus
#include <jni.h>
#include<stdio.h>
#include<stdlib.h>

JNIEXPORT jstring JNICALL Java_com_example_hellofromc_MainActivity_callC
(JNIEnv * env, jobject obj) {
	char* arr = "hello fromC!!!";

	return (*env)->NewStringUTF(env, arr);
}
```
4.配置c代码编译的脚本文件 Android.mk文件
在jni文件夹里新建一个Android.mk文件,写上代码

``` stylus
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)

LOCAL_MODULE    := callC
LOCAL_SRC_FILES := callC.c

include $(BUILD_SHARED_LIBRARY)

```
5.在java代码里面写静态代码块

``` stylus
public class MainActivity extends Activity {

	==static{
		System.loadLibrary("callC");
	}==
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
	}

	public native void callC();

}
```
6.像使用一般java方法一样调用native的方法.

``` stylus
public class MainActivity extends Activity {

	static{
		System.loadLibrary("callC");
	}
	
	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		//这里就打印一个吐司进行测试 
		Toast.makeText(this, callC(),0).show();
	}

	public native String callC();

}
```

7.完成
![enter description here][3]


  [1]: ./images/jniimg1.jpg "jniimg1"
  [2]: ./images/jniimg2.jpg "jniimg2"
  [3]: ./images/jniimg3.gif "jniimg3"