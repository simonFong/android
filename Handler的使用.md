---
title: Handler的使用
tags: handler
grammar_cjkRuby: true
---


返回主线程

``` 必须手打,没有提示
private Handler mHandler = new Handler(){
        @Override
        public void handleMessage(Message msg) {
            
        }
    };
	
	//传递参数what,obj
	mHandler.obtainMessage(action,result).sendToTarget();
```
