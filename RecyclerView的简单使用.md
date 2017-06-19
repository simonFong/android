---
title: RecyclerView的简单使用 
tags: Manager,Adapter,Decoration
grammar_cjkRuby: true
---

# 前言
今天研究了一下RecyclerView,发现这真的非常强大,不仅可以完全取缔ListView和GridView,还可以有很多其他的效果,可以非常炫酷,今天先来记录下最简单的使用.

RecyclerView是自Android 5.0之后才发布的,要使用它要先根据自己sdk的版本进行导包:

``` stylus
compile 'com.android.support:recyclerview-v7:25.3.1'
```

导包完成后就可以开始使用了.

# 1.控件使用
RecyclerView是一个控件,它的使用方法跟ListView的用法差不多,直接在布局中使用.

``` stylus
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/activity_main2"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="#5555"
    tools:context="com.simon.demo.my.Main2Activity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <Button
            android:id="@+id/add_btn"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="添加item"/>

        <Button
            android:id="@+id/delete_btn"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="删除item"/>
    </LinearLayout>

    <android.support.v7.widget.RecyclerView
        android:id="@+id/recycler_view"
        android:paddingLeft="3dp"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</LinearLayout>
```

# 2.Adapter和LayoutManager
在使用RecyclerView时候，必须指定一个适配器Adapter和一个布局管理器LayoutManager。适配器继承RecyclerView.Adapter类，具体实现类似ListView的适配器，取决于数据信息以及展示的UI。布局管理器用于确定RecyclerView中Item的展示方式以及决定何时复用已经不可见的Item，避免重复创建以及执行高成本的findViewById()方法。

## ①LayoutManager布局管理器
RecyclerView提供了三种布局管理器：

 - LinerLayoutManager 以垂直或者水平列表方式展示Item
 - GridLayoutManager 以网格方式展示Item
 - StaggeredGridLayoutManager 以瀑布流方式展示Item

``` stylus
//这里使用了线性垂直列表
mLinearLayoutManager = new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false);
mRecyclerView.setLayoutManager(mLinearLayoutManager);
```

## ②Adapter适配器
创建一个类继承RecyclerView.Adapter
``` stylus
public class RecycleAdapter extends RecyclerView.Adapter<RecycleAdapter.ViewHolder>{

    private final Context context;
    private final ArrayList<String> mData;

    public RecycleAdapter(Context c, ArrayList<String> data){
        this.context = c;
        this.mData = data;
    }

    //获取item布局,并创建ViewHolder与之绑定
    @Override
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
	    //这里填充的布局root写parent的话,会只显示一个item,改为null后才正常显示
        //解决http://blog.csdn.net/fantasiasango/article/details/52188064
        //如果用View.inflate填充的布局没有调用到设置的属性
//        View view = View.inflate(parent.getContext(), R.layout.view_rv_item, null);
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.view_rv_item, parent, false);
        ViewHolder viewHolder = new ViewHolder(view);
        return viewHolder;
    }

    //
    @Override
    public void onBindViewHolder(ViewHolder holder, int position) {
        holder.mTx.setText(mData.get(position));
    }

    @Override
    public int getItemCount() {
        return mData.size();
    }

    public static class ViewHolder extends RecyclerView.ViewHolder{
 //有写情况下需要手动设置属性,不然布局会显示不正常
        RelativeLayout.LayoutParams layoutParams = new RelativeLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.WRAP_CONTENT);
        itemView.setLayoutParams(layoutParams);
        private final TextView mTx;

        public ViewHolder(View itemView) {
            super(itemView);
            mTx = (TextView) itemView.findViewById(R.id.item_tv);
        }
    }
}
```
Activity中使用代码

``` stylus
 mRecycleAdapter = new RecycleAdapter(this,getData());
 mRecyclerView.setAdapter(mRecycleAdapter);
 
 //模拟数据
    private ArrayList<String> getData() {
        ArrayList<String> strings = new ArrayList<>();
        for(int i = 0; i < 50; i++) {
            strings.add("我是超人"+i);
        }
        return strings;
    }
```

## ③Decoration修饰器
这是用来自定义RecycleView的样式,decoration的样式可以同时使用多个,不同的decoration效果会重叠起来,从而达到不同的效果.

