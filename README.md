#模块文档

[Vscroll-banner](#vscroll-banner "竖直滚动banner") [formVerify](#formverify "表单验证") [scrollToBottom](#scrolltobottom "滑动到底部事件") [loadFile](#loadfile "异步加载文件") [pay](#pay "支付") [sliderGroup](#slidergroup "div窗口组") [IScrollSimple](#iscrollsimple "iscroll窗口组") [echo-taichiyi](#echo-taichiyi "懒加载") [pullToRefreshA](#pulltorefresha "下拉刷新") 


## Vscroll-banner

竖直滚动banner

```
VscrollBanner('selector');
VscrollBanner({params});
```

### selector
 - 类型: 字符串
 - 默认值: 无
 - 描述: 选择器, 如: '#VscrollBanner1'

### params
speed

 - 类型: 数字
 - 默认值: 300 (单位:ms)
 - 描述: 滚动速度

interval

 - 类型: 字符串
 - 默认值: 3000 (单位:ms)
 - 描述: 滚动间隔时间

type

 - 类型: 字符串
 - 默认值: single
 - 描述: 单行显示双行显示, double(双行), single(单行) 


## 实例

 ```
 VscrollBanner('.js_vscrollbanner__wrap');

 VscrollBanner('.js_vscrollbanner__wrap', {
     type: 'double',
     interval: 1200,
 });

 ```


## formVerify

如果想验证某个表单元素请在该元素上添加Class: js_form-verify

```
scrollToBottom(callback(ret, err))
```

### 验证规则

在带有js_form-verify类的表单元素上添加以下属性, 会进行相应的验证, 单个表单元素可以同时添加多个属性

#### required

 - 说明: required = 0 时, 表示此元素为选填
 - 默认值: 无

例子

```
<input type="text" name="id" class="js_form-verify" data-required="0">
```

#### tips

 - 说明: 验证错误时的提示
 - 默认值: 请填写所有必填项

例子

```
<input type="text" name="id" class="js_form-verify" data-tips="缺少id字段">
```

#### regular

 - 说明: 验证规则为正则表达式
 - 默认值: 无

例子

```
<input type="tel" name="phone" class="js_form-verify" data-regular="/^1[34578]\d{9}$/" data-tips="请输入11位正确手机号">
```

#### eqlength

 - 说明: 该元素的值的长度得等于设定的值
 - 默认值: 无

例子

```
<input type="password" name="password" class="js_form-verify" data-eqlength="6" data-tips="密码长度必须为6位数">
```

#### maxlength

 - 说明: 该元素的值的长度得小于设定的值
 - 默认值: 无

例子

```
<input type="password" name="password" class="js_form-verify" data-maxlength="16" data-tips="密码长度不能大于16位数">
```

#### minlength

 - 说明: 该元素的值的长度得大于设定的值
 - 默认值: 无

例子

```
<input type="password" name="password" class="js_form-verify" data-minlength="8" data-tips="密码长度不能小于8位数">

<textarea name="feedback" placeholder="请输入您的反馈" class="js_form-verify" data-minlength="8" data-tips="反馈内容不能少于8个字"></textarea>
```

#### eqname

 - 说明: 两个元素的值是否相等, eqname的值为要将相比元素的name
 - 默认值: 无

例子

```
<input type="password" name="user_password" class="js_form-verify" data-minlength="8" data-tips="密码长度不能小于8位数">

<input type="password" name="user_repassword" class="js_form-verify" data-eqname="user_password" data-tips="两次输入的密码不一致">
```

### 方法说明

#### callback(ret, err)

- 说明: 验证成功会返回表单数据
- 类型: JSON 对象
- 内部字段: 

```json
{
    status: true          //布尔类型；操作状态值
    data: {}              //JSON 对象；表单数据
    msg: ''           //字符串；错误提示
}
```

#### 实例

```javascript
form_verify(function(ret) {
    if (ret.status) {
        // 验证通过
        console.log(ret.data);
    } else {
        // 验证失败
        console.log(ret.msg);
    }
});
```

##**scrollToBottom**
######滑动到底部事件
######scrollToBottom({params}, callback())

###**params**

####selector:
- 类型: 字符串
- 默认值: 无
- 描述: 监听某个div到底部则填该div的选择器, 如果要监听整个窗口则填body.

> 别忘了设置该元素的高度(也就是height属性)

####distance:
- 类型: 数字
- 默认值: 0
- 描述: 离底部到还多少距离时触发事件

###**callback(ret, err)**
ret:
- 类型: JSON 对象
- 内部字段：
~~~
{
    status: true          //布尔类型；
    toBottom: false       	   //布尔类型；是否到达底部
    scrollTop: 10          //数字 ; 距离顶部的距离 ; 
}
~~~
err:
- 类型: JSON 对象
- 内部字段：
~~~
{
    msg: ''       	   //字符串类型；错误提示
}
~~~
###**示例代码**
~~~
scrollToBottom({
    selector: '#scrolltobottom-wrap',
    // selector: '.scrolltobottom-wrap',
    // selector: 'body',
    distance: 20 //到达底部的距离
}, function(ret, err) {
    console.log('到底部了');
});
~~~

##**loadFile**
###### 异步加载文件,如.json, .js, .css
###### loadFile({params, callback(ret, err)})

###**params**

####url:
- 类型: 字符串
- 默认值: 无
- 描述: 支持本地路径 和 远程链接

###**callback(ret, err)**
ret:
- 类型: JSON 对象
- 内部字段：
~~~
{
    status: true          //布尔类型；如果加载的是JSON文件则为true
    data: {}       	   //JSON 对象；如果加载的是JSON文件则包含JSON文件数据, 否则为空对象
}
~~~
err:
- 类型: JSON 对象
- 内部字段：
~~~
{
    msg: ''       	   //字符串类型；错误提示
}
~~~
###**示例代码**
~~~
loadFile({
     url: '../js/city-datas.json'
     // url: 'http://cdn.bootcss.com/bootstrap/4.0.0-alpha.5/css/bootstrap-flex.css'
}, function(ret, err) {
    console.log(ret);
    console.log(err);
});

~~~

#**pay**
* * * * *

######封装了微信支付和支付宝的接口
>[warning] 需要添加两个APICloud模块: wxPay, aliPay

##**aliPay**
######支付宝支付
>[danger] 使用前请在此模块中配置好5个参数: partner, seller, rsaPriKey, rsaPubKey, notifyURL

官方文档: [http://docs.apicloud.com/Client-API/Open-SDK/aliPay#a3](http://docs.apicloud.com/Client-API/Open-SDK/aliPay#a3)

######aliPay({params}, callback(ret, err))

###**params**

####subject:
- 类型: 字符串
- 描述: 商品名

####body:
- 类型: 字符串
- 描述: 交易商品的简介

####amount:
- 类型: 字符串
- 描述: 交易商品的价钱（单位为元，精确到分如：10.29元）

####tradeNO:
- 类型: 字符串
- 描述: 交易订单编号（由商家按自己的规则生成），不可包含字母，否则在 iOS 平台上报错

>[info] 其他参数为选填, 更多参数参看官方文档

###**callback(ret, err)**
>[info] callback(ret, err) 参看示例代码

###**示例代码**
~~~
pay.aliPay({
    subject: '为18888888888支付100元话费',
    body: '移动网上营业厅'
    amount: '100.00',
    tradeNO: '72313122986723423'
}, function(ret, err) {
    if (ret.code === '9000') {
        alert(支付成功);
        // Do Something
    } else {
        // 支付失败
        console.log(ret.code); //失败状态码
        console.log(ret._msg); //失败提示
        // Do Something
    }
});
~~~
##**wxPay**
######微信支付
>[danger] 使用前请在此模块中配置好4个参数: apiKey, mchId, partnerKey, notifyUrl

官方文档: http://docs.apicloud.com/Client-API/Open-SDK/wxPay#b4

######wxPay({params}, callback(ret, err))
###**params**

####description:
- 类型: 字符串
- 描述: 商品或支付订单简要描述

####body:
- 类型: 字符串
- 描述: 交易商品的简介

####totalFee:
- 类型: 字符串
- 描述: 交易商品的价钱（单位为元，精确到分如：10.29元）

####tradeNo:
- 类型: 字符串
- 描述: 商户系统内部的订单号，32个字符以内，可包含字母

>[info] 其他参数为选填, 更多参数参看官方文档

###**callback(ret, err)**
>[info] callback(ret, err) 参看示例代码

###**示例代码**
~~~
pay.wxPay({
    description: '为18888888888支付100元话费',
    totalFee: '100.00',
    tradeNo: '72313122986723423'
}, function(ret, err) {
    if (ret.status) {
        alert('支付成功');
        // Do Something
    } else if (err && err.code) {
        switch (err.code) {
            case -2:
                alert('用户取消');

                break;
            case -1:
                alert(err._msg); //错误信息
                break;

            case 1:
                alert('必传参数缺失');
                break;

            default:
                alert(err._msg); //错误信息
                break;
        }
        // Do Something
    }
});
~~~

##**sliderGroup**
###### 创建div窗口组的实例
###### sliderGroup({params}, callback(index))
###**params**

####id:
- 类型: 字符串
- 默认值：无
- 描述:  元素ID, 如: '#slidergroup1'

####scrollEnabled:
- 类型: 布尔
- 默认值: true
- 描述:  是否能够左右滑动

####clickTransition:
- 类型: 布尔
- 默认值: false
- 描述:  点击导航是否带过度动画

####touchTransition:
- 类型: 布尔
- 默认值: true
- 描述:  左右滑动是否带过度动画

###**callback(index)**
ret:
- 类型: 数字
- 默认值: 无
- 描述:  当前索引

###**示例代码**
~~~
// 创建实例, 并保存到一个变量上
var slidergroup1 = sliderGroup({
    id: 'slidergroup1',
    scrollEnabled: false,
    clickTransition: false,
    touchTransition: true
}, function(index) {
    console.log(index);
});

// 设置 div 组当前可见 div
slidergroup1.setSliderGroupIndex({
    index: 2,
    scroll: false,
});
~~~

##**setSliderGroupIndex**
###### 设置 div 组当前可见 div
###### setFrameGroupIndex({params})
###**params**

####index:
- 类型: 数字
- 默认值：无
- 描述:  div 索引

####scroll:
- 类型: 布尔
- 默认值: false (没有动画)
- 描述:  是否平滑滚动至目标窗口，即是否带有动画

###**示例代码**
~~~
// 设置 div 组当前可见 div
slidergroup1.setSliderGroupIndex({
    index: 1,
    scroll: false,
});
~~~

###**标准CSS**
~~~
/*=== slider-group -start- ==*/
/* 遵循BEM规范 */
.slider-group {
    float: left;
    width: 100%;
}

.slider-group__nav {
    position: relative;
    text-align: center;
    float: left;
    width: 100%;
}

.slider-group__nav-item {
    float: left;
}

.slider-group__nav-item_active {
    color: #f35d4a;
}

.slider-group__bar {
    position: absolute;
    height: 2px;
    background-color: #f35d4a;
    bottom: 0;
    transition-timing-function: ease-out;
}

.slider-group__main-wrap {
    float: left;
    width: 100%;
    overflow: hidden;
    opacity: 0;
    -webkit-transition: opacity 0.1s ease-in;
}

.slider-group__main {
    float: left;
    width: 100%;
    min-width: 3500px;
}

.slider-group__main-item {
    float: left;
    position: relative;
    overflow-x: hidden;
    min-height: 1px;
}
/*=== slider-group -end- ==*/
~~~

###**标准HTML**
~~~
<section class="slider-group" id="slidergroup2">
    <div class="slider-group__nav">
        <div class="slider-group__nav-item slider-group__nav-item_active" style="width:50%;height: 40px;line-height: 40px;" data-index="0">店铺顾问</div>
        <div class="slider-group__nav-item" style="width:50%;height: 40px;line-height: 40px;" data-index="1">店铺活动</div>
        <div class="slider-group__bar" style="width:50%;"></div>
    </div>
    <div class="slider-group__main-wrap">
        <wrap class="slider-group__main">
            <item class="slider-group__main-item">
                <div>111</div>
                <div>111</div>
                <div>111</div>
                <div>111</div>
            </item>
            <item class="slider-group__main-item">
                <div>222</div>
                <div>222</div>
                <div>222</div>
            </item>
        </wrap>
    </div>
</section>
~~~

##**IScrollSimple**
###### 创建div窗口组的实例
###### IScrollSimple('string', callback(index))
###**params**

####selector:
- 类型: 字符串 || 标签
- 默认值：无
- 描述:  选择器, 如: '#IScrollSimple', document.getElementById('IScrollSimple')

####indicators:
ret:
- 类型: JSON 对象
- 内部字段：
~~~
{
    el: true          //字符串 || 标签；如: '#dotty', '.dotty', document.getElementById('dotty')
}
~~~
###**callback(index)**
ret:
- 类型: 数字
- 默认值: 无
- 描述:  当前索引

###**示例代码**
~~~
// 创建实例, 并保存到一个变量上
var slidergroup1 = sliderGroup({
    id: 'slidergroup1',
    scrollEnabled: false,
    clickTransition: false,
    touchTransition: true
}, function(index) {
    console.log(index);
});

// 设置 div 组当前可见 div
slidergroup1.setSliderGroupIndex({
    index: 2,
    scroll: false,
});
~~~

##**goToPage**
###### 设置 div 组当前可见 div
###### goToPage(index, scroll)
###**params**

####index:
- 类型: 数字
- 默认值：无
- 描述:  div 索引

####scroll:
- 类型: 布尔
- 默认值: false (没有动画)
- 描述:  是否平滑滚动至目标窗口，即是否带有动画

###**示例代码**
~~~
// 设置 div 组当前可见 div
IScroll.goToPage(1, false);
~~~

###**标准CSS**
~~~
/*=== slider-group -start- ==*/
/* 遵循BEM规范 */
.slider-group {
    float: left;
    width: 100%;
}

.slider-group__nav {
    position: relative;
    text-align: center;
    float: left;
    width: 100%;
}

.slider-group__nav-item {
    float: left;
}

.slider-group__nav-item_active {
    color: #f35d4a;
}

.slider-group__bar {
    position: absolute;
    height: 2px;
    background-color: #f35d4a;
    bottom: 0;
    transition-timing-function: ease-out;
}

.slider-group__main-wrap {
    float: left;
    width: 100%;
    overflow: hidden;
    opacity: 0;
    -webkit-transition: opacity 0.1s ease-in;
}

.slider-group__main {
    float: left;
    width: 100%;
    min-width: 3500px;
}

.slider-group__main-item {
    float: left;
    position: relative;
    overflow-x: hidden;
    min-height: 1px;
}
/*=== slider-group -end- ==*/
~~~

###**标准HTML**
~~~
<section class="slider-group" id="slidergroup2">
    <div class="slider-group__nav">
        <div class="slider-group__nav-item slider-group__nav-item_active" style="width:50%;height: 40px;line-height: 40px;" data-index="0">店铺顾问</div>
        <div class="slider-group__nav-item" style="width:50%;height: 40px;line-height: 40px;" data-index="1">店铺活动</div>
        <div class="slider-group__bar" style="width:50%;"></div>
    </div>
    <div class="slider-group__main-wrap">
        <wrap class="slider-group__main">
            <item class="slider-group__main-item">
                <div>111</div>
                <div>111</div>
                <div>111</div>
                <div>111</div>
            </item>
            <item class="slider-group__main-item">
                <div>222</div>
                <div>222</div>
                <div>222</div>
            </item>
        </wrap>
    </div>
</section>
~~~

##**懒加载**
###### 基于echo.js修改, echo-taichiyi.js

### **示例代码**
~~~
echo_taichiyi({
    unload: true, // 再次出现在视野内是否再次加载
    throttle: 0, // 延迟多少秒显示
    // offset: 0, // 提前多少距离显示
    errorImage: '../img/gaugin.jpg' // 图片加载失败时, 作为替换的图片
}, function(element, type) {
	// element: 元素
	// type: 1.load(进入视野)
    			 2.unload(淡出视野)
});

~~~

##**下拉刷新**
###### 基于aui-pull-refresh-2.js修改, pull-refresh-a.js

## **pullToRefreshA({params})**
### **params**
#### container
- 类型: 元素(标签)
- 默认值：无
- 描述:  元素, 如: document.querySelector('.gazer-content')

#### pullImage
- 类型: 字符串
- 默认值：无
- 描述:  下拉时显示的图片，带旋转

#### loadingImage
- 类型: 字符串
- 默认值：无
- 描述:  加载中的图片

#### callback
- 类型: 函数
- 默认值：function(){}
- 描述:  回调函数

### **标准css**
~~~
.aui-load-wrap {
    width: 2.2em;
    height: 2.2em;
    border: 1px solid #dddddd;
    background: #ffffff;
    border-radius: 1.1em;
    position: absolute;
    left: 50%;
    top: 0;
    margin-left: -1.1em;
    z-index: 999;
    -webkit-transform: translate3d(0, -100%, 0);
    transform: translate3d(0, -100%, 0);
}

.aui-load-wrap img {
    width: 100%;
    display: inline-block;
    -webkit-transform: rotate(0);
    transform: rotate(0);
    -webkit-transform: translateZ(0);
    transform: translateZ(0);
}

.aui-load-wrap .aui-loading {
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;
    display: inline-block;
    -webkit-animation: rotate .8s linear 0s infinite;
    animation: rotate .8s linear 0s infinite;
}

@-webkit-keyframes rotate {
    0% {
        -webkit-transform: rotate(0deg) scale(1);
        transform: rotate(0deg) scale(1);
    }
    50% {
        -webkit-transform: rotate(180deg) scale(1);
        transform: rotate(180deg) scale(1);
    }
    100% {
        -webkit-transform: rotate(360deg) scale(1);
        transform: rotate(360deg) scale(1);
    }
}

@keyframes rotate {
    0% {
        -webkit-transform: rotate(0deg) scale(1);
        transform: rotate(0deg) scale(1);
    }
    50% {
        -webkit-transform: rotate(180deg) scale(1);
        transform: rotate(180deg) scale(1);
    }
    100% {
        -webkit-transform: rotate(360deg) scale(1);
        transform: rotate(360deg) scale(1);
    }
}

~~~
### **示例代码**
~~~
var loadingCallback = function(status) {
    if (status == 'success') {
        window.setTimeout(function() {
            // TODO
            pullRefresh.cancelLoading(); //刷新成功后调用此方法隐藏
        }, 1400)
    }
}
var pullRefresh = new pullToRefreshA({
    container: document.querySelector('.gazer-content'),
    // "pullImage": "../img/pull_refresh.png", //下拉时显示的图片，带旋转
    // "loadingImage": "../img/pull_refresh_2.png", //加载中的图片
    "callback": loadingCallback //刷新回调
});

~~~
