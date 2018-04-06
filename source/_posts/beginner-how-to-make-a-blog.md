title: github + hexo(melody) + travis 做免费且高大上的博客
categories:
  - 博客
date: 2018-04-06 12:16:00
tags: blog
---

从上大学到现在，换过很多博客网站，从最早的博客园，到CSDN，再到阿里云主机上自建博客，写了很多东西，但非常零散，而且也觉得UI样式过时了。
直到遇到github、hexo和travis，才感觉写博客是可以多么`专注`。
最近偶然发现一个hexo主题，特别的好看，因此想写下这篇文章。
一来做个总结，二来当做对此主题的推广和对主题maker的感谢！
废话不多说，上菜。

> 本文假定你使用的是`MAC`，且安装有`Node`，且懂得使用`github`和`git`命令

## 如何才算做到专注
`写完blog，直接push到github，完事`。这，就是本文要实现的效果。

## github
[官网](https://github.com)
首先在github上创建一个项目，项目必须要遵守格式：账户名.github.io。
然后从master切出一个分支，如hexo分支，我们把hexo分支作为写博客的分支，把master作为travis构建好的静态资源分支。

## hexo
[官网](https://hexo.io/)
```
npm install hexo-cli -g
hexo init blog
cd blog
npm install
hexo server
```
服务器起来后就可以在浏览器中输入[localhost:4000](localhost:4000)实时看到你博客了

### melody主题
一切尽在此文档[hexo-theme-melody](https://molunerfinn.com/hexo-theme-melody-doc/#/zh-Hans/)

## travis
[官网](https://travis-ci.org)
### 参考
[hexo持久化构建以及给自有域名github-page上HTTPS](https://molunerfinn.com/hexo-travisci-https/)
[使用 Travis 自动部署 Hexo 到 Github 与 自己的服务器](https://segmentfault.com/a/1190000009054888)
