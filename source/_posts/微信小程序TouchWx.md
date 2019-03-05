---
title: 微信小程序TouchWx
date: 2019-02-25 17:39:43
tags: 微信小程序
categories: 
- 微信小程序
- Touch Wx
---

### 微信小程序框架TouchWx

Touch Wx框架：http://www.wetouch.net/wx.html

优势：

1. 有丰富的组件，基于原生，并且原生组建也可以使用
2. 可以在输出的原始代码进行继续开发
3. 开发完成后可以将代码转为H5界面

##### 一、Touch Wx

1、安装和第一个程序

可以参考官方的文档：

http://www.wetouch.net/touchwx_doc/quickstart/begin/ide

创建第一个Touch Wx程序按照官方文档就可以，很快速

2、使用Touch Wx制作登陆界面

<div align=center>
    <img width=200 src='/images/TouchWx/2636.gif'/>
</div>



最后结果如上图

使用的是Touch Wx框架和组件，提交校验使用的是WxValidate.js，动态校验是自己增加的

touchWx 有一些非常好用的封装组件，以及封装的样式

**居中**：直接再css中增加即可.mix-flex-center();

```css
.name-text {
  margin-left: 8%;
  .mix-flex-center();
  width: 80px;
  height: 30px;
  background: #ffffff;
}
```

是将display:flex属性进行了封装，在源码中就可以看到

<div align=center>
    <img width=200 src='/images/TouchWx/text.png'/>
</div>

**阴影效果**：

```
box-shadow: 3px 3px 8px #e57a7e;
```

引用iconfont图片

按照官网的步骤，

http://www.wetouch.net/touchwx_doc/quickstart/extend/icon

最后引用使用下边这句话即可icon-yess为下载时对应的图片名称

```
<ui-icon type="icon-yess" size="40"></ui-icon> 
```

**这里需要注意**：

1. 打开app.wxa文件，保存一下，确保样式被加载进来
2. icon-yess名字需要对应
3. 是将iconfont.ttf文件转为Base64，不是iconfont.css中的base64



##### 二、WxValidate使用

WxValidate使用比较简单，在提交的时候进行判断信息是否填写完成

下载WxValidate.js文件

下载地址：https://github.com/skyvow/wx-extend/tree/master/src/assets/plugins/wx-validate

代码中引入

```
<script>
import WxValidate from "../../static/utils/WxValidate";
</script>
```

引入之后，需要先进行初始化校验

```js
initValidate() {
    const rules = {
      name: {
        required: true,
        rangelength: [1, 8]
      },
      tel: {
        required: true,
        tel: true
      }
    };
    const message = {
      name: {
        required: "请输入姓名",
        rangelength: "请输入1~8个字符"
      },
      tel: {
        required: "请输入电话号码",
        tel: "请输入正确的手机号码"
      }
    };
    this.WxValidate = new WxValidate(rules, message);
  }
```

提交的时候进行判断

```js
if (!this.WxValidate.checkForm(params)) {
      const error = this.WxValidate.errorList[0];
      wx.showModal({
        content: error.msg,
        showCancel: false
      });
      return false;
    }
```

<div align=center>
    <img width=200 src='/images/TouchWx/show.png'/>
</div>



主要代码

