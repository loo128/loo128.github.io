---
layout: post
title: android的基站定位
description: 
category: blog
---
+ ###关于基站定位

	 一般应用于手机用户，手机基站定位服务又叫做移动位置服务（LBS——Location Based Service），它是通过电信移动运营商的网络（如GSM网）获取移动终端用户的位置信息（经纬度坐标），在电子地图平台的支持下，为用户提供相应服务的一种增值业务，例如目前中国移动动感地带提供的动感位置查询服务等。
+ ###需求调研
	
	由于之前公司项目需要用到手机定位，公司采用的百度定位，对于百度定位，大家可以去百度开放平台查看API文档，地址是：[*http://developer.baidu.com/map/geosdk.htm*](http://developer.baidu.com/map/geosdk.htm "http://developer.baidu.com/map/geosdk.htm")，在此就不多说，今天主要介绍基站定位的流程及一些注意事项，由于在APP使用的过程中，有很多客户反应百度定位失败的情况，为了解决这一问题，公司决定采用了外链定位策略--基站定位
+ ###基站定位原理
	
	首先,为什么移动和联通要疯狂建设基站呢?为什么在野外比较荒凉的地方,手机没有信号呢?那就是因为,我们每个人的手机都是靠搜索基站,跟基站互相通信赖以维生的,我们从一个地方走到另一个地方,手机获取的基站就从一个换成另一个,手机是在不断的搜索中渡过自己的一生:) ，基站定位,就是靠从用户手机上获得基站的信息,然后将基站信息上传给基站定位提供商的服务器,服务器拥有这些基站所在地的经纬度信息,返回给用户,用户就知道了自己的大概位置！

+ ###APP定位流程

	- 程序启动时／交易发生前，发起一次**百度**定位请求，如果此次定位失败，则间隔10秒重新进行**百度**定位（总共*3*次） 
	- 如**百度**定位失败，则启动**外链定位**，获取移动设备搜索的基站信息，上送前置，失败后间隔10秒重新发送1次。 
	- 两种定位方式都未成功获取定位信息，则此次定位失败。
	
基站信息的组成：
    
    public int cellId; (cellId)//基站编号  
    public int mobileCountryCode;(mcc)//国家代码   
    public int mobileNetworkCode;(mnc)//网络代码  
    public int locationAreaCode;(lac)//区域代码  

 各自的十六进制数拼成的字符串   lac+cellId+mcc+mnc 

基站信息组成发送后台接口

	request:
	{
		stations:"18ACF27101cc0000"//APP组件好的基站信息，直接转发后台
		termInfo:"btpos_123456789"//账号+手机唯一序列号
	}

部分关键代码：注意不同运营商之间获取基站信息的差异

>中国电信

	if (phoneType == TelephonyManager.PHONE_TYPE_CDMA) {
		CdmaCellLocation cdma = (CdmaCellLocation) mTelephonyManager .getCellLocation(); 
		if (cdma == null) { 
	    	FyLog.i(FyLog.TAG_APP_OTHERS, "CdmaCellLocation is null"); 
	    	return null; 
		} 
		cellId = cdma.getBaseStationId(); 
		lac = cdma.getNetworkId(); 
		mcc = operator.substring(0, 3); 
		mnc = String.valueOf(cdma.getSystemId()); 
	} 
>中国联通&中国移动 

	if(phoneType == TelephonyManager.PHONE_TYPE_GSM) {// 
		GsmCellLocation gsm = (GsmCellLocation) mTelephonyManager.getCellLocation(); 
	    if (gsm == null) { 
	        FyLog.i(FyLog.TAG_APP_OTHERS, "GsmCellLocation is null"); 
	        return null; 
	    } 
		cellId = gsm.getCid(); 
		lac = gsm.getLac(); 
		mcc = operator.substring(0, 3); 
		mnc = operator.substring(3, 5); 
	} 

