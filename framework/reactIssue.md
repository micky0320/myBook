# 本文为react的一些问题及相关处理方式



## react自定义属性的修复办法

react 默认是不支持自定义属性的写法的，如：'otitle';
以前用来处理webtrends是用'data-'的方式先将自定义属性标记上，再通过replaceAttr给react的Dom写上对应属性。

后来有同事分享，表示如果在类上加上'is'，就可以让react识别到自定义属性，写法如下；
<div
	is
	otitle="我是自定义属性"
></div>


## 

