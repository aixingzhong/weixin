MINA框架程序包含一个描述整体程序的 app 和多个描述各自页面的 page。
主体部分由三个文件组成，必须放在项目的根目录：app.js，app.json,app.wxss,
一个框架页面由四个文件组成，分别是自己写的js，wxml，wxss，json，这四个文件必须具有相同的路径与文件名。框架方便调用


主体app.js: 小程序逻辑
App()函数用于项目根目录app.js中用来注册一个小程序。接受一个object参数.

onLaunch :生命周期函数，监听小程序初始化，当小程序初始化完成时触发

onShow:生命周期函数，监听小程序显示，当小程序启动或从后台进入前台是触发

onHide：生命周期函数，当小程序从前台进入后台是触发

其他：开发者可以添加任意的函数或数据，用this可以访问


主体app.json: 小程序公共设置
pages:设置页面路径

window：设置默认页面的窗口表现

tabBar:设置底部tab的表现

networkTimeout：设置网络超时时间

debug：设置是否开启debug模式

主体app.wxss:设置公共的通用样式


逻辑层（app service） 逻辑层将数据进行处理后发送给视图层，同时接受视图层的事件反馈

App()必须在app.js中注册，且不能注册多个。函数用来注册一个小程序。接受一个object参数，其指定小程序的生命周期函数等。

getApp()可以获取到小程序实例。通过getApp获取实例之后，不要私自调用生命周期函数。

Page()函数用来注册一个页面。接受一个object参数，其指定页面的初始数据、生命周期函数、事件处理函数等。

初始化数据：page注册页面后可以通过data对象初始化数据

事件处理函数：程序不是运行在浏览器中，没有全局对象，不能通过js获取元素帮定事件
通过设置元素的自定义属性bindtap来绑定自定义的函数事件

setData（）函数用于将数据从逻辑层发送到视图层，通过this.setData()改变对应的绑定元素数据，同时改变对应的this.data的值

getCurrentPages() 函数用于获取当前页面栈的实例，以数组形式按栈的顺序给出，第一个元素为首页，最后一个元素为当前页面。
注意：不要尝试修改页面栈，会导致路由以及页面状态错误。

框架视图层（view）  将逻辑层的数据反应成视图，同时将视图层的事件发送给逻辑层。

WXML（WeiXin Markup Language）MINA框架设计的一套标签语言，结合基础组件、事件系统，可以构建出页面的结构。（又可以多学一门微信语言了）

数据绑定：WXML中的动态数据均来自对应Page的data。

简单的数据绑定：通过页面元素值{{xxx}}获得js中的page函数中data中的xxx对象中属性值


列表渲染数据绑定：页面元素通过设置属性wx:for-items="{{xxx}}",值为{{item}},for循环js中的page函数中的data中的xxx对象中的属性值，
生成相对的元素和元素的值

条件渲染数据绑定：页面元素通过设置设置属性wx:if="",wx:elif="",wx:else="";如果true则生成显示该元素

