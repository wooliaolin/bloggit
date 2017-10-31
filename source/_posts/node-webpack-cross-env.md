---
title: laravel-mix node webpack error 
date: 2017-10-10
categories: 
- PHP
- laravel
- Laravel-mix
---

运行 Mix ` npm run production ` 时报错：

` Module build failed: ModuleBuildError: Module build failed: Error: /home/www/shelectric/node_modules/mozjpeg/vendor/cjpeg: error while loading shared libraries: libpng12.so.0: cannot open shared object file: No such file or directory `
![error](http://pic.signalonline.cn/clipboard.png)
缺少libpng12.so.0
` yum install libpng12 `  <font color=#ec502b>安装后完美解决。</font>