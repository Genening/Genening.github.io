---
title: 404problem
date: 2019-08-29 12:53:52
thumbnail: /gallery/thumbnail/workspace.png
categories: log
tags: 博客建设
---
在8月28日晚，也就是昨晚，在更新了一些_config.yml里面的内容后，输入`hexo clean && hexo g && hexo d`指令后，出现了页面404，不管是刷新还是改其他信息，都无法解决这个问题，在看了网上很多相关博客后也没有找到问题的根源，最终还是在仔细看了GitHub的404页面的提醒，如下图<br>
<!--more-->
![404page](404problem/404problem.png)
才发现，原来是GitHub的page的repository的根目录里没有了`index.html`文件，导致在访问`https://genening.github.io`时GitHub无法找到静态网页的文件，所以显示不出来，跳转到了404页面
找到了问题所在之后，我就开始想办法解决了。先是查看了另外一个网站—— `https://193.148.16.42`的根目录的index.html文件，看看里面的内容应该是什么，然后再查看了整个目录的结构，对比我部署到GitHub的repository里面的文件目录结构，发现有很多不同，如果自己从头做一份的话很麻烦，而且hexo博客应该会自动生成，怎么会没有了呢，于是我就重新运行了一遍`hew new "blogname"`，发现hexo博客又重新生成了一遍目录，这一次目录结构就和另一份博客的目录一致了，于是我紧接着`hexo clean && hexo g && hexo d`一遍，发现GitHub上面的目录又更新了，再次访问，就能显示正常的blog页面了。
具体产生这个问题的原因还不知道，不过也算是吃一堑长一智了，下次注意一些就好，而且也找到了解决问题的思路，也算是花费了我半天时间找解决办法的收获吧。故写此博客用以记录。
