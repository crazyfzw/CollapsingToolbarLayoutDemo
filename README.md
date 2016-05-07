# CollapsingToolbarLayoutDemo
Material Design之利用CollapsingToolbarLayout实现带Banner的toolbar的折叠效果



运行效果截图

![images](https://github.com/crazyfzw/ProjectImages/blob/master/CollapsingToolbarLayoutDemo/Coll.gif)

详细可看我博客：
[Material Design之利用CollapsingToolbarLayout轻松实现知乎日报新闻详情页顶部效果（带banner的toolbar折叠效果）](http://blog.csdn.net/fzw_faith/article/details/51336257)

布局xml
 <android.support.design.widget.CoordinatorLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <android.support.design.widget.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="256dp"
            android:fitsSystemWindows="true">

            <android.support.design.widget.CollapsingToolbarLayout
                android:id="@+id/collapsing_toolbar_layout"
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:fitsSystemWindows="true"
                app:contentScrim="@color/toolbarcolor"
                app:expandedTitleMarginStart="38dp"
                app:layout_scrollFlags="scroll|exitUntilCollapsed">

                <ImageView
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:fitsSystemWindows="true"
                    android:scaleType="centerCrop"
                    android:src="@drawable/skill"
                    app:layout_collapseMode="parallax"
                    app:layout_collapseParallaxMultiplier="0.7"/>


                <android.support.v7.widget.Toolbar
                    android:id="@+id/toolbar"
                    android:layout_width="match_parent"
                    android:layout_height="?attr/actionBarSize"
                    app:layout_collapseMode="pin"/>

            </android.support.design.widget.CollapsingToolbarLayout>

        </android.support.design.widget.AppBarLayout>

        <android.support.v4.widget.NestedScrollView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:scrollbars="vertical"
            app:layout_behavior="@string/appbar_scrolling_view_behavior">

            <WebView
                android:id="@+id/webview"
                android:layout_width="match_parent"
                android:layout_height="match_parent"></WebView>
        </android.support.v4.widget.NestedScrollView>

    </android.support.design.widget.CoordinatorLayout>

Java代码


        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);
        toolbar.setNavigationOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                onBackPressed();
            }
        });

        //使用CollapsingToolbarLayout必须把title设置到CollapsingToolbarLayout上，设置到Toolbar上则不会显示
        CollapsingToolbarLayout mCollapsingToolbarLayout = (CollapsingToolbarLayout) findViewById(R.id.collapsing_toolbar_layout);
        mCollapsingToolbarLayout.setTitle("Bar Brother 徒手健身");
        //通过CollapsingToolbarLayout修改字体颜色
        mCollapsingToolbarLayout.setExpandedTitleColor(Color.WHITE);//设置还没收缩时状态下字体颜色
        mCollapsingToolbarLayout.setCollapsedTitleTextColor(Color.WHITE);//设置收缩后Toolbar上字体的颜色
        //toolbar navigationicon 改变返回按钮颜色
        final Drawable upArrow = getResources().getDrawable(R.drawable.abc_ic_ab_back_mtrl_am_alpha);
        upArrow.setColorFilter(getResources().getColor(R.color.white), PorterDuff.Mode.SRC_ATOP);
        getSupportActionBar().setHomeAsUpIndicator(upArrow);
