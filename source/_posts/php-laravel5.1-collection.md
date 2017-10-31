---
title: Laravel 5.1 服务 —— 集合
date: 2017-10-24
categories: 
- PHP
- Laravel5.1
---

# 简介
Illuminate\Support\Collection类为处理数组数据提供了平滑、方便的封装。例如，查看下面的代码，我们使用帮助函数collect创建一个新的集合实例，为每一个元素运行strtoupper函数，然后移除所有空元素

```
$collection = collect(['taylor', 'abigail', null])->map(function ($name) {
    return strtoupper($name);
})->reject(function ($name) {
    return empty($name);
});

``` 
