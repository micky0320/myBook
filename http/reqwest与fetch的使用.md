# reqwest、fetch的使用
项目中使用ajax(此处是指jq封装的ajax，后面不作赘述)和reqwest比较多，就想简单整理一下

Ajax的使用大家可以去查API，文档很详细了；

## reqwest的使用
很多人看到reqwest，第一感觉就是：“哎，哥们你写错了吧，应该是request吧。” 额，表示很伤〜真的没写错.

reqwest的全用，官方npm包说的很直白。


> It's AJAX
> All over again. Includes support for xmlHttpRequest, JSONP, CORS, and CommonJS Promises A.


普通的reqwest写法跟ajax大抵差不多，像下面这样：
```javascript
// 普通请求
reqwest({
    url: 'path/to/json'
  , type: 'json'
  , method: 'post'
  , data: { foo: 'bar', baz: 100 }       // 入参
  , error: function (err) { }
  , success: function (resp) {
      qwery('#content').html(resp.content)
    }
})

// jsonp请求
reqwest({
    url: 'path/to/json'
  , type: 'jsonp'
  , method: 'get'						// jsonp请求,method可不写，写成post，依然会被浏览器默认为get
  , error: function (err) { }
  , success: function (resp) {
      qwery('#content').html(resp.content)
    }
})

// cors请求
reqwest({
    url: 'path/to/json'
  , type: 'json'
  , method: 'post'
  , contentType: 'application/x-www-form-urlencoded'
  , crossOrigin: true					// cors跨域，服务端与客户端存在cookie等数据凭证交互时需要设置crossOrigin，withCredentials
  , withCredentials: true
  , error: function (err) { }
  , success: function (resp) {
      qwery('#content').html(resp.content)
    }
})

// promise写法
reqwest({
    url: 'path/to/data.jsonp?foo=bar'
  , type: 'jsonp'
  , jsonpCallback: 'foo'
})
  .then(function (resp) {
    qwery('#content').html(resp.content)
  }, function (err, msg) {
    qwery('#errors').html(msg)
  })
  .always(function (resp) {
    qwery('#hide-this').hide()
  })
```


## fetch的使用

```
// 请求html 
fetch('/users.html')
  .then(function(response) {
    return response.text()				// 将内容将化成字符串类型数据
  }).then(function(body) {
    document.body.innerHTML = body
  })

// 提交json数据
fetch('/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({        		// fetch的入参数据跟reqwest的data不太一样，是body
    name: 'Hubot',
    login: 'hubot',
  })
})

// cors请求
fetch('https://example.com:1234/users', {
  mode: "cors",							// 设置为支持跨域请求
  credentials: 'include'				// 设置允许发送相关凭证
})

fetch的mode配置项有3个值，如下：

same-origin：该模式是不允许跨域的，它需要遵守同源策略，否则浏览器会返回一个error告知不能跨域；
其对应的response type为basic。

cors: 该模式支持跨域请求，顾名思义它是以CORS的形式跨域；当然该模式也可以同域请求不需要后端额外的CORS支持；
其对应的response type为cors。

no-cors: 该模式用于跨域请求但是服务器不带CORS响应头，也就是服务端不支持CORS；这也是fetch的特殊跨域请求方式；
其对应的response type为opaque


// fetch不支持jsonp，那么需要叫上他的兄弟fetchJsonp
fetchJsonp('/users.jsonp')
  .then(function(response) {
    return response.json()
  }).then(function(json) {
    console.log('parsed json', json)
  }).catch(function(ex) {
    console.log('parsing failed', ex)
  })
```
---------------------------------------
***
