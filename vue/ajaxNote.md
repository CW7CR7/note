$.get({四个参数})



1. url:等待载入的页面的url地址
2. data：等待发送的key/value参数
3. success：载入成功时候的回调函数
4. dataType：返回内容格式，xml,json,script,text,html

$.post({四个参数})

$.getJSON({四个参数})



通用的写法：$.ajax({很多参数})

1. url:请求地址
2. type：GET/POST(jQuery1.9.0之后是method)
3. data:要发送的数据
4. async:是否异步