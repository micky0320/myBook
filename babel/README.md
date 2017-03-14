本节内容概述
安装必要的插件
创建入口文件并执行
安装必要的插件
运行
```
npm i babel-core babel-plugin-transform-runtime babel-preset-es2015 babel-preset-stage-3 babel-runtime --save
```
安装一堆需要的插件。
然后在项目根目录创建```.babelrc```文件，文件内容编写为
```javascript
{
  "presets": ["stage-3", "es2015"],
  "plugins": ["transform-runtime"]
}
```
创建入口文件并执行
假如你编写es6的代码文件是test.js，那么你需要创建另一个文件，例如test-entry.js作为入口文件。入口文件内容编写为

```javascript
require("babel-core/register");
require("./test.js");
```

然后直接运行```node test-entry.js```就可以了