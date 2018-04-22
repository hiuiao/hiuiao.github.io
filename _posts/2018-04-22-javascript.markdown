---
layout: post
title: "javascript"
date: 2018-04-22 10:38:00 +0800
---
## 语法

* 组成部分

    ```
    核心(ECMAScript)
    文档对象模型(DOM)
    浏览器对象模型(BOM):html5
    ```
    
* script外部脚本放置位置

    ```
    放在<head>中意味着必须等到全部代码被下载解析和执行完之后才能呈现页面内容.所以一般放在<body>后面
    ```
    
* 变量

    ```
    区分大小写.关键字不能做变量或函数的名字.
    变量使用前无需定义.
    定义方式:var+变量名
    
    基础数据类型:number,boolean,string('或"括起来),undefined(已创建但没有赋值的变量),null(空对象引用)
    复合数据类型:Object(对象,由变量和函数组成),Array(变量组成),Function
    任何一个类都是Object的子类
    
    函数外边直接定义的变量为全局变量,函数内部定义的变量为局部变量
    函数内定义的变量没有块范围,整个函数内有效.哪怕在函数中间使用var声明,在函数开始处照样有效.(如果不不使用var,则开头为全局变量或报错)
    
    String,Boolean,Number,Array,Object,Function都有自己的包装类,可以直接操作包装类的属性和方法
    ```
    
* 字符串函数

    ```
    string.concat()不改变string本身,操作完成后string仍然是原值而不是连接后的值
    ```
    
* 运算符

    ```
    !==(严格不等于,不进行类型转换,比较类型和值.!=会先进行类型转换)
    instanceof(判断某个变量是否是指定类的实例)
    ```
    
* 数值转换

    ```
    parseInt()
    parseFloat()
    float无法判断相等
    String()或num.toString(10)(10进制)
    ```
    
* 注释

    ```
    单行://
    多行:/*  */
    ```

## nodejs

### 命令行(REPL)

* 退出

    ```
    ctrl+c两次或ctrl+d
    process.exit()
    ```

* 变量

    ```
    变量声明可以不用var,但是如果没有的话会直接打印出来所赋的值.(返回undifined表示返回值是void)
    _获取上一个表达式的运算结果
    ```

### 基础语法

* 回调函数(函数式编程)

    ```javascript
    //异步编程的直接体现就是回调.
    //函数a有一个参数,这个参数是函数b.当函数a执行完以后执行函数b.这个过程就叫做回调.
    //回调函数是通过callback来实现的.首先在主函数中要有callback的参数定义,然后在callback部分填上回调函数.回调函数此时只是被定义,只有在执行到callback的时候,回调函数才会真正执行.
    var fs=require("fs");
    fs.readFile('input.txt',function(err,data){
        if(err) return console.error(err);
        console.log(data.toString());
    });
    console.log("程序执行结束!");
    ```

* =>(箭头函数)
    
    ```
    (x)=>x+6 相当于:
    function(x){
        return x+6;
    }
    ```

* stream
    
    ```
    所有stream都是eventemitter的实例
    data:有数据可读时触发
    end:没有更多的数据可读时触发
    error:接收和写入过程中发生错误时触发
    finish:所有数据已被写到底层系统时触发
    ```

* call及apply

    ```
    blackCat.say.call(whiteDog); //whiteDog为没有say对象的待操作对象
    为了动态改变this而出现的.当一个object没有某个方法,但是其他对象有,我们可以借助call或apply用其他对象的方法来操作
    ```

* new

    ```
    如果返回一个函数的返回结果就是一个对象,那么没有任何区别.
    不用创建临时对象.不用return临时对象.
    ```

* pipe

    ```javascript
    //stream流通过pipe来控制流量
    //zlib.createGzip()返回的是一个对象
    //read流流入对象zlib,zlib输出到write
    fs.createReadStream('input.txt').pipe(zlib.createGzip()).pipe(fs.createWriteStream('input.txt.gz'));
    ```

* exports和require

    ```
    exports公开接口,然后用require来获取这个公开的接口
    ```

### 代码分析

* server.js代码分析

    ```javascript
    //请求自带的http模块,并把它赋值给http变量
    var http=require('http');
    
    //调用http提供的函数createserver.括号内是其构造函数.这个函数返回一个对象.这个对象有个listen的方法
    http.createServer(function(request,response){
        response.writeHead(200,{'Content-Type':'text/plain'});
        response.end('Hello World\n');
    }).listen(8888)
    
    console.log('Server running at http://127.0.0.1:8888/')
    ```

### npm

* 全局安装与本地安装
    
    ```
    npm install express -g(加g就是全局)
    全局安装将安装包放在/usr/local下,可以直接在命令行里使用.
    本地安装将安装包放在./node_modules下(运行npm命令时所在的目录)
    ```

* package.json
    
    ```
    位于node_modules/express/package.json
    main字段:指定了程序的主入口文件.require('modulename')就会加载这个文件.默认是indwx.js
    ```

* 卸载/更新/搜索

    ```
    npm uninstall express
    npm update express
    npm search express
    ```

* 创建/发布模块

    ```
    npm init
    npm adduser //注册用户
    npm publish //发布
    ```
    
* 版本号

    ```
    X.Y.Z
    bug修改->Z
    新增功能,但向下兼容->Y
    向下不兼容->X
    ```

* cnpm

    ```
    使用国内源
    npm install -g cnpm --registry=https://registry.npm.taobao.org
    ```


## 工具

* webstorm设置

    File->Settings->Languages & Frameworks->Node.js and NPM,点击旁边的enable即可
