---
title: Github+Hexo搭建博客
date: 2018-07-07 13:53:11
tags: 博客搭建
---
# 简介

- 此文是通过Github+Hexo搭建博客的操作步骤，一步一步搭建属于你自己的博客！<!--more-->


## 一、Github配置

- 登录github
- 主页中点击自己的头像，进入your profile
- 点击repositories，新建一个
- Repositories name：yourname.github.io(yourname为用户名)


## 二、环境配置

- 安装[Node.js](https://nodejs.org/en/)
- 安装[Git](https://github.com/waylau/git-for-win)
- 安装完成后，在开始菜单中找到Git-Git Bash，进入命令行
- git config --global user.name "username"
- git config --global user.email "email"
- cmd中输入npm install -g hexo -cli


## 三、网站代码以及设置

- 在C盘创建一个test文件夹，cmd进入test文件夹
- 输入 hexo init blog
- 等待安装后会在test文件夹内创建一个blog文件夹，进入blog文件夹，_config.yml：网站的配置信息，source：资源文件夹，themes：主题文件夹，Hexo会根据主题来生成静态页面
- 等待提示Start blogging with hexo，就是安装成功了，文件夹中自带一篇文章"Hello World"，命令行进入blog目录下，输入hexo g，生成静态文件。
- 输入hexo s，启动服务器，默认情况下，访问网址为localhost:4000。
- 重新打开git bash，输入ssh-keygen -t rsa -C "Github的注册邮箱地址"，一直Enter过来，得到信息:Your public key has been saved in C:/xxx/xxx/.ssh/id_rsa.pub，找到该文件使用记事本打开
- 复制里面所有内容，再进入[github.com/settins/ssh](https://github.com/settings/keys)，New SSH key ---Title:Blog-----Key:刚刚复制的内容。

## 四、博客网站配置信息

- 进入blog文件夹，用sublime打开_config.yml文件，修改参数。

- hexo框架的blog基础信息
    ```
    title: Debris的博客
    subtitle: 不想再犹豫。
    description: Python之路上~
    author: Debris
    language: zh-CN
    timezone: Asia/Shanghai
    ```

- 部署服务器的相关配置信息，只需要修改repo部分
    ```
    deploy: 
      type: git
      repo: https://github.com/username/username.github.io.git
      branch: master
    ```
    
- 各类主题的配置信息，要在主题文件夹下的_config.yml上进行配置。

## 五、发表文章

- cmd进入blog文件夹下，hexo new "Hello Blog"

- 打开info中的地址，打开文件

```
---
title: Hello blog
date: 
tags: 测试
---
测试文章，欢迎关注作者博客: https://qianzhaorong.github.io/

```

- 执行以下步骤
```
C:\test\blog
$ hexo clean
INFO  Deleted database.
INFO  Deleted public folder.

C:\test\blog
$ hexo generate
INFO  Start processing
INFO  Files loaded in 1.48 s
...
INFO  29 files generated in 4.27 s

C:\test\blog
$ hexo server
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/. Press Ctrl+C to stop.
```

- 打开localhost:4000打开后检查，没问题后部署到服务器
```
C:\test\blog
$ hexo deploy
INFO  Deploying: git
```

- 上一步可能会出现：error deployer not found:git，输入以下代码：
```
npm install hexo-deployer-git --save
再次hexo deploy
```

- 同时也有可能出现fatal: HttpRequestException encountered，此时需要更新Windows的git凭证管理器。网址为[https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.14.0](https://github.com/Microsoft/Git-Credential-Manager-for-Windows/releases/tag/v1.14.0)

## 六、访问网站

- 在每一次部署到服务器后，可以通过浏览器访问 username.github.io(这里的username为github的用户名)来访问自己的博客网站。

> tips:若想要使用next主题装饰自己的博客，可以参考[此篇博文](https://reuixiy.github.io/technology/computer/computer-aided-art/2017/06/09/hexo-next-optimization.html#%E9%99%84%E4%B8%8A%E6%88%91%E7%9A%84-custom-styl)。当然如果想要选择其它主题，可以去[hexo主题网站](https://hexo.io/themes/)Look look！


