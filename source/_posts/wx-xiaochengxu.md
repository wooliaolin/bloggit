---
title: 微信小程序,简易教程
date: 2017-10-31
categories: 
- 微信小程序
- 
---

# [小程序简易教程](https://mp.weixin.qq.com/debug/wxadoc/dev/)

### 创建页面
每一个[小程序页面](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/app-service/page.html)是由同路径下同名的四个不同后缀文件的组成，如：index.js、index.wxml、index.wxss、index.json。.js后缀的文件是脚本文件，.json后缀的文件是配置文件，.wxss后缀的是样式表文件，.wxml后缀的文件是页面结构文件。

> 常用标签 [`<view/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/component/view.html)、[`<image/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/component/image.html)、[`<text/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/component/text.html) 、[`<block/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxml/list.html)

###### `index.wxml` 是页面的结构文件：
```
<!--index.wxml-->
<view class="container">
  <view class="userinfo">
    <block wx:if="{{hasUserInfo}}">
      <image bindtap="bindViewTap" class="userinfo-avatar" src="{{userInfo.avatarUrl}}" background-size="cover"></image>
      <text class="userinfo-nickname">{{userInfo.nickName}}</text>
    </block>
    <button wx:else open-type="getUserInfo" bindgetuserinfo="getUserInfo"> 获取头像昵称 </button>
  </view>
  <view class="usermotto">
    <text class="user-motto">{{motto}}</text>
  </view>
</view>
```
本例中使用了 [`<view/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/component/view.html)、[`<image/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/component/image.html)、[`<text/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/component/text.html) 来搭建页面结构，绑定数据和交互处理函数。

###### `index.js` 是页面的脚本文件。
在这个文件中我们可以监听并处理页面的生命周期函数、获取小程序实例，声明并处理数据，响应页面交互事件等。

```
//index.js
//获取应用实例
const app = getApp()

Page({
  data: {
    motto: 'Hello World',
    userInfo: {},
    hasUserInfo: false
  },
  //事件处理函数
  bindViewTap: function() {
    wx.navigateTo({
      url: '../logs/logs'
    })
  },
  onLoad: function () {
    if (app.globalData.userInfo) {
      this.setData({
        userInfo: app.globalData.userInfo,
        hasUserInfo: true
      })
    } else {
      // 由于 getUserInfo 是网络请求，可能会在 Page.onLoad 之后才返回
      // 所以此处加入 callback 以防止这种情况
      app.userInfoReadyCallback = res => {
        this.setData({
          userInfo: res.userInfo,
          hasUserInfo: true
        })
      }
    }
  },
  getUserInfo: function(e) {
    this.setData({
      userInfo: e.detail.userInfo,
      hasUserInfo: true
    })
  }
})
```

###### `index.wxss` 是页面的样式表：
```
/**index.wxss**/
.userinfo {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.userinfo-avatar {
  width: 128rpx;
  height: 128rpx;
  margin: 20rpx;
  border-radius: 50%;
}

.userinfo-nickname {
  color: #aaa;
}

.usermotto {
  margin-top: 200px;
}
```
页面的样式表是<font style="color:red">非必要</font>的。当有页面样式表时，页面的样式表中的样式规则会层叠覆盖 app.wxss 中的样式规则。如果不指定页面的样式表，也可以在页面的结构文件中直接使用 app.wxss 中指定的样式规则。

###### `index.json` 是页面的配置文件：
页面的配置文件是<font style="color:red">非必要</font>的。当有页面的配置文件时，配置项在该页面会覆盖 app.json 的 window 中相同的配置项。如果没有指定的页面配置文件，则在该页面直接使用 app.json 中的默认配置。

###### 使用 [`<block/>`](https://mp.weixin.qq.com/debug/wxadoc/dev/framework/view/wxml/list.html) 控制标签来组织代码，在 <block/> 上使用 wx:for 绑定 logs 数据，并将 logs 数据循环展开节点
logs 的页面结构
```
<!--logs.wxml-->
<view class="container log-list">
  <block wx:for="{{logs}}" wx:for-item="log">
    <text class="log-item">{{index + 1}}. {{log}}</text>
  </block>
</view>
```