```
<template>
  <view class="page">
    <form class="content"  bindsubmit='submitForm'>
        <view class="name">
          <view class="name-text">姓名</view>
          <view class="name-row">
            <view class="name-row-icon" ></view>
            <input class="name-input" name='name' placeholder-class="placeholder" type="text" placeholder="请输入姓名" data-id="isShow1" 
              data-success="isSuccess1" data-name="name" data-style="borderChange1" bindblur="inputName" bindinput="inputInfo" value="{{name}}" style="{{borderChange1}}"/>
            <view class="name-row-icon" wx:if="{{ isShow1 }}">
              <icon type="success" size="24" wx:if="{{ isSuccess1 }}"></icon>
              <icon type="cancel" size="24" wx:if="{{ !isSuccess1 }}"></icon>
            </view>
          </view>
        </view>
        <view class="name">
          <view class="name-text">电话</view>
          <view class="name-row">
            <view class="name-row-icon" ></view>
            <input class="name-input" name='tel' placeholder-class="placeholder" type="number" placeholder="请输入电话"  data-id="isShow2" 
              data-success="isSuccess2" data-name="tel" data-style="borderChange2" bindblur="inputName" bindinput="inputInfo"  value="{{tel}}"  style="{{borderChange2}}"/>
            <view class="name-row-icon" wx:if="{{ isShow2 }}">
              <icon type="success" size="24"  wx:if="{{ isSuccess2 }}"></icon>
              <icon type="cancel" size="24"  wx:if="{{ !isSuccess2 }}"></icon>
            </view>
          </view>
        </view>
        <view class="name">
          <view class="name-text">QQ</view>
          <view class="name-row">
            <view class="name-row-icon" ></view>
            <input class="name-input" name="qqNum" placeholder-class="placeholder" type="number" placeholder="请输入QQ号码"  data-id="isShow3" 
              data-success="isSuccess3" data-name="qqNum" data-style="borderChange3" bindblur="inputName" bindinput="inputInfo" value="{{qqNum}}" style="{{borderChange3}}"/>
            <view class="name-row-icon" wx:if="{{ isShow3 }}">
              <icon type="success" size="24"  wx:if="{{ isSuccess3 }}"></icon>
              <icon type="cancel" size="24"  wx:if="{{ !isSuccess3 }}"></icon>
            </view>
          </view>
          <!-- <ui-icon type="icon-yess" size="40"></ui-icon> -->
        </view>
        <view class="submit-button">
          <button form-type='submit' class="button-style-demo1">立即提交</button>
        </view>
    </form>
  </view> 
</template>

<script>
import WxValidate from "../../static/utils/WxValidate";
export default {
  config: {
    navigationBarTitleText: "首页",
    backgroundColor: "#F4F4F4",
    navigationBarTextStyle: "black",
    usingComponents: {
      "cc-city": "../../packages/cc-city"
    }
  },
  data: {
    borderChange1:
      "border: 1px solid #84bb95; box-shadow: 2px 2px 8px #84bb95;",
    borderChange2:
      "border: 1px solid #84bb95; box-shadow: 2px 2px 8px #84bb95;",
    borderChange3:
      "border: 1px solid #84bb95; box-shadow: 2px 2px 8px #84bb95;",
    noFill: "border: 1px solid #c01920; box-shadow: 2px 2px 8px #e57a7e;",
    fill: "border: 1px solid #84bb95; box-shadow: 2px 2px 8px #84bb95;"
  },
  onLaunch() {
    console.log("onLaunch");
  },
  onShow() {},
  onLoad() {
    this.initValidate();
  },
  //输入框输入完后
  inputName(e) {
    console.log(e);
    var show = e.currentTarget.dataset.id;
    var isSuccess = e.currentTarget.dataset.success;
    var borderchange = e.currentTarget.dataset.style;
    console.log("val:", borderchange);
    var val = e.detail.value;
    //[`${isSuccess}`]   [show]
    this.setData({
      [show]: true
    });
    if (val == "") {
      var that = this;
      this.setData({
        [`${isSuccess}`]: false,
        [`${borderchange}`]: this.data.noFill
      });
    } else {
      var bool = false;
      var temp = e.currentTarget.dataset.name;
      console.log(temp);
      switch (temp) {
        case "name":
          console.log("inputName", "name");
          bool = true;
          break;
        case "tel":
          console.log("inputName", "tel");
          bool = this.tel(val);
          break;
        case "qqNum":
          console.log("inputName", "qqNum");
          bool = this.qq(val);
          break;
      }
      if (bool) {
        this.setData({
          [`${isSuccess}`]: true,
          [`${borderchange}`]: this.data.fill
        });
      } else {
        this.setData({
          [`${isSuccess}`]: false,
          [`${borderchange}`]: this.data.noFill
        });
      }
    }
  },
  //输入框输入时触发
  inputInfo(e) {
    var borderchange = e.currentTarget.dataset.style;
    var show = e.currentTarget.dataset.success;
    var name = e.currentTarget.dataset.name;
    var val = e.detail.value;
    this.setData({
      [name]: val.replace(/\s+/g, "")
    });
    if (val == "") {
      this.setData({
        [`${show}`]: false
      });
    } else {
      var bool = false;
      var temp = e.currentTarget.dataset.name;
      console.log(temp);
      switch (temp) {
        case "name":
          bool = true;
          break;
        case "tel":
          bool = this.tel(val);
          break;
        case "qqNum":
          bool = this.qq(val);
          console.log(bool);
          break;
      }
      if (bool) {
        this.setData({
          [`${show}`]: true,
          [borderchange]: this.data.fill
        });
      } else {
        this.setData({
          [`${show}`]: false,
          [borderchange]: this.data.noFill
        });
      }
    }
  },

  tel(value) {
    return /^1[34578]\d{9}$/.test(value);
  },
  qq(value) {
    return value.length <= 12 && value.length >= 4;
  },
  //初始化规则
  initValidate() {
    const rules = {
      name: {
        required: true,
        rangelength: [1, 8]
      },
      tel: {
        required: true,
        tel: true
      }
    };
    const message = {
      name: {
        required: "请输入姓名",
        rangelength: "请输入1~8个字符"
      },
      tel: {
        required: "请输入电话号码",
        tel: "请输入正确的手机号码"
      }
    };
    this.WxValidate = new WxValidate(rules, message);
  },
  //提交
  submitForm(e) {
    const params = e.detail.value;
    console.log(params);
    if (!this.WxValidate.checkForm(params)) {
      const error = this.WxValidate.errorList[0];
      wx.showModal({
        content: error.msg,
        showCancel: false
      });
      return false;
    }
  }
};
</script>

<style lang="less">
.page {
  widows: 100%;
  height: 100%;
  .mix-flex-center();
  background-color: #ededee;
}
.content {
  width: 80%;
  height: 90%;
  border-radius: 10px;
  background-color: #ffffff;
  display: block;
}
.name {
  height: 80px;
  width: 100%;
}
.name-text {
  margin-left: 8%;
  .mix-flex-center();
  width: 80px;
  height: 30px;
  background: #ffffff;
}
.name-row {
  display: flex;
  width: 100%;
}
.name-row-icon {
  width: 12%;
  .mix-flex-center();
}

.name-input {
  height: 40px;
  width: 72%;
  font-size: 14px;
  border-radius: 10px;
  padding-left: 10px;
}
.placeholder {
  color: #ccc;
}
.submit-button {
  width: 100%;
  .mix-flex-center();
}
.button-style-demo1 {
  width: 60%;
  background-color: #c01920;
  border-radius: 20px;
  border-color: #c01920;
  box-shadow: 3px 3px 8px #e57a7e;
  color: #fff;
}
.button-style-demo1::after {
  border: none;
}
</style>
```

