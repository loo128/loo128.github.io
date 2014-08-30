---
layout: post
title: 关于魅族SmartBar的适配2
description: 顶栏与底栏同时存在及自定义底栏背景
category: blog
---

##顶栏与底栏同时存在
我们在做适配的过程中，未免会遇到这样的一个需求，需要Actionbar和Smartbar底栏同时存在，那我们改怎么处理呢？其实很简单，分为两步

#######1、自定义ActionBar布局

    mCustomView = LayoutInflater.from(this).inflate(R.layout.activity_main_actionbar, null);
	actionBar.setDisplayOptions(ActionBar.DISPLAY_SHOW_CUSTOM);
	actionBar.setCustomView(mCustomView);

#######2、拆分ActionBar
只需在AndroidManifest的<activity>或者<application>加上uiOptions="splitActionBarWhenNarrow"，例如：

    <activity
	    android:name=".ActionBarSplit"
	    android:label="@string/action_bar_split"
	    android:uiOptions="splitActionBarWhenNarrow" >
    </activity>

##自定义底栏背景
大家第一想到的肯定是改变Actionbar样式不就好了，就像这样：

     <style name="CustomActionBar" parent="@android:style/Widget.DeviceDefault.Light.ActionBar">
        <item name="android:background">@drawable/action_bar_bg</item>
        <item name="android:backgroundSplit">@drawable/action_bar_bg</item>
     </style>
答案是否定的，因为这样做的话，你的顶部栏和底部栏都会变成你上面background的样式了，如果我们想要不改变顶部栏的颜色同时，还想要自定义底部栏，我们该怎么办呐？郁闷，找了好久，才发现Actionbar的底部栏的默认背景颜色是通过android:windowBackground属性来配置的，所以我们只需要给需要改变底栏背景的Acticity配置这个属性样式即可：

###### App Base Theme

    <style name="AppTheme" parent="android:Theme.Holo.Light">
        <item name="android:windowContentOverlay">@null</item>
        <item name="android:windowBackground">@color/window_background</item>
        <item name="android:homeAsUpIndicator">@drawable/ic_action_back</item>
        <item name="android:actionBarStyle">@style/ActionBar</item>
        <item name="android:windowAnimationStyle">@style/HoloThemeActivityAnimation</item>
        <item name="android:actionOverflowButtonStyle">@style/ActionbarOverFlowStyle</item>
        <item name="android:actionMenuTextAppearance">@style/ActionBar.TitleText</item>
        <item name="android:actionMenuTextColor">@color/white</item>
        <item name="android:windowIsTranslucent">true</item>
    </style>

######适配smartbar黑色背景主题

    <style name="CustomTheme" parent="@style/AppTheme">
        <item name="android:windowBackground">@color/black</item>
    </style>

######Activity样式
     <activity
            android:name=".ui.MainActivity"
            android:launchMode="singleTask"
            android:screenOrientation="portrait"
            android:theme="@style/CustomTheme"
            android:uiOptions="splitActionBarWhenNarrow" />
     <activity

[loo28]:    http://loo128.github.io  "loo128"
