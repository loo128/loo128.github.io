---
layout: post
title: ichartjs在android应用中的使用
description: 
category: blog
---

 ichartjs 是一款基于HTML5的图形库。使用纯javascript语言, 利用HTML5的canvas标签绘制各式图形。 ichartjs致力于为您的应用提供简单、直观、可交互的体验级图表组件。是WEB/APP图表展示方面的解决方案 。如果你正在开发HTML5的应用，ichartjs正好适合您。 ichartjs目前支持饼图、环形图、折线图、面积图、柱形图、条形图。ichartjs是基于Apache License 2.0协议的开源项目。

此文以制作一个3D的柱形图为例讲解ichartjs的使用

首先,我们要去ichartjs官网下载其js库，因为我们的要用到东西就是在html文件中导入一个js文件即可

ichartjs官网地址：[*http://www.ichartjs.com/*](http://www.ichartjs.com/)

源代码地址：[*http://code.google.com/p/ichartjs/source/checkout*](http://code.google.com/p/ichartjs/source/checkout)

将ichart.1.2.min.js放置assets文件中，新建一个html文件，也放置在assets文件下，代码如下：

	<!DOCTYPE html> 
	<html> 
	<head> 
	<meta charset="UTF-8" /> 
	<title>ichartjs 示例</title> 
	<script type="text/javascript" src="ichart.1.2.min.js"></script> 
	<script type="text/javascript"> 
	$(function(){
		var data = [
					{name : 'IE',value : 35.75,color:'#bc6666'},
					{name : 'Chrome',value : 29.84,color:'#cbab4f'},
					{name : 'Firefox',value : 24.88,color:'#76a871'},
					{name : 'Safari',value : 6.77,color:'#9f7961'},
					{name : 'Opera',value : 2.02,color:'#2ba5a4'},
					{name : 'Other',value : 0.73,color:'#6f83a5'}
				];
		
		new iChart.Column3D({
			render : 'canvasDiv',
			data: data,
			title : 'Top 5 Browsers from 1 to 29 Feb 2012',
			width : 800,
			height : 400,
			align:'left',
			offsetx:50,
			legend : {
				enable : true
			},
			sub_option:{
				label:{
					color:'#111111'
				}
			},
			coordinate:{
				width:600,
				scale:[{
					 position:'left',	
					 start_scale:0,
					 end_scale:40,
					 scale_space:8,
					 listeners:{
						parseText:function(t,x,y){
							return {text:t+"%"}
						}
					}
				}]
			}
		}).draw();
	});
	</script> 

以上画图部分的属性大家可以参照源代码中docs文件夹中的 API文档  所有的属性都有说明，可以根据自己需求定制不同的效果，在此不做详细说明,最后，在Activity中

	package com.example.ichartjsdemo; 

	import android.annotation.SuppressLint; 
	import android.app.Activity; 
	import android.os.Bundle; 
	import android.view.Menu; 
	import android.webkit.WebView; 
	public class MainActivity extends Activity { 
		private WebView webView; 
		@SuppressLint({ "JavascriptInterface", "SetJavaScriptEnabled" }) 
		@Override 
		protected void onCreate(Bundle savedInstanceState) { 
			super.onCreate(savedInstanceState); 
			setContentView(R.layout.activity_main); 
			webView = (WebView) findViewById(R.id.webview); 
			webView.getSettings().setJavaScriptEnabled(true); // 设定该WebView可以执行JavaScript程序 
			webView.getSettings().setBuiltInZoomControls(true); // 设定该WebView可以缩放 
			webView.loadUrl("file:///android_asset/line.html"); 
		} 
		
		@Override 
		public boolean onCreateOptionsMenu(Menu menu) { 
			getMenuInflater().inflate(R.menu.main, menu); 
			return false; 
		} 
	} 

运行效果图：

![ichartjs_in_android.png](http://loo128.github.io/images/ichartjs_in_android.png) 