---
title:  自定义Toast并移动
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


根据系统定义吐司的原理,自定义吐司,并实现能移动的功能,自定义吐司暂时没有掌握,先总结下移动的原理

``` stylus
public class WindowsViewService extends Service {

    private WindowManager mWn;
    private View mView;
    private WindowManager.LayoutParams mParams;

    @Nullable
    @Override
    public IBinder onBind(Intent intent) {
        return null;
    }

    @Override
    public void onCreate() {
        //获取窗口管理器
        mWn = (WindowManager) getSystemService(Context.WINDOW_SERVICE);
        //LayoutParams相当于一个Layout的信息包，它封装的是Layout的位置、高、宽等信息。
        mParams = new WindowManager.LayoutParams();
        mParams.height = WindowManager.LayoutParams.WRAP_CONTENT;
        mParams.width = WindowManager.LayoutParams.WRAP_CONTENT;
        //flag表示触摸属性等,FLAG_NOT_TOUCH_MODAL即使这个window是可获取焦点的,也允许window之外点击事件传递给其他在其之后的window
        mParams.flags = WindowManager.LayoutParams.FLAG_NOT_TOUCH_MODAL;
        //设置半透明,format表示显示属性,格式等
        mParams.format = PixelFormat.TRANSLUCENT;
        //type表示窗口的级别,TYPE_TOAST级别最低,不能移动
        mParams.type = WindowManager.LayoutParams.TYPE_PHONE;
        mView = View.inflate(getApplicationContext(), R.layout.toastlayout, null);
        //给布局一个触摸的监听器
        mView.setOnTouchListener(new View.OnTouchListener() {
            private float mStartRawY;
            private float mStartRawX;

            @Override
            public boolean onTouch(View v, MotionEvent event) {

                switch (event.getAction()) {
                    case MotionEvent.ACTION_DOWN:
                        //获取点击时手指位置的x,y
                        mStartRawX = event.getRawX();
                        mStartRawY = event.getRawY();
                        break;
                    case MotionEvent.ACTION_MOVE:
                        //移动时手指位置的x,y
                        float rawX1 = event.getRawX();
                        float rawY1 = event.getRawY();
                        //偏差量
                        int dx = (int) (rawX1 - mStartRawX);
                        int dy = (int) (rawY1 - mStartRawY);
                        //只能在Activity起作用
                        //tx.layout(tx.getLeft()+dx,tx.getTop()+dy,tx.getRight()+dx,mView.getBottom()+dy);
                        mParams.x += dx;
                        mParams.y += dy;
                        //更新窗口布局的位置
                        mWn.updateViewLayout(mView, mParams);
                        //重新赋值开始位置坐标,
                        mStartRawX = event.getRawX();
                        mStartRawY = event.getRawY();
                        break;
                    case MotionEvent.ACTION_UP:
                        //提起

                        break;
                }
                return true;
            }
        });


        mWn.addView(mView, mParams);
    }
```