主要使用的三个方法:

``` stylus
public void onDraw(Canvas c, RecyclerView parent, State state)
public void onDrawOver(Canvas c, RecyclerView parent, State state)
public void getItemOffsets(Rect outRect, View view, RecyclerView parent, State state)
```
举例使用:

``` stylus
public class MyItemDecoration extends RecyclerView.ItemDecoration {

    private final Paint mPaint;
    private final int mDividerHeight;

    public MyItemDecoration(Context context) {
        mPaint = new Paint();
        mPaint.setColor(Color.BLUE);
        mDividerHeight = 10;
    }

    //    这两个方法都是用于绘制间隔样式
    @Override
    public void onDraw(Canvas c, RecyclerView parent, RecyclerView.State state) {
        super.onDraw(c, parent, state);
    }

    @Override
    public void onDrawOver(Canvas c, RecyclerView parent, RecyclerView.State state) {
        super.onDrawOver(c, parent, state);
        int childCount = parent.getChildCount();
        int left = parent.getPaddingLeft();
        int right = parent.getWidth() - parent.getPaddingRight();

        for (int i = 0; i < childCount - 1; i++) {
            View view = parent.getChildAt(i);
            int top = view.getBottom();
            int bottom = view.getBottom() + 5;
            Log.v("cherish233", "left:" + left + "---" + "top:" + top + "---" + "right:" + right + "---" + "bottom:" + bottom + "---");
            c.drawRect(left, top, right, bottom, mPaint);
        }
        //        View view = parent.getChildAt(0);
        //        int top = view.getBottom();
        //        int bottom = view.getBottom() + mDividerHeight;
        //        Log.v("cherish233", "left:" + left + "---" + "top:" + top + "---" + "right:" + right + "---" + "bottom:" + bottom + "---");
        //        c.drawRect(left, top, right, bottom, mPaint);


    }

    //设置item的偏移量，偏移的部分用于填充间隔样式
    @Override
    public void getItemOffsets(Rect outRect, View view, RecyclerView parent, RecyclerView.State state) {
        super.getItemOffsets(outRect, view, parent, state);
        outRect.bottom = mDividerHeight;

    }

}
```

在Activity中的使用代码

``` stylus
mMyItemDecoration = new MyItemDecoration(this);
mRecyclerView.addItemDecoration(mMyItemDecoration);
```


完整的Activity代码:

``` stylus
public class Main2Activity extends AppCompatActivity implements View.OnClickListener {

    private Button mAddBtn;
    private Button mDeleteBtn;
    private RecyclerView mRecyclerView;
    private LinearLayout mActivityMain2;
    private LinearLayoutManager mLinearLayoutManager;
    private RecycleAdapter mRecycleAdapter;
    private MyItemDecoration mMyItemDecoration;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);
        initView();
        initData();
    }

    private void initData() {
        mLinearLayoutManager = new LinearLayoutManager(this, LinearLayoutManager.VERTICAL, false);
        mRecycleAdapter = new RecycleAdapter(this,getData());
        mMyItemDecoration = new MyItemDecoration(this);

        mRecyclerView.setLayoutManager(mLinearLayoutManager);
        mRecyclerView.setAdapter(mRecycleAdapter);
        mRecyclerView.addItemDecoration(mMyItemDecoration);
    }

    //模拟数据
    private ArrayList<String> getData() {
        ArrayList<String> strings = new ArrayList<>();
        for(int i = 0; i < 50; i++) {
            strings.add("我是超人"+i);
        }
        return strings;
    }

    private void initView() {

        mAddBtn = (Button) findViewById(R.id.add_btn);
        mAddBtn.setOnClickListener(this);
        mDeleteBtn = (Button) findViewById(R.id.delete_btn);
        mDeleteBtn.setOnClickListener(this);
        mRecyclerView = (RecyclerView) findViewById(R.id.recycler_view);
    }

    @Override
    public void onClick(View v) {
        switch (v.getId()) {
            case R.id.add_btn:

                break;
            case R.id.delete_btn:

                break;
        }
    }
}
```


最终效果:    
![enter description here][1]


  [1]: ./images/GIF5.gif "GIF5"