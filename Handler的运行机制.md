---
title: Handler的运行机制 
tags: Handler,Looper,MessageQueue
grammar_cjkRuby: true
---


Handler的作用
我们在进行耗时操作后,需要进行UI修改操作时,因为修改UI不能再子线程里进行,所以必须返回主线程里,这时我们就可以使用Handler来进行线程与线程的转换和通信.

Handler的运行机制
![enter description here][1]


  [1]: ./images/%E6%95%B0%E6%8D%AE%E6%B5%81%E5%9B%BE.png "数据流图"
  
 1.Looper.prepare(),这个方法是查找当前线程有没有Looper对象,如果有,则会抛出异常,因为一个线程只能存在一个Looper,如果没有,就会在当前线程创建一个looper.当looper被创建后,调用looper.loop,就会对MessageQueue不断地进行读取,如果MessageQueue接收到Message,looper读取到了Message后会让对应的Handler进行处理,会调用dispatchMessage,最终调用handlerMessage.

 2.判断Handler是否能处理UI操作,决定于Handler绑定的Looper是否在主线程里

3.activity创建的时候系统会调用一个ActivityThread的方法,这个方法会调用Looper.prepare和looper.loop方法,所以在主线程中不用Looper都可以使用Handler,而不需要再调用Looper.prepare和looper.loop

4.如果在子线程里使用Handler,必须要先判断当前线程是否存在Looper,如果不存在就必须创建一个,或者绑定一个存在的Looper才能使用Handler