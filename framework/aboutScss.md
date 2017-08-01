关于react框架使用scss的绕坑指南

tip:react配合scss的情况下出现的

以前使用的预处理器都是用less，今天新起一个项目，使用到scss的一些用法@mixin,@function时，写着写着刚感觉很爽的时候，然后页面就报红了.很尴尬!!


发现页面的jsx中引入less都可以正常使用，

```javascript
import '../style/xxx.less'
```

 经过反复验证发现，当scss书写到一定量时，只要变更了scss的内容，就会页面报错，无法进行下去。
 目测看上去像是热加载加载完毕了，scss的编绎未完成，导致页面的样式没能成功加载。

 对照了以前的过来人写过的项目，发现，原来人家是这样写的
 方法一：
```javascript
 import classes from './index.scss'
```
```jsx
<div className={classes.tip}></div>
```
感觉很麻烦〜，以前用less就没有这种烦恼，但是scss是真的好用，谁用谁知道〜虽然很早就知道postcss,stylus,但是没时间弄（主要是懒〜我也很无奈啊，扯远了，收〜）


方法二：
在main.scss中引入页面的scss文件，main.scss直接被layout引用，因为每个页面都用使用layout，这样优先加载完样式，然后通过路由去访问页面时，不会影响渲染。


