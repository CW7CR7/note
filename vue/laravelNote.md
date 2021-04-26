## 文件的上传

```php
可以放在请求后，查看上传的文件
dd($_FILES);
文件内容：
"userImg" => array:5 [▼
    "name" => "phpstudy伪静态位置.png"
    "type" => "image/png"
    "tmp_name" => "C:\Users\chenyanan\AppData\Local\Temp\phpD9A9.tmp"
    "error" => 0（0-7的值，但是没有5）
    "size" => 206237
  ]
if($request->hasFile('photo')){}
$request->hasFile('photo')和$request->photo等价
```



photo是input的name名字。$request->hasFile('photo')的状态码0-7，但是没有5

获取文件路径和扩展名：

```php
$path=$request->photo->path();
$extension=$request->photo->extension();
```

```php
$uri=$request->path();//后缀名：addQuickly/81
```

```php
处理表单数组输入时，可以使用”.”来访问数组输入：

也就是说没传值的话，用sally作为默认值传递
$name = $request->input('name', 'Sally');


```

**BUG:文件上传打印$_FILES值为空原因,上传不上去的原因**

解决方法：1)查看form中是否添加enctype="multipart/form-data";

​        2)查看input标签是否添加name属性 

​        3)正确格式        

```html
<form action="upload.php" method="post" enctype="multipart/form-data">
 
文件上传:<input type="file" name='file'>
 
         <button type="submit">上传</button>
 
</form>
```



```php
 if (Input::method() == 'POST') {
            // dd($_FILES);
            $path = $request->userImg->path();
            $extension = $request->userImg->extension();
            // dd($path);//C:\Users\chenyanan\AppData\Local\Temp\php3A27.tmp
            dd($extension); //png
        }
```

**文件路径问题需要注意：**

如果是php路径加./，如果是浏览器则是/



#### unlink（）

1、函数的定义
unlink() 函数用于删除文件。若成功，则返回 true，失败则返回false.

//删除文件
  $to_link = 'C:\Users\Administrator\Desktop\cut.jpg';
   @unlink($to_link);

2、@unlink()

有时候会看到用@unlink()来删除文件。这个@是php中的错误抑制符。比如当你要删除不存在的文件，正常使用unlink()是要报错的。但是使用@unlink() 的话，则不会报错。

3、@错误抑制符

@是可以屏蔽函数执行过程中遇到问题而产生的一些错误、警告信息，这样用户就看不到程序的出错信息。这样除了用户界面会友好一些外，更重要的是安全性，因为屏蔽了出错文件的路径等信息。



#### post请求

```php
protected function form(Request $request, $id)
    {
        $input = $request->all();
userImg是视图层input的name键值
        $thisImg=$request->Input('userImg');
}
```

#### substr()截取指定的字符串前面或者后面的内容

```php
$AAA = '123_45678';
$result = substr($AAA, 0, strrpos($AAA, "_"));
// echo $result;//输出123
$AAA = '123_45678';
$result = substr($AAA, strripos($AAA, "_") + 1);
echo $result; //输出45678
```

#### php substr()截取字符串

```
substr(string,start,length)
参数：string
就是要截取的字符串

参数：start
必需。规定在字符串的何处开始。
正数 - 在字符串的指定位置开始
负数 - 在从字符串结尾开始的指定位置开始
0 - 在字符串中的第一个字符处开始

参数：length
可选。规定被返回字符串的长度。默认是直到字符串的结尾。也就是说不写就是截取到结尾
正数 - 从 start 参数所在的位置返回的长度
负数 - 从字符串末端返回的长度
```

#### 提交的文件保存的方法move

```php
$request->userImg->move('../../4dmodels/tp5/public/', '22' . '.' . $extension);
```

多个提交图片的input框

```php+HTML
@extends('parent')
<!-- 继承开始 -->
@section('mainbody')
<!-- <link rel="stylesheet" href="../../public/css/add.css"> -->
<link rel="stylesheet" href="{{ asset('css/addQuickly.css') }}" />
<link rel="stylesheet" href="{{ asset('layui/css/layui.css') }}" />
<div class="dil"></div>
<div class="main-container">
    <div class="main_wrap" id="pic_wrap">
        <div class="row" style="margin-bottom: 20px">
            <div class="col-md-3">
                <h4 class="title1">操作指南</h4>
            </div>
            <div class="col-md-9 resourcesList clearfix">
                <div class="title1">资源列表</div>
                <button class="packThenUploadBtn">打包上传</button>
                <button class="packThenDownloadBtn">打包下载</button>
            </div>
            <div class="col-md-3 leftWrap">
                <div class="leftGuide">
                    <div class="titleOfLeftGuide">第一步：下载资源源文件</div>
                    <div class="contentOfLeftGuide">
                        点击<span class="packThenDownloadBtn">打包下载</span
                        >可下载该场馆所有资源源文件，耗时较长，请耐心等待
                    </div>
                    <div class="titleOfLeftGuide">第二步：编辑资源源文件</div>
                    <div class="contentOfLeftGuide">
                        编辑保存文件时，<span>文件名称不可改</span>;<span>.psd文件请另存为.png格式文件再上传</span>。
                    </div>
                    <div class="titleOfLeftGuide">第三步：上传替换资源文件</div>
                    <div class="contentOfLeftGuide">
                        上传完资源，请点击<span class="subBtn">提交</span
                        >，系统自动进行场馆资源替换。
                    </div>
                </div>
            </div>
            <div class="col-md-9 rightWrap clearfix">
                <div class="item">
                    <!-- 提交的盒子 -->
                    <form
                        action="{{url('addQuickly/'.$thisScene->id)}}"
                        method="POST"
                        enctype="multipart/form-data"
                    >
                        <!-- 1.场馆logo -->
                        <div class="item-content">
                            <div class="pull-left">
                                <img id="logo-img" style=' border: 1px solid
                                #999; display: block; width: 60px; height:
                                60px;' src={{asset('tp5/public/images/images'.$thisScene->sceneNum.'/序.png')}}
                                width="60" height="60" class="img-rounded"/>
                                <!-- onclick="chooseImageFile('thisImg')" -->

                                <input
                                    type="file"
                                    name="userImg"
                                    id="logo-img-input"
                                    hidden="true"
                                    accept="image/*"
                                    class="img-input"
                                />
                                <!-- onchange="showImgToView('thisImg')" -->
                                <!-- 模板ID -->
                                <input
                                    name="thisSceneID"
                                    type="number"
                                    hidden="true"
                                    value="{{$thisScene->id}}"
                                />
                            </div>
                            <div class="pull-left works_intro">
                                <p>场馆logo</p>
                                <p>图片资源</p>
                            </div>
                            <div class="pull-right works_edit">
                                <span
                                    ><a
                                        href="{{url('addQuickly/'.$thisScene->id)}}"
                                        target="_self"
                                        >快速建馆</a
                                    ></span
                                >|
                                <span
                                    ><a
                                        href="{{url('tp5/showProPC.html?m='.$thisScene->sceneNum)}}"
                                        target="_blank"
                                        >查看</a
                                    ></span
                                >
                            </div>
                        </div>
                        <!-- 2.场馆介绍 -->
                        <div class="item-content">
                            <div class="pull-left">
                                <img style=' border: 1px solid
                                #999; display: block; width: 60px; height:
                                60px;' src={{asset('tp5/public/images/images'.$thisScene->sceneNum.'/党建成果图片.png')}}
                                width="60" height="60" class="img-rounded"/>
                                <!-- onclick="chooseImageFile('thisImg')" -->
                                <input
                                    type="file"
                                    name="introduceImg"
                                    id="introduce-img-input"
                                    class="img-input"
                                    hidden="true"
                                    accept="image/*"
                                />

                            </div>
                            <div class="pull-left works_intro">
                                <p>场馆logo</p>
                                <p>图片资源</p>
                            </div>
                            <div class="pull-right works_edit">
                                <span
                                    ><a
                                        href="{{url('addQuickly/'.$thisScene->id)}}"
                                        target="_self"
                                        >快速建馆</a
                                    ></span
                                >|
                                <span
                                    ><a
                                        href="{{url('tp5/showProPC.html?m='.$thisScene->sceneNum)}}"
                                        target="_blank"
                                        >查看</a
                                    ></span
                                >
                            </div>
                        </div>
                        <!-- 3.荣誉墙 -->
                        <div class="item-content">
                            <div class="pull-left">
                                <img style=' border: 1px solid
                                #999; display: block; width: 60px; height:
                                60px;' src={{asset('tp5/public/images/images'.$thisScene->sceneNum.'/荣誉墙.png')}}
                                width="60" height="60" class="img-rounded"/>
                                <!-- onclick="chooseImageFile('thisImg')" -->
                                <input
                                    type="file"
                                    name="honor-wall"
                                    id="honor-wall-img-input"
                                    class="img-input"
                                    hidden="true"
                                    accept="image/*"
                                />

                            </div>
                            <div class="pull-left works_intro">
                                <p>场馆logo</p>
                                <p>图片资源</p>
                            </div>
                            <div class="pull-right works_edit">
                                <span
                                    ><a
                                        href="{{url('addQuickly/'.$thisScene->id)}}"
                                        target="_self"
                                        >快速建馆</a
                                    ></span
                                >|
                                <span
                                    ><a
                                        href="{{url('tp5/showProPC.html?m='.$thisScene->sceneNum)}}"
                                        target="_blank"
                                        >查看</a
                                    ></span
                                >
                            </div>
                        </div>
                        <!-- token -->
                        {{ csrf_field() }}
                        <input
                            type="submit"
                            value="立即提交"
                            class="layui-btn layui-btn-danger"
                            id="immediately"
                        />
                    </form>
                </div>
            </div>
        </div>
    </div>
</div>
<script src="{{ asset('js/jquery-1.9.1.js') }}"></script>
<script src="{{ asset('layui/layui.js') }}"></script>
<script>
    // 图片点击
    $(".img-rounded").click(function (e) {
        var thisInput = $(e.target).siblings("input")[0];
        // 手动调用
        $("#" + thisInput.id).click();
        // 调用showImgToView方法
        $("#" + thisInput.id).change(function (e) {
            console.log(e.target.id);
            var index = $(".img-input").index(this);
            console.log(index, "index");
            showImgToView(e.target.id, index);
        });
    });

    //2、创建FileReader对象
    var fileReader0 = new FileReader();
    var fileReader1 = new FileReader();
    var fileReader2 = new FileReader();
    var fileReader3 = new FileReader();
    //正在判断是否符合图片类型
    regexImageFile = /^(?:image\/bmp|image\/cis\-cod|image\/gif|image\/ief|image\/jpeg|image\/jpeg|image\/jpeg|image\/pipeg|image\/png|image\/svg\+xml|image\/tiff|image\/x\-cmu\-raster|image\/x\-cmx|image\/x\-icon|image\/x\-portable\-anymap|image\/x\-portable\-bitmap|image\/x\-portable\-graymap|image\/x\-portable\-pixmap|image\/x\-rgb|image\/x\-xbitmap|image\/x\-xpixmap|image\/x\-xwindowdump)$/i;
    //3、利用改变事件将图片显示出来 input-file ID
    function showImgToView(inputFileId, ind) {
        //选择图片文件
        var imgFile = $("#" + inputFileId).get(0).files[0];

        //判断上传文件是否为图片格式
        if (!regexImageFile.test(imgFile.type)) {
            return;
        } else {
            console.log("fileReader" + "" + ind);
            eval("fileReader" + "" + ind).readAsDataURL(imgFile);
        }
    }
    /* fileReader1.onload = function (evt) {
        //将该URL绑定到img标签的src属性上，就可以实现图片的上传预览效果
        console.log($(".img-rounded")[1]);
        console.log(evt.target);
        $(".img-rounded").eq(1).attr("src", evt.target.result);
    }; */
    //4、读取文件
    $(".img-rounded").each((index, item) => {
        console.log(eval("fileReader" + index));
        eval("fileReader" + index).onload = (e) => {
            console.log(e.target);
            $(".img-rounded").eq(index).attr("src", e.target.result);
        };
    });
</script>
@endsection
<!-- 继承结束 -->

```





### ajax异步响应

比如Return view这种就是属于传统直接响应

其他有两种响应方式：

1. ajax响应

   ```
   ajax常见响应类型：JSon，xml,text/html。不会直接返回数组，一般都会json格式化
   ```

   

2. 重定向（跳转）



laravel中return布尔值是不允许的



遇到的BUG：

注意：一定要设置：type=“button”，否则会默认为：type=“submit”,请求完成后会进行页面重定向，进行页面刷新



#### location.search

location.search是从当前URL的?号开始的字符串 
如:http://www.51js.com/viewthread.php?tid=234

它的search就是?tid=4324

#### js中的substring()

参数     描述：
start     必需。一个非负的整数，规定要提取的子串的第一个字符在 stringObject 中的位置。
end      可选。一个非负的整数，比要提取的子串的最后一个字符在 stringObject 中的位置多 1。如果省略该参数，那么返回的子串会一直到字符串的结尾。

返回值：
一个新的字符串，该字符串值包含 stringObject 的一个子字符串，其内容是从 start 处到 end-1 处的所有字符，其长度为end减 start。

substring 方法返回的子串包括 start 处的字符，但不包括 end 处的字符。
如果 start 与 end 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）。
如果 start 比 end 大，那么该方法在提取子串之前会先交换这两个参数。
如果 start 或 end 为负数，那么它将被替换为 0。

1. substring的第二个参数是下标
2. substr的第二个参数是长度



ajax响应回请求 返回数据：

```php
public function test2(){
        $courses = DB::table('courses');
        $courses = $courses->get();
        return response()->json($courses);
    }
返回多个数据：
    public function test2(){
        $courses = DB::table('courses');
        $courses = $courses->get();
        $num = $courses->count();
        return response()->json(['course'=>$courses,'num'=>$num]);
    }
```

遇到的BUG：POST提交ajax请求产生了419错误：解决方法：

```js
$("#btn").click(function () {
            console.log(1);
            $.post('/test2',{
                '_token':'{{csrf_token()}}'
            },data=>{
                console.log(data);
            })
        });
```



# laravel-admin

第一步：

```
php artisan admin:make ViewController --model=App\Models\View
```

然后会提示：

Add the following route to app/Admin/routes.php:

  $router->resource('views', ViewController::class);