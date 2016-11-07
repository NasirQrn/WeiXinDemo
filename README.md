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
            color	        HexColor	是		        tab 上的文字默认颜色
            selectedColor	HexColor	是		        tab 上的文字选中时的颜色
            backgroundColor	HexColor	是		        tab 的背景色
            borderStyle	    String	    否	    black	tabbar上边框的颜色， 仅支持 black/white
            list	        Array	    是		        tab 的列表，详见 list 属性说明，最少2个、最多5个 tab
                pagePath	        String	是	页面路径，必须在 pages 中先定义
                text	            String	是	tab 上按钮文字
                iconPath	        String	是	图片路径，icon 大小限制为40kb
                selectedIconPath	String	是	选中时的图片路径，icon 大小限制为40kb
            
            position	    String	    否	    bottom	可选值 bottom、top
        
        networkTimeout 设置网络超时时间 （非必填 类型：Object）
            request	        Number	否	wx.request的超时时间，单位毫秒
            connectSocket	Number	否	wx.connectSocket的超时时间，单位毫秒
            uploadFile	    Number	否	wx.uploadFile的超时时间，单位毫秒
            downloadFile	Number	否	wx.downloadFile的超时时间，单位毫秒
            
        debug 设置是否开启 debug 模式   （非必填 类型：Boolean）
        
    
    
    
  例
  {
    "pages": [     //整体写 不用后缀
      "pages/index/index",
      "pages/logs/index"
    ],
    "window": {                          //设置小程序的状态栏、导航条、标题、窗口背景
      "navigationBarTitleText": "Demo",  //导航栏标题文字内容
      "navigationBarBackgroundColor": "HexColor"， //导航栏背景颜色
      "navigationBarTextStyle" : "white"， //导航栏标题颜色 注：仅支持 black/white
      "backgroundColor":"HexColor",  //	下拉背景字体、loading 图的样式，仅支持 dark/light
      "backgroundTextStyle" :"white"，
      "enablePullDownRefresh": true //是否开启下拉刷新
    
    
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
  
  
  
App.js
    App({//生命周期函数
      onLaunch: function() { // 小程序初始化完成，会触发 onLaunch（**_注：全局只出发一次_**）
        // Do something initial when launch.
      },
      onShow: function() { //小程序启动，或 从 _后台进入前台显示_，会触发 onShow
          // Do something when show.
      },
      onHide: function() { //小程序从 _前台进入后台_， 会触发 onHide
          // Do something when hide.
      },
      globalData: 'I am global data'
    })
    
   onLaunch	Function	生命周期函数--监听小程序初始化	当小程序初始化完成时，会触发 onLaunch（全局只触发一次）
   onShow	Function	生命周期函数--监听小程序显示	当小程序启动，或从后台进入前台显示，会触发 onShow
   onHide	Function	生命周期函数--监听小程序隐藏	当小程序从前台进入后台，会触发 onHide
   其他	     Any	     开发者可以添加任意的函数或数据到 Object 参数中，用 this 可以访问
 
    **_前台、后台定义_** ： 当用户点击左上角关闭，或者按了设备 Home 键离开微信，小程序并没有直接销毁，而是进入了后台；当再次进入微信或再次打开小程序，又会从后台进入前台。
    
    只有当小程序进入后台一定时间，或者系统资源占用过高，才会被真正的销毁。
  
  getApp()
  全局函数 getApp() ,使用this 就可以拿到小程序实例
  
 
 
Page
    page({...}) 函数用来注册一个页面。接受一个object 参数，其指定页面的初始数据、生命周期函数、事件处理函数等
    
1、 object参数说明
      data	                Object	    页面的初始数据
      onLoad	            Function	生命周期函数--监听页面加载
      onReady	            Function	生命周期函数--监听页面初次渲染完成
      onShow	            Function	生命周期函数--监听页面显示
      onHide	            Function	生命周期函数--监听页面隐藏
      onUnload	            Function	生命周期函数--监听页面卸载
      onPullDownRefresh 	Function	页面相关事件处理函数--监听用户下拉动作
      onReachBottom	        Function	页面上拉触底事件的处理函数
      其他	Any	开发者可以添加任意的函数或数据到 object 参数中，在页面的函数中用 this 可以访问

    wxml引用事例
        <view>{{text}}</view>
        <view>{{array[0].msg}}</view>
        
    js 事例
        Page({
          data: {
            text: 'init data',
            array: [{msg: '1'}, {msg: '2'}]
          }
        })
 
  
2、  生命周期函数
      onLoad: 页面加载
      一个页面只会调用一次。
      接收页面参数可以获取wx.navigateTo和wx.redirectTo及<navigator/>中的 query。
      
      onShow: 页面显示
      每次打开页面都会调用一次。
     
      onReady: 页面初次渲染完成 
      一个页面只会调用一次，代表页面已经准备妥当，可以和视图层进行交互。
      对界面的设置如wx.setNavigationBarTitle请在onReady之后设置。详见生命周期
      
      onHide: 页面隐藏
      当navigateTo或底部tab切换时调用。
      
      onUnload: 页面卸载
      当redirectTo或navigateBack的时候调用。
     
  
  
 3、页面相关事件处理函数
   onPullDownRefresh: 下拉刷新
    监听用户下拉刷新事件。
    需要在config的window选项中开启enablePullDownRefresh。
    当处理完数据刷新后，wx.stopPullDownRefresh可以停止当前页面的下拉刷新。
    
    
    
 4、事件处理函数
    除了初始化数据和生命周期函数，Page 中还可以定义一些特殊的函数：事件处理函数。在渲染层可以在组件中加入事件绑定，当达到触发事件时，就会执行 Page 中定义的事件处理函数。

    
    示例代码：
    wxml中
    <view bindtap="viewTap"> click me </view>
    
    js中
        Page({
                viewTap: function() {
                    console.log('view tap')
                }
            })
            
    
    Page.prototype.setData()
        setData 函数用于将数据从逻辑层发送到视图层，同时改变对应的 this.data 的值。

        ** 注意：**
                 ** 直接修改 this.data 无效，无法改变页面的状态，还会造成数据不一致。**
                 ** 单次设置的数据不能超过1024kB，请尽量避免一次设置过多的数据。**
       
                 
setData() 参数格式
    接受一个对象，以 key，value 的形式表示将 this.data 中的 key 对应的值改变成 value。
    其中 key 可以非常灵活，以数据路径的形式给出，如 array[2].message，a.b.c.d，并且不需要在 this.data 中预先定义。

    示例代码：

        <!--index.wxml-->
        <view>{{text}}</view>
        <button bindtap="changeText"> Change normal data </button>
        <view>{{array[0].text}}</view>
        <button bindtap="changeItemInArray"> Change Array data </button>
        <view>{{object.text}}</view>
        <button bindtap="changeItemInObject"> Change Object data </button>
        <view>{{newField.text}}</view>
        <button bindtap="addNewField"> Add new data </button>


    //index.js
    Page({
      data: {
        text: 'init data',
        array: [{text: 'init data'}],
        object: {
          text: 'init data'
        }
      },
      changeText: function() {
        // this.data.text = 'changed data'  // bad, it can not work
        this.setData({
          text: 'changed data'
        })
      },
      changeItemInArray: function() {
        // you can use this way to modify a danamic data path
        this.setData({
          'array[0].text':'changed data'
        })
      },
      changeItemInObject: function(){
        this.setData({
          'object.text': 'changed data'
        });
      },
      addNewField: function() {
        this.setData({
          'newField.text': 'new data'     //this.data 不需要预先定义
        })
      }
    })