---
layout:    post
title:     开发微信小程序踩过的坑
date:      2020-02-15 17:18:18
summary:  自动化程序
categories: Program
tags: Weixin
excerpt: 本文记录开发微信小程序遇到的坑，包括JS异步函数的回调，icopath 错误。
mathjax: true
---

## 微信小程序开发踩过的坑

### Javascript编程

`wx.request`为异步函数，使用起来总是很不方便，调用结束后总是返回`undefine`。
请看如下代码：

    onload: function () {
        wx.request({
          url:'http://118.24.159.109/',
          header:{
            'content-type': 'application/json'
          },
          success: function(res){
              var price1 = JSON.parse(res.data.price);
              for (var k = 0; k<markersData.length;k++){
                markersData[k].value = price1;          //高德返回的数据中加入value属性 
              }
              console.log(price1);
          }
        })
        console.log(markersData[0].value)    //返回undefine值
        that.showMarkerInfo(markersData,0);
    })

* 注：完整代码请查看GitHub。
我们得到的结果这样的。

![返回undfine](/Images/2020/weixin-app-1.png)

`wx.request`是异步请求，JS不会等待`wx.request`执行完毕再往下执行，所以JS按顺序会先执行`that.showMarkerInfo()`，等服务器返回数据以后，`that.showMarkerInfo()`早就执行完了，也就返回不了数据了。

####解决办法：
    
就是把需要使用异步数据的函数写在回调里

    onload: function () {
        wx.request({
          url:'http://118.24.159.109/',
          header:{
            'content-type': 'application/json'
          },
          success: function(res){
              var price1 = JSON.parse(res.data.price);
              for (var k = 0; k<markersData.length;k++){
                markersData[k].value = price1;          //高德返回的数据中加入value属性 
              }
                console.log(price1);
                console.log(markersData[0].value)    //返回正常值
                that.showMarkerInfo(markersData,0);
          }
        })

    })
如图：

![正常值](/Images/2020/weixin-app-正常值.png)


### 缺少文件, error: iconPath=xx, file not found

开发工具运行正常，上传代码时显示`缺少文件, error: iconPath=xx, file not found`

![正常值](/Images/2020/icopath.png)

除了使用绝对路径，你还需要检查tabBar中的路径是否完整，"iconPath"为空的也会显示错误。

    tabBar": {
    "list": [
      {
        "pagePath": "pages/index/index",
        "text": "加油",
        "iconPath": "/images/weather1.png",  
        "selectedIconPath": "/images/weather2.png"
      },










