Node.js 提供了 http 模块，http 模块主要用于搭建 HTTP 服务端和客户端，使用 HTTP 服务器或客户端功能必须调用 http 模块，代码如下：
```javascript
var http = require('http');
```
在通常的服务器中，数据流通的方式是客户先通过浏览器进行发送请求，服务器在项目中进行查找，然后进客户所需要的页面进行返回，在查找的过程中可能存在两种情况，就是存在和不存在，当然，我们会做出判断，下面就是简单的服务器实现过程：
#### 1、编写服务器代码server.js
```javascript
var http=require('http');
var fs = require('fs');
var url = require('url');

//创建服务器
http.createServer(function(request,response) {
    //解析请求，包括文件名
    var pathname= url.parse(request.url).pathname;
    //输出请求的文件名
    console.log("Request for "+ pathname + "  received.");

    //从文件系统中都去请求的文件内容
    fs.readFile(pathname.substr(1),function(err, data) {
        if(err) {
            console.log(err);
            //HTTP 状态码 404 ： NOT FOUND
            //Content Type:text/plain
            response.writeHead(404,{'Content-Type': 'text/html'});
        }
        else {
            //HTTP 状态码 200 ： OK
            //Content Type:text/plain
            response.writeHead(200,{'Content-Type': 'text/html'});

            //写会相应内容
            response.write(data.toString());
        }
        //发送响应数据
        response.end();
    });
}).listen(8081);

console.log('Server running at http://127.0.0.1:8081/');
```
通过上面代码，我们就能够实现服务器对于文件的查找，下面，我们就进行创建一个html文件，然后通过浏览器进行访问
#### 2、编写html文件（index.html），用于浏览器进行请求
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>index</title>
</head>
<body>
   这是一个用于进行nodejs服务器测试的html文件，我们能够通过在浏览器上面输入
   http://127.0.0.1:8081/WebServer/index.html进行访问
</body>
</html>
```
创建完之后，我们进行测试，现在我的目录结构是这样的：


#### 3、进行测试
    (1) 首先我们启动服务器，使用命令node WebServer/server.js
    (2) 在浏览器进行访问，在url栏中输入http://127.0.0.1:8081/WebServer/index.html
其显示效果如下所示：
![图片未找到](http://img.blog.csdn.net/20170604165545657?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvc3V3dTE1MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

当然，我们也能够通过访问通过http://127.0.0.1:8081/LoveYou.html访问server.js文件夹外边的文件

