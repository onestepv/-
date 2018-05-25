## 小程序的的学习
### 小程序的生命周期
    小程序的生命周期：
    APP({
      onLanuch: function(options) {...},
      //当小程序初始化完成时，会触发(全局只触发一次)
      onShow: function(options) {...},
      //当小程序启动时，或者从后台转入前台时会触发
      onHide: function(options) {...},
      //当小程序从前台进入后台时会触发
    })
    globalData: 用来存放小程序每个页面统一的信息

### 小程序page页面的生命周期
    Page({
      data: {
        text: "This is page data."
      },
      onLoad: function(options) {
        // 页面加载时触发
        //options的值为上个页面的传值
        //可以通过this.setData({...})将上个页面的传值存进本页面
      },
      onReady: function() {
        // 页面显示时触发
      },
      onShow: function() {
        // 页面初次渲染完成
      },
      onHide: function() {
        // 页面隐藏
      },
      onUnload: function() {
        // 页面卸载(当redirectTo或navigateBack时调用)
      },
      //以上为page页面的生命周期
      onPullDownRefresh: function() {
        // 下拉事件
      },
      onReachBottom: function() {
        //触底事件 如分页
      },
      onShareAppMessage: function () {
       // return custom share data when user share.
      },
      onPageScroll: function() {
        // Do something when page scroll
      },
    })
### onLoad onReady onShow的响应顺序
    onLoad > onShow > onReady
    onShow 相当于jquery里的$(document).ready 文档结构加载完成（不包含图片等非文字媒体文件）
    onReady 相当于window.onload 表示页面包含图片在内的所有元素都加载完毕
### 小程序的text标签默认有上边距
    解决办法：
    display: block;
### wx.redirectTo()和wx.navigateTo()
    前者相当于location.replace() 关闭当前页面，跳转到应用内的某个页面
    后者相当于location.href() 保留当前页面，跳转到应用内的某个页面，使用wx.navigateBack可以返回到原页面
    
    后者会在浏览历史记录(history)对象中增加一条新的记录，前者则相当于用replace中的url代替了现有的页面url，
    把history的url替换为重新定向后的url。
    
