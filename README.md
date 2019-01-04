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
      注：1.当页面存在计时器试，需要注意计时器启动和取消的位置；
          2.当用户按home键或者右上角圆点退出小程序，执行onHide onUnload执行情况
      
      //以上为page页面的生命周期
      
      onReachBottom: function() {
        //触底事件 如分页
      },
      onShareAppMessage: function () {
       // return custom share data when user share.
      },
       ......
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
    
    注：wx.navigateTo()最多只能跳5次，因为小程序页面的实例使用栈的数据结构存储，栈内元素最多5个
### 小程序跳转页面传参
    url: '../../xxx?A=a & B=b'
### 小程序的下拉分页
    data: {
        pageIndex: 1;       //默认为1，当前请求数据为第几页，请求1次加一
        pageSize: 10;       //每页显示记录条数，这里显示10条记录
        isLastPage: 0;      //'0'表示false '1'表示true
        contentList: []
    }
    (1)请求的记录条数<=0,改变isLastPage的状态值，isLastPage:1
    (2)请求的记录条数<每页需要显示的记录条数      isLastPage:1
    (3)记录条数>显示数
    满足（2）（3）则触发：
    请求接口，将记录填充到contentList里，每请求一次，pageIndex+1，
    改变默认的pageIndex的值 this.setData({pageIndex: this.data.pageIndex})
    第二次后的数据，使用数组合并，并到contentList中；
    
    
    
   
    
 
    
    
    
    
    
    
    
    
    
    
    
    
