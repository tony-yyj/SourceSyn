---
title: Hexo七牛图床使用
abbrlink: 3030296820
date: 2017-07-28 10:51:05
tags: 
    - Hexo
    - Hexo优化
categories: Hexo
alias: 3030296820/
---
<!-- TOC -->

- [1. 七牛云介绍](#1-七牛云介绍)
- [2. 创建七牛云账号](#2-创建七牛云账号)
- [3. 安装插件一键部署](#3-安装插件一键部署)

<!-- /TOC -->
<!-- more -->

# 1. 七牛云介绍

七牛云是国内领先的企业级云服务商,重点是七牛的免费额度啊：

- 10GB 永久免费存储空间
- 每月10GB 下载流量
- 每月10 万次 Put 请求
- 每月100 万次 Get 请求
- 国内有多个CDN，速度足够快，还可以申请全球加速。
对于小站，完全够用了。

# 2. 创建七牛云账号
  http://www.qiniu.com/

- 在添加资源中，找到“对象存储”,“立即添加”，“创建对象存储”
- 找到内容控制，上传图片（图片名最好为bg+日期，这样外链URL比较清楚简洁）。
- 在操作栏点击···复制外链；也可以不复制只需更改外链最后的图片名，将外链URL放在```![](外链URL)```中。

# 3. 安装插件一键部署

在你的hexo主目录下运行以下命令进行安装

```bash
npm install hexo-qiniu-sync --save
```

添加插件配置信息到 _config.yml 文件中:

```yml
#七牛云存储设置
##offline       是否离线. 离线状态将使用本地地址渲染
##sync          是否同步
##bucket        空间名称.
##access_key    上传密钥AccessKey
##secret_key    上传密钥SecretKey
##secret_file   秘钥文件路径，可以将上述两个属性配置到文件内，防止泄露，json格式。绝对路径相对路径均可
##dirPrefix     上传的资源子目录前缀.如设置，需与urlPrefix同步 
##urlPrefix     外链前缀.
##up_host      上传服务器路径,如选择华北区域的话配置为http://up-z1.qiniu.com
##local_dir     本地目录.
##update_exist  是否更新已经上传过的文件(仅文件大小不同或在上次上传后进行更新的才会重新上传)
##image/js/css  子参数folder为不同静态资源种类的目录名称，一般不需要改动
##image.extend  这是个特殊参数，用于生成缩略图或加水印等操作。具体请参考http://developer.qiniu.com/docs/v6/api/reference/fop/image/ 
##              可使用基本图片处理、高级图片处理、图片水印处理这3个接口。例如 ?imageView2/2/w/500 即生成宽度最多500px的缩略图
qiniu:
  offline: false
  sync: true
  bucket: bucket_name
  secret_file: sec/qn.json or C:
  access_key: AccessKey
  secret_key: SecretKey
  dirPrefix: static
  urlPrefix: http://bucket_name.qiniudn.com/static
  up_host: http://upload.qiniu.com
  local_dir: static
  update_exist: true
  image: 
    folder: images
    extend: 
  js:
    folder: js
  css:
    folder: css
```

- bucket 指的是七牛账户创建的七牛存储控件的名称
- access_key 与 secret_key是七牛账户的秘钥，可以在秘钥管理中查看
- dirPrefix  这个是七牛的目录名，七牛存储空间没有显示的目录。所谓目录，就是在指定访问域名后面先加上你的目录名，再加上你上传的图片名，这样就相当于目录了，来区分图片的分类
- urlPrefix  这个是访问图片的域名地址，比如我的是` http://otrbi6kkj.bkt.clouddn.com/qiniuhexo`可以在七牛的内容管理上自己上传一张图片，然后查看外链，就会一目了然了
- local_dir 这个是本地的图片文件夹，这个就是插件同步七牛的图片来源。你所有的图片等资源都放在这里。名字可以任意，需要在博客根目录下创建这个文件夹，如我的是 qiniuhexo
- image、js、css 这三个参数是文件夹的名字，这三个文件夹会在hexo运行后，插件自动会在上一步你指定的那个local_dir下创建这三个文件，名字分别是folder参数值，分别可以放相应的资源


[Hexo七牛图床使用 - Roylee Blog From A iOS Developer  ](http://error408.com/2016/08/02/Hexo%E4%B8%83%E7%89%9B%E5%9B%BE%E5%BA%8A%E4%BD%BF%E7%94%A8/)

[gyk001/hexo-qiniu-sync](https://github.com/gyk001/hexo-qiniu-sync)

[Hexo 七牛同步插件的使用](http://www.ixirong.com/2016/10/31/how-to-use-hexo-qiniu-sync-plugin/)