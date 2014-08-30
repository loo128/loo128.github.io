---
layout: post
title: 解决ScrollView嵌套ListView的冲突问题
description: 
category: blog
---
最近项目中遇到了一个界面，里面涉及ScrollView嵌套ListView的问题，按照正常思路，在有ListView布局的外层套一个ScrollView,发现ListView显示不全，只显示部分的Item,经过研究，有以下3种解决方案

1. #####手动设置ListView高度

    经过测试发现，在xml中直接指定ListView的高度，是可以解决这个问题的，但是ListView中的数据是可变的，实际高度还需要实际测量。于是需要手动代码设置ListView高度，实现代码如下：
	
	>取代ListView的LinearLayout，使之能够成功嵌套在ScrollView中
	
		public class LinearLayoutForListView extends LinearLayout {
			private BaseAdapter adapter;
			private OnClickListener onClickListener = null;
			public void bindLinearLayout() {
			int count = adapter.getCount();
			this.removeAllViews();
			for (int i = 0; i < count; i++) {
				View v = adapter.getView(i, null, null);
	            v.setOnClickListener(this.onClickListener);
	            addView(v, i);
	        }
       		Log.v("countTAG", "" + count);
    	}
		public LinearLayoutForListView(Context context) {
			super(context);  
采用这个方法有个细节需要注意：就是getView方法返回的View必须由LinearLayout组成，而且LinearLayout里面也不能有其他的如LinearLayout，RelativeLayout等的子布局，只能存在一个外围的LinearLayout布局，最近做的项目就是遇到这个问题，所以在ListView中遇到比较复杂的布局的时候就要考虑其他方案了，比如下面介绍的两种方法

2. 采用LinearLayout取代ListView
 
    如果ListView 中Item的数量不是很大，完全没必要用ListView,用LinearLayout代替即可，也不会出现上述冲突问题

3. 自定义可适应ScrollView的ListView

	这种方法比较省事，而且改动也很小，只需要自定义一个类继承自ListView，然后重写里面的onMeasure方法，代码如下：

     > 重写该方法，达到使ListView适应ScrollView的效果
     
	    @Override
	    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) 
	        int expandSpec = MeasureSpec.makeMeasureSpec(Integer.MAX_VALUE >> 2,
	        MeasureSpec.AT_MOST);
	        super.onMeasure(widthMeasureSpec, expandSpec);
	    }
