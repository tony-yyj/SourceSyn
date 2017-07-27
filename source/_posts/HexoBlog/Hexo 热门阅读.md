---
title: Hexo 添加热门阅读
abbrlink: 2683804451
date: 2017-07-26 21:30:09
tags: 
    - Hexo
    - Next主题
categories: Hexo搭建博客
---
热门阅读
<!-- more -->
```js
<script src="https://cdn1.lncld.net/static/js/av-core-mini-0.6.1.js"></script>
<script>AV.initialize("{{theme.leancloud_visitors.app_id}}", "{{theme.leancloud_visitors.app_key}}");</script>
<script type="text/javascript">
  var time=0
  var title=""
  var url=""
  var query = new AV.Query('Counter');//表名
  query.notEqualTo('id',0); //id不为0的结果
  query.descending('time'); //结果按阅读次数降序排序
  query.limit(20);  //最终只返回10条结果
  query.find().then(function (todo) {
    for (var i=0;i<10;i++){ 
      var result=todo[i].attributes;
      time=result.time; 
      title=result.title; 
      url=result.url;    
      var content="<p>"+"<font color='#0477ab'>"+"【阅读次数:"+time+"】"+"<a href='"+"http://wwww.mashangxue123.com"+url+"'>"+title+"</font>"+"</a>"+"</p>";
      document.getElementById("heheda").innerHTML+=content
    }
  }, function (error) {
    console.log("error");
  });
</script>
```