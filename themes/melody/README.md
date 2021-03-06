# hexo-theme-melody

<p align="center">
  <img src="https://raw.githubusercontent.com/Molunerfinn/hexo-theme-melody-doc/master/docs/imgs/logo.png">
</p>

<p align="center">
  <a href="https://standardjs.com" target="_blank"><img alt="JavaScript Style Guide" src="https://img.shields.io/badge/code_style-standard-brightgreen.svg?style=flat-square"></a>
  <a href="" target="_blank"><img alt="license" src="https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square"></a>
  <a href="https://hexo.io" target="_blank"><img alt="hexo-image" src="https://img.shields.io/badge/hexo-%3E%3D3.0-blue.svg?style=flat-square"></a>
  <a href="https://github.com/Molunerfinn/hexo-theme-melody/releases/latest">
    <img src="https://img.shields.io/github/release/Molunerfinn/hexo-theme-melody.svg?style=flat-square" alt="">
  </a>
</p>

A simple & beautiful & fast theme for Hexo.

See demo:

* [molunerfinn.com](https://molunerfinn.com)
* [Elody's Blog](https://elody-07.github.io)
* [zouyaoji's Blog](https://zouyaoji.top/)
* [flytreeleft's Blog](https://flytreeleft.org/)
* [StaunchKai](http://staunchkai.com/)

# Documentation

Documentation is [here](https://molunerfinn.com/hexo-theme-melody-doc/)

# Screenshots

![](https://raw.githubusercontent.com/Molunerfinn/hexo-theme-melody-doc/master/docs/imgs/index-page.png)
![](https://raw.githubusercontent.com/Molunerfinn/hexo-theme-melody-doc/master/docs/imgs/archives.png)
![](https://raw.githubusercontent.com/Molunerfinn/hexo-theme-melody-doc/master/docs/imgs/post.png)
![](https://raw.githubusercontent.com/Molunerfinn/hexo-theme-melody-doc/master/docs/imgs/post-2.png)
![](https://raw.githubusercontent.com/Molunerfinn/hexo-theme-melody-doc/master/docs/imgs/mobile.png)

# Installation

Find your hexo work folder

```bash
git clone -b master https://github.com/Molunerfinn/hexo-theme-melody themes/melody
```

If you don't have jade & stylus renderer, follow this:

```bash
npm install hexo-renderer-jade hexo-renderer-stylus
```

# Configuration

For smoothly updating theme-melody, I recommand to create a config file named `melody.yml` in your hexo work folder's (**Notice: not the theme-melody folder**) `source/_data` folder(If it doesn't exist, create one)

Copy the contents of `_config.yml` to `melody.yml`. Now you can configure it by yourself and you can update theme-melody smoothly.

# Update

Jump into the melody folder, just `git pull` is OK.

> For more details, please check [documentation](https://molunerfinn.com/hexo-theme-melody-doc/)

# Browser Support

IE >= 10

# TODOS

* ~~Doc~~
* ~~Search~~ // Algolia support
* ~~Analysis~~ // Baidu & Google analytics support
* ~~MathJax~~ // MathJax support
* ~~i18n~~ // zh-Hans & en support
* ~~PWA~~ // v1.2 support
* Performance optimization
* ...

# License

[MIT](http://opensource.org/licenses/MIT)

Copyright (c) 2017 Molunerfinn
