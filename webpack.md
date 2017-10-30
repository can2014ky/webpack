### webpack简介

是一款模块加载兼打包工具

支持AMD/CMD语法

处理依赖关系，然后解析出模块之间的依赖，将代码打包;

将各种资源都作为模块来使用和处理，如: js css less sass等;

```
可以把SASS文件的写法转换成CSS，而不在使用其他转换工具。
可以把ES6或者ES7的代码，转换成大多浏览器兼容的JS代码。
可以把React中的JSX转换成JavaScript代码。
```



### node安装

```
https://nodejs.org/en/
```



### npm

```
nodejs包管理和分发工具
http://npmjs.org/
```



### npm 常用命令

```
npm init 创建package.json文件;
npm install <module-name>  -g/--save-dev/--save  安装模块
npm update <module-name>    更新模块
npm uninstall <module-name> 卸载模块
```



### 安装淘宝镜像

```
 npm install -g cnpm --registry=https://registry.npm.taobao.org
```



http://webpack.github.io/

```
安装webpack
cnpm install webpack -g
安装后就可以在命令行中使用webpack的命令;
把依赖写入package.json
cnpm install webpack --save-dev
```



### cnpm初始化

````
>cnpm init  生成 package.json文件
````



### webpack安装

```
cnpm install  -g  webpack        //全局安装
cnpm install --save-dev webpack  // 本地安装

[webpack.config.js]  类似于 gulpfile.js 负责配置文件;
[main.js]
[index.html]
```



### webpack打包

```
>webpack ./main.js  ./build/build.js   // 打包命令
```



### webpack配置

````
[webpack.config.js] 
module.exports={
    entry:"./src/main.js",
    output:{
        filename:"./dist/bundle.js"
    }
}
````



### css打包

```
[main.js]
require("./app.css");
document.write("hello webpack");

[app.css]
body{ background:pink;}

[webpack.config.js]
module:{
    loaders:[
        {test:/\.css$/,loader:"style-loader!css-loader"}
    ]
}

> cnpm install css-loader style-loader --save-dev
```



### 图片打包

```
[main.js]
var img = document.createElement("img");
img.src=require("./test.jpg");
document.body.appendChild(img);

[webpack.config.js]
 {test:/\.(jpg|png)$/,loader:"style-loader!css-loader"}
 
> cnpm install file-loader url-loader --save-dev
```





### webpack-dev-server

轻量级服务器，修改代码后会自动刷新浏览器

```
> cnpm install webpack-dev-server -g
> cnpm install webpack-dev-server --save-dev  //将依赖写入package.json
> webpack-dev-server --hot--line [--port 3000]//自动刷新

[webpack.config.js]
 devServer:{
        //设置项目根目录
        contentBase:__dirname,
        //服务器的IP地址，可以使用IP也可以使用localhost
        host:'localhost',
        //服务端压缩是否开启
        compress:true,
        //配置服务端口号
        port:3000
    }
```



### js模块打包

webpack内部集成了common.js的js模块打包机制，可以按js的依赖依次引入对应的js文件;

````

[main.js]
var autil = require("autil.js");
var dt= new Date();
autil.print(dt,2);

[autil.js]
var util = require("util.js")
module.exports{
    print:function(date,2){
         consoe.log(util.getDate(date,type))
    }
}

[util.js]
module.exports{
     getDate:function(date,type){
           if(type==2){return "2017年10月23日"}
           if(type==1){return "2017-10-23"}
     }
}
````



### 插件使用(压缩文件) 

插件可以完成loader不能完成的功能，有些插件内置到webpack中，有些可通过npm单独安装,

uglify-js是用npm安装的js代码压缩工具，在grunt和gulp中经常使用;

```
[webpack.config.js]
var webpack = require("webpack");
plugins:[
       new webpack.optimize.UglifyJsPlugin({
            compress:{
                warnings:false
            }
       })
   ]
```



### 打包html  

动态打包index.html文件，bundle.js文件动态加载文件中;

```
>cnpm install --save-dev html-webpack-plugin 

[webpack.config.js]
const htmlPlugin= require('html-webpack-plugin');
new htmlPlugin({
            hash:true,
            template:'./src/index.html'
        })
```



### less 打包

```
> cnpm install less-loader --save-dev

[black.less]
@base:#000;
#box{width:300px; height:300px; background:@base;}

[main.js] 	
import less from './black.less';

[webpack.config.js]
{test:/\.less$/,loader:"style-loader!css-loader!less-loader"}
```

a2.js  a1.js  a.js

b2.js b1.js b.js

### 多入口文件

```
[webpack.config.js]

module.exports={
   entry:{
        bd1:"./main1.js",
        bd2:"./main2.js"
   }
   output:{
       filename:"[name].js"
   }
}
```



### vue文件

vue  --  vue-cli  ---> 依赖包  --> 打包

### 技术胖博客

```
http://jspang.com/2017/09/16/webpack3-2/
```



### gulp 与 webpack的比较

```
http://www.gulpjs.com.cn/docs/getting-started/
```



