---
title: ListView 的简单应用
tags: Adapter, holder
grammar_cjkRuby: true
---


## LIstView

``` MainActivity
public class MainActivity extends Activity {

	private ListView mUsersLv;
	private UserAdapter mUserAdapter;

	@Override
	protected void onCreate(Bundle savedInstanceState) {
		super.onCreate(savedInstanceState);
		setContentView(R.layout.activity_main);
		
		//1.列表有了
		mUsersLv =(ListView) findViewById(R.id.users_lv);
		//2.数据有了
		ArrayList<User> datas=new ArrayList<User>();
		for (int i = 0; i < 30; i++) {
			datas.add(new User("张三"+i, 18+i));
		}
		//3.创建一个适配器
		mUserAdapter = new UserAdapter(datas);
		mUsersLv.setAdapter(mUserAdapter);
	}
}
```

Adapter

``` MyAdapter
public class MyAdapter extends BaseAdapter {

	private ArrayList<User> mDatas;

	public UserAdapter2( ArrayList<User> datas) {
		mDatas = datas;
	}

	// 告诉列表有多少个item
	@Override
	public int getCount() {
		return mDatas.size();// 30
	}
	
	//ViewHolder通常出现在适配器里，为的是listview滚动的时候快速设置值
	class ViewHolder{
		TextView nameTv;
		TextView ageTv;
	}

	//convertView就是缓存的View
	@Override
	public View getView(int position, View convertView, ViewGroup parent) {
		//1.创建所有子控件的集合对象---->当你找到这个对象 就相当于找到所有子控件
		ViewHolder holder=null;
		//2.如果缓存的对象为null说明是第一次创建的
		if (convertView==null) {
			//3.初始化itemView
			convertView = LayoutInflater.from(parent.getContent()).inflate(
					R.layout.user_lv_item_layout, parent, false);
			//4.把所有的子控件包起来
			holder=new ViewHolder();
			holder.nameTv = (TextView) convertView.findViewById(R.id.name_tv);
			holder.ageTv = (TextView) convertView.findViewById(R.id.age_tv);
			//5.将集合对象与convertView绑定起来(结婚了)
			convertView.setTag(holder);
		}else {
			//6.通过convertView找到绑定的集合对象
			holder=(ViewHolder) convertView.getTag();
		}
		//7.为集合对象中的每个子控件赋新的数据
		User user = mDatas.get(position);
		holder.nameTv.setText(user.getName());
		holder.ageTv.setText(user.getAge()+"");
		return convertView;
	}

	@Override
	public Object getItem(int position) {
		// TODO Auto-generated method stub
		return null;
	}

	@Override
	public long getItemId(int position) {
		// TODO Auto-generated method stub
		return 0;
	}

}
```
