# hiuiao.github.io

基于jekyll完成.

## 初始安装
创建github项目.按照xxx.github.io填写项目名称.  
Add .gitignore加上jdkyll.license随意  

```shell
git clone https://github.com/xxx/xxx.github.io.git
gem install jekyll bundler
cd xxx.github.io.git
jekyll new ./ --force
bundle install
bundle exec jekyll serve
#此时jekyll已经在本地运行.http://127.0.0.1:4000/

```

## 配置

\_config.yml进行配置  
修改titile,email,github\_username,注释掉twitter\_username

## 写博客

将文件加入\_posts文件夹内  
按照YYYY-MM-DD-title.markdown添加文件
文件开头需要填写如下yaml信息:

```
---
layout: post
title: "title"
date: YYYY-MM-DD 12:00:00 +0800
```
