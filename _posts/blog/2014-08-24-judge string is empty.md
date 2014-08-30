---
layout: post
title:  android 判断字符串是否为空的最优方法
description: 
category: blog
---
 在android 的开发中经常会使用判断字符串是否为空，虽然现在智能手机的运行速度越来越高，但为了使应用更加的流畅，我们应该保证在编写程序时使用较好的方法来提高效率。以下为五种方法的运行时间的比较：

	private void function1() { 
	    long startTime = System.currentTimeMillis(); 
	    for (long i = 0; i < n; i++) { 
	        if (s == null || s.equals("")) 
	        ; 
	    } 
	    long endTime = System.currentTimeMillis(); 
	    Log.i("DEBUG", "function 1 use time: " + (endTime - startTime) + "ms"); 
	} 

	private void function2() { 
	   	long startTime = System.currentTimeMillis(); 
	   	for (long i = 0; i < n; i++) { 
	        if (s == null || s.length() <= 0) 
	        ; 
	    } 
    	long endTime = System.currentTimeMillis(); 
   	 	Log.i("DEBUG", "function 2 use time: " + (endTime - startTime) + "ms"); 
	} 

	private void function3() { 
	    long startTime = System.currentTimeMillis(); 
	    for (long i = 0; i < n; i++) { 
	        if (s == null ||s.isEmpty()) 
	        ; 
	    } 
	    long endTime = System.currentTimeMillis(); 
	    Log.i("DEBUG", "function 3 use time: " + (endTime - startTime) + "ms"); 
	} 

	private void function4() { 
	    long startTime = System.currentTimeMillis(); 
	    for (long i = 0; i < n; i++) { 
	        if (s == null || s == "") 
	        ; 
	    } 
	    long endTime = System.currentTimeMillis(); 
	    Log.i("DEBUG", "function 4 use time: " + (endTime - startTime) + "ms"); 
	} 

	private void function5() { 
	    long startTime = System.currentTimeMillis(); 
	    for (long i = 0; i < n; i++) { 
	    if (TextUtils.isEmpty(s)) 
	        ; 
	    } 
	    long endTime = System.currentTimeMillis(); 
	    Log.i("DEBUG", "function 5 use time: " + (endTime - startTime) + "ms"); 
	}

+ **方法一: 最多人使用的一个方法, 直观, 方便, 但效率很低.**

+ **方法二: 比较字符串长度, 效率高, 是我知道的最好一个方法.**

+ **方法三: android API 9 才开始提供的办法, 效率和方法二基本上相等, 但出于兼容性考虑, 推荐使			用方法二或方法四.**

+ **方法四: 这是种最直观,简便的方法,而且效率也非常的高,与方法二、三的效率差不多**

+ **方法五: Android为我们提供了一个简单实用的TextUtils类**


以下代码在我机器上的运行结果: (机器性能不一, 仅供参考)

	08-24 21:36:20.324: I/DEBUG(4302): function 1 use time: 2245ms
    08-24 21:36:21.074: I/DEBUG(4302): function 2 use time: 749ms
    08-24 21:36:21.415: I/DEBUG(4302): function 3 use time: 343ms
    08-24 21:36:21.795: I/DEBUG(4302): function 4 use time: 381ms 
    08-24 21:36:22.836: I/DEBUG(4302): function 5 use time: 1042ms

注意:s == null 是有必要存在的.
如果 String 类型为 null, 而去进行 equals(String) 或 length() 等操作会抛出java.lang.NullPointerException.
并且s==null 的顺序必须出现在前面.不然同样会抛出java.lang.NullPointerException.
如下代码:

	String str=  null;
	if("".equales(str) || str== null){//会抛出异常
		System.out.println("success");
	}// "".equales(str);后置确保不会遇null报错。