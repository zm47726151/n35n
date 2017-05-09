在myeclipse中启动tomcat运行maven项目报错如下:

 

Add Deployment 

Reason: Invalid Subscription Level - Discontinuing this MyEclipse operation. 


An internal error occurred during: "Add Deployment". 

Invalid Subscription Level - Discontinuing this MyEclipse operation. 

![认证图片](http://img.blog.csdn.net/20141127135402047?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvenpxOTAwNTAz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)
奇怪的是其它非maven启动却没问题

 

一开始以为是jdk设置问题,检查后发现没问题

 

然后发现

myeclipse里面有个认证证书



 

 

结果发现真的是 myeclipse的到期问题.....

 

 

两个解决方案:

1.破解工具破解

myeclipse注册机

2.在线生成注册码破解 在线破解只能一小段时间

在线生成myeclipse注册码

原文地址：http://blog.csdn.net/zzq900503/article/details/41409441