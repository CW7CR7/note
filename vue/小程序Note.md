# 小程序Note

首先去微信公众平台下载微信开发者工具

登录该开发工具时候需要用自己的手机微信进行扫一扫

#### 微信小程序实时更新 设置方式：

<img src="imgs\微信小程序实时更新 Snipaste_2021-04-23_14-08-22.jpg" style="zoom:50%;" />

创建时候的项目名称是项目在本地时候的名字，而不是项目上线在微信小程序时候的样子

## 我的APPID和秘钥

```html
小程序ID
wxbfc9cd7f2d1f14c8

秘钥
b6fd170443e8fbc37c25c980e8164c71
小程序账号：sc52292@163.com
```

微信开发者工具的内核是vscode的内核

小程序刚发布的时候，压缩包大小不能大于1M。17年4月之后，放宽到2M

17.1.9小程序上线

常规的小程序1-2周即可开发完成

#### DPR

就是设备像素比，物理像素/设备独立像素的值

比如iphone6的dpr就是2

## viewport移动端适配

手机厂商生产手机的时候大部分手机默认页面宽度为980px。但是实际上呢，手机视口宽度都小于980px，比如iphone678就是375px

```html
<meta name="viewport" content="width=device-width,initial-scale=1.0">
    
</meta>
width=device-width代表的意思就是
width就是布局视口，device-width就是视觉视口。视觉视口此时就是375px
initial-scale=1.0 意思就是缩放比是1:1
```



#### 小程序下载地址

[小程序开发工具下载地址](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)

#### rem适配

root em的意思

#### rem实现步骤 底层js:

```js
function remRefresh(){
    let clientWidth=document.documentElement.clientWidth;
#    屏幕等分10份
    let rem=clientWidth/10;
    document.documentElement.style.fontSize=rem+'px'
    document.body.style.fontSize='12px'
}
window.addEventListener('pageshow',()=>{
    remRefresh()
}) 
#防抖
let timeoutID
window.addEventListener('resize',()=>{
    timeoutID&&clearTimeout(timeoutID)
    timeoutID=setTimeout(()=>{
        remRefresh()
    },500)
})
```



### 这里我们延伸一下防抖节流

防抖：通过使用定时器的方式，把一段时间内的多次触发变成一次触发。不抖了，就是射一次

节流：减少一段时间的触发频率



#### 小程序的特点

1. 小程序是没有DOM的
2. 小程序的json文件大部分都是配置文件
3. 小程序的是陪单位是rpx (responsive pixel)响应式像素单位。比如iphone6的屏幕是375px，那么1px=2rpx。不管任何设备都是750rpx

如果没有自己的服务器，那么可以使用小程序提供的云开发

#### 预览

微信IDE的上方有一个预览，点击。有一个扫描二维码预览。这里如果没有设置的话，只有自己的账号可以预览。如果想让小伙伴们也可以预览，就要进入小程序的后台首页。找到左侧侧边栏的 管理=>成员管理=>项目成员&体验成员。

当然，也可以不选择扫描二维码预览，而是选择自动预览。自动预览更加的方便。自动预览只能是我们自己这个开发人员

#### 真机调试

有时候，模拟器并不准确，这个时候就必须用真机调试

写完了项目要先上传

#### 配置文件project.config.json

#### 是否允许被爬虫

sitemap.json如果没有，则默认所有页面都允许被索引。

sitemap.json:

```json
{
  "desc": "这个是carlos的",
  "rules": [{
    "action": "allow",
    "page": "*"
  }]
}
```

必须要有app.js这个文件

app.json里面的颜色不能写red这种格式，必须16进制的

小程序会先加载pages数组的第一项路径的网页，当然也可以通过entryPagePath来新增人为规定小程序加载的首页

一个页面的文件夹下面一般有wxml,json,wxss,js这四个文件

#### 标签

div->view

img->image



只能用class不能用id

Page（）

注册当前页面的实例

### git第一次项目添加仓库

1.git init（第一次提交代码）
2.git add .
3.git commit -m "提交说明"
4.git remote add origin 库的地址
5.git push -u origin master