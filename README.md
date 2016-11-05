# WeiXinDemo
微信官方demo 

基础
  1、基础关键内容 app.js app.json app.wxss 
  2 .js脚本文件     .json配置文件   .wxss样式表文件（css文件） .wxml网页文件（html文件）
  
  app.js----可在此文件中   1、监听并处理小程序的生命周期函数， 2、声明全局变量。（例：调用API）
  
  app.json----对整个小程序进行*全局配置*  （例：1、有哪些页面组成 2、窗口颜色 3、导航条样式 4、默认标题） （注：不可有任何注释）
  
  app.wxss----公共样式表
  
  3、为了方便开发者减少配置项，微信规定 **描述页面的*四个文件*（.js .json .wxss .wxml）和*文件夹* 同名！**
  
  
  app.json配置项列表
  
    pages 设置页面路径 （必填  类型：String Array）
    
    window  设置默认页面的窗口表现  （非必填 类型：Object）
    
    tabBar 设置底部 tab 的表现     （非必填 类型：Object）
    
    networkTimeout 设置网络超时时间 （非必填 类型：Object）
    
    debug 设置是否开启 debug 模式   （非必填 类型：Boolean）
  例
  {
    "pages": [
      "pages/index/index",
      "pages/logs/index"
    ],
    "window": {
      "navigationBarTitleText": "Demo"
    },
    "tabBar": {
      "list": [{
        "pagePath": "pages/index/index",
        "text": "首页"
      }, {
        "pagePath": "pages/logs/logs",
        "text": "日志"
      }]
    },
    "networkTimeout": {
      "request": 10000,
      "downloadFile": 10000
    },
    "debug": true
  }