# Android-Improve-Skills

## 高级UI

### 1、Recyclerview

- 配置Gradle

```
compile ‘com.android.support:recyclerview-v7:23.2.1’
```

#### 1.1 MateriaDesign控制全局样式

```
<!--
      Base application theme, dependent on API level. This theme is replaced
      by AppBaseTheme from res/values-vXX/styles.xml on newer devices.
  -->
  <style name="AppBaseTheme" parent="Theme.AppCompat.Light">
      <!--
          Theme customizations available in newer API levels can go in
          res/values-vXX/styles.xml, while customizations related to
          backward-compatibility can go here.
      -->
  </style>

  <!-- Application theme. -->
  <style name="AppTheme" parent="AppBaseTheme">
      <!-- All customizations that are NOT specific to a particular API-level can go here. -->
      <item name="android:textColor">@color/mytextcolor</item>
      <item name="colorPrimary">@color/colorPrimary_pink</item>
      <item name="colorPrimaryDark">@color/colorPrimary_pinkDark</item>
      <item name="android:windowBackground">@color/background</item>
<item name="colorAccent">@color/accent_material_dark</item>
 <!-- 设置虚拟导航栏背景颜色 -->
      <item name="android:navigationBarColor">@color/colorPrimary_pink</item>

  </style>

```

|类型|作用|
|:---|:---|
|colorPrimary|主色|
|colorPrimaryDark|主色--深色，一般可以用于状态栏颜色、底部导航栏|
|colorAccent|（代表各个控件的基调颜色--CheckBox、RadioButton、ProgressBar等等）|
|android:textColor|当前所有的文本颜色|

运用场景：Dialog在不同版本展示的效果不一样，统一改用v7里边的Dialog

- 兼容性开发

  - 沉浸式（QQ）

#### 1.2 MaterialDesign兼容性控件的使用

在appcompat-V7里面有很多为兼容而生的控件，这样就可以做到高低版本和不同的ROM之间体验一致！还可以配合appcompat的主题使用达到体验一致性

- android.support.v7.app.AlertDialog

- 进度条样式设置

```
style="@style/Widget.AppCompat.ProgressBar.Horizontal"
```

- SwipeRefreshLayout下拉刷新

- PopupWindow、ListPopupWindow、PopupMenu

- android.support.v7.widget.LinearLayoutCompat

给包裹在里面的所有子控件添加间隔线

```
<android.support.v7.widget.LinearLayoutCompat
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            app:divider="@drawable/abc_list_divider_mtrl_alpha"
            app:showDividers="beginning|middle"
            android:orientation="vertical" >
```

#### 1.3 V7 RecyclerView

特点：

- 谷歌在高级版本提出一个新的替代ListView、GridView的控件。

- 高度解耦。

- 自带了性能优化。ViewHolder。

- 低耦合高内聚

使用RecycleView的时候要先设置显示的方向

```
list = new ArrayList<String>();
for (int i = 0; i < 60; i++) {
  list.add("item"+i);
}

recylerview = (RecyclerView)findViewById(R.id.recylerview);
//		adapter = new MyRecyclerAdapter(list);
adapter = new MyStaggedRecyclerAdapter(list);
//LayoutManager布局摆放管理器(线性摆放、瀑布流)
//		recylerview.setLayoutManager(new LinearLayoutManager(this));//默认垂直
//reverseLayout:数据倒置，从右边开始滑动
//		recylerview.setLayoutManager(new LinearLayoutManager(this, LinearLayoutManager.HORIZONTAL, true));
//		recylerview.setLayoutManager(new GridLayoutManager(this, 3));
//瀑布流效果
recylerview.setLayoutManager(new StaggeredGridLayoutManager(3, LinearLayoutManager.VERTICAL));
recylerview.setAdapter(adapter);
```

**个人开发使用出现的问题：**

今天把项目中的ListView换成最近比较流行的RecycleView发现，之前好好的item，改用了RecycleView之后就变得参差不齐了，解决方法

stackoverflow给的答案是：

如果之前使用的是 view.inflate，要换成LayoutInflater

在onCreateViewHolder方法中把

View view = View.inflate(mContext, R.layout.xlistview_course_item, null)

换成

View view = mInflater.from(mContext).inflate(R.layout.xlistview_course_item, parent, false)即可。

#### 2、MaterialDesign_LayoutInflater源码分析

TODO：

#### 3、RecyclerView设置分割线

- RecyclerView没有默认的分割线，需要自己绘制。
    - RecyclerView.ItemDecoration

       线性的分割线

	     网格的分割线

-
