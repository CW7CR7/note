# 移动端适配Note以及UI慕客切图

UI切图一般用蓝湖或者慕客，蓝湖10人以上收费，慕客100人以上收费。打了错别字，应该是

[慕客地址](https://www.mockplus.cn/idoc?home=1)

进入首页下载PS插件，然后双击下载好的插件，然后打开PS

慕客在PS中的位置:

<img src="imgs\慕客在PS中的位置Snipaste_2021-04-20_14-52-04.jpg" style="zoom:67%;" />



如果要使用这个插件，必须要注册慕客账号，并且PS不能是绿色版的。慕客比CutMan更强大。点击切图上面的文字，即可在右边的窗口复制文字

### 实现移动端适配的几种方式

1. flex布局
2. 百分比布局
3. rem布局
4. vw/vh布局
5. 响应式布局

和vue适配比较好的vantUI就是flex+rem+flexble.js



首先定义页面最小宽度和最大宽度，设置为320-750px

设置主体内容为margin:0 auto;

引用线上CDN flexible.js

<script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.2/??flexible_css.js,flexible.js"
></script>

### VSCODE更换主体注释颜色

配置文件路径：C:\Users\chenyanan\.vscode\extensions\uloco.theme-bluloco-dark-3.3.4\themes

找到name为comments的一个对象，修改其颜色，即可完成注释颜色修改

```json
{
      "name": "Comments",
      "scope": [
        "comment",
        "punctuation.definition.comment",
        "comment.block.documentation punctuation.definition",
        "string.comment",
        "comment.block.documentation",
        "comment.block"
      ],
      "settings": {
        // 修改注释颜色
        // "foreground": "#636d83"
        "foreground": "#2a9257"
      }
    },
```

vscode默认皮肤深绿色:#638f4e

#### 屏幕大小大于750px给他一个约束

```css
body{
    min-width: 320px;
    max-width: 750px;
    margin: 0 auto;
}
// 屏幕大于750px时候,html字体大小就不变化了
@media screen and (min-width:750px){
    html{
        font-size: 37.5px  !important;
    }
}
```

flexible.js把页面平均分成了10等分，iphone678都是375px所以上面的字体设置为37.5比较合适

## rem适配

#### vscode下载插件：px to rem&rpx(cssrem)

此插件的设置：调整默认字体大小。比如图上面是16就代表1rem=16px

<img src="imgs\cssrem插件默认字体大小Snipaste_2021-04-20_16-36-20.jpg" style="zoom:50%;" />

然后再在css页面里面输入px就可以让你手动选择转换为对应的rem

#### flex布局竖向为主轴

```html
display:flex;
flex-direction:column;
align-items:center;
justify-content这个代表主轴方向
```

#### 去除a标签的默认样式

```css
text-decoration:none;
```

#### 选择前面三个选择器：

```csss
:nth-type-of(-n+3)
```

平时可以多用用header nav标签

#### swiper下载地址

[swiper地址](https://www.swiper.com.cn/download/index.html)

然后把整个包解压到项目里，进入项目的package文件夹里面，复制css和js文件到自己的项目文件夹下面，引入这两个就可以使用

#### opacity透明度

#### 适配iphoneXR可以用火狐浏览器

<img src="imgs\火狐浏览器控制台Snipaste_2021-04-23_16-02-58.jpg" style="zoom:50%;" />