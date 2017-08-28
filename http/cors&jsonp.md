cors与jsonp的区别

1.请求方式的区别
cors跨域是一种新型的跨域方式，支持`get/post/option`等方式请求，
jsonp只支持get方式请求，

2.获取的数据类型
cors是json，内容是数据
jsonp是jsonp的数据类型，由两部分组成，回调函数和数据；

3.ajax配置的不同
cors跨域配置，然后需要让服务端支持，加上允许某域的某接口的配置，这样就可以实现跨域通信。
```
xhrFields: {
    withCredentials: true
},
crossDomain: true,
```