模板数据绑定：template元素设置name=“xxx”为模板，template通过is=“xxx”找到相对应的模板，data=“{{...dataobject}”获取js中
page函数中data中的dataobject的值

微信小程序组件：
视图容器，基础内容，表单组件，操作反馈，导航，媒体组件，地图，画布，客服回话

API
网络API列表：
wx.request   		发起网络请求,wx.request发起的是https请求。一个微信小程序，同时只能有5个网络请求连接。
wx.uploadFile    	上传文件,将本地资源上传到开发者服务器
wx.downloadFile         下载文件,下载文件资源到本地
wx.connectSocket  	创建webSocket连接,一个微信小程序同时只能有一个webSocket连接
wx.onSocketOpen   	监听webSocket打开
wx.onSocketError	监听webSocket错误
wx.sendSocketMessage 	发送websocket消息
wx.onSocketMessage      接受websocket消息
wx.closeSocket 		关闭websocket连接
wx.onSocketClose	监听webSocket

媒体API列表：
wx.chooseImage			从相册选择图片或者拍照
wx.previewImage			预览图片
wx.startRecord			开始录音,当主动调用wx.stopRecord，或者录音超过1分钟时自动结束录音，返回录音文件的临时文件路径
wx.stopRecord			结束录音
wx.playVoice			播放语音,同时只允许一个语音文件正在播放，如果前一个语音文件还没播放完，将中断前一个语音播放。
wx.pauseVoice 			暂停播放语音,再次调用wx.playVoice播放同一个文件时，会从暂停处开始播放。如果想从头开始播放，需要先调用wx.stopVoice
wx.getBackgroundAudioPlayerState	获取音乐播放状态
wx.playBackroundAudio		播放音乐
wx.pauseBackgroundAudio		暂停播放音乐
wx.seekBackgroundAudio		控制音乐播放进度
wx.stopBackgroundAudio		停止播放音乐
wx.onBackgroundAudioPlay	监听音乐开始播放
wx.onBackgroundAudioPause	监听音乐暂停
wx.onBackgroundAudioStop	监听音乐结束
wx.chooseVideo			从相册选择视频，或者拍摄,返回视频的临时文件路径。
wx.saveFile			保存文件
wx.createAudioContext(audioId)   创建并返回 audio 上下文 audioContext 对象
wx.createVideoContext(videoId)	创建并返回 video 上下文 videoContext 对象
wx.getSavedFileList(OBJECT)	获取本地已保存的文件列表
wx.getSavedFileInfo(OBJECT)	获取本地文件的文件信息
wx.removeSavedFile(OBJECT)	删除本地存储的文件
wx.openDocument(OBJECT)		新开页面打开文档，支持格式：doc, xls, ppt, pdf, docx, xlsx, pptx

数据API列表：
wx.getStorage		获取本地数据缓存
wx.setStorage		设置本地数据缓存
wx.clearStorage		清理本地数据缓存

位置API列表：
wx.getLocation		获取当前位置
wx.openLocation		打开内置地图

设备API列表：
wx.getNetworkType		获取网络类型
wx.getSystemInfo		获取系统信息
wx.onAccelerometerChange	监听重力感应数据
wx.onCompassChange		监听罗盘数据
wx.makePhoneCall(OBJECT)  	拨打电话
wx.scanCode(OBJECT)		调起客户端扫码界面，扫码成功后返回对应的结果

界面API列表：
wx.setNavigationBarTitle	设置当前页面标题
wx.showNavigationBarLoading	显示导航条加载动画
wx.hideNavigationBarLoading	隐藏导航条加载动画
wx.navigateTo	新窗口打开页面
wx.redirectTo	原窗口打开页面
wx.navigateBack	退回上一个页面
wx.createAnimation	动画
wx.createContext	创建绘图上下文
wx.drawCanvas	绘图
wx.hideKeyboard	隐藏键盘
wx.stopPullDownRefresh	停止下拉刷新动画

开放接口：
wx.login		登录
wx.getUserInfo		获取用户信息
wx.requestPayment	发起微信支付


微信小程序API界面交互

wx.showToast(OBJECT)	微信小程序显示消息提示框

wx.hideToast()		隐藏消息提示框

wx.showModal(OBJECT)	微信小程序​显示模态弹窗

wx.showActionSheet(OBJECT)	微信小程序显示操作菜单

wx.setNavigationBarTitle(OBJECT)	 动态设置当前页面的标题

wx.showNavigationBarLoading()		​ 在当前页面显示导航条加载动画

wx.hideNavigationBarLoading()		隐藏导航条加载动画

wx.navigateTo(OBJECT)			保留当前页面，跳转到应用内的某个页面，使用wx.navigateBack可以返回到原页面。

wx.redirectTo(OBJECT)			关闭当前页面，跳转到应用内的某个页面。

wx.navigateBack(OBJECT)			关闭当前页面，返回上一页面或多级页面。可通过 getCurrentPages()) 获取当前的页面栈，决定需要返回几层。

wx.switchTab(OBJECT)			跳转到 tabBar 页面，并关闭其他所有非 tabBar 页面

wx.createAnimation(OBJECT)		 创建一个动画实例animation。调用实例的方法来描述动画。最后通过动画实例的export方法导出动画数据传递给组件的animation属性。

animation				动画实例可以调用以下方法来描述动画，调用结束后会返回自身，支持链式调用的写法。

wx.createContext()			 创建并返回绘图上下文context对象。

wx.hideKeyboard()			 收起键盘

onPullDownRefresh			在 Page 中定义 onPullDownRefresh 处理函数，监听该页面用户下拉刷新事件

wx.stopPullDownRefresh()		停止当前页面下拉刷新。


开放接口
wx.login(OBJECT)			调用接口获取登录凭证（code）进而换取用户登录态信息，包括用户的唯一标识（openid） 及本次登录的 会话密钥（session_key）。
					用户数据的加解密通讯需要依赖会话密钥完成。


wx.checkSession(OBJECT)			检查登陆态是否过期

wx.getUserInfo(OBJECT)			微信小程序获取用户信息，需要先调用wx.login接口

wx.requestPayment(OBJECT)		微信小程序发起微信支付


微信小程序API 分享 
onShareAppMessage		设置该页面的分享信息



微信小程序 Q&A

bindchange			获取用户输入

样式表不支持级联选择器

本地资源无法通过css获取

本地资源无法通过css获取

