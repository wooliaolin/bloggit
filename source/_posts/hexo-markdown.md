---
title: Markdown语法 与 Hexo常用指令
---

# Markdown 语法的简要规则
## 标题
如果一段文字被定义为标题，只要在这段文字前加 # 号即可。
` # 一级标题`
` ## 二级标题`
` ### 三级标题`
以此类推，总共六级标题，建议在井号后加一个空格，这是最标准的 Markdown 语法。

## 列表
无序列表：在文字前加上 `-` 或 `*` 
` * 第1列 `
` * 第2列 `
` * 第3列 `
有序列表：在文字前加 `1.` `2.` `3.`
` 1. 第1列 `
` 2. 第2列 `
` 3. 第3列 `
注意符号和文字直接加上一个空格。

## 表格
```
Name | Academy | score 
- | :-: | -: 
Harry Potter | Gryffindor| 90 
Hermione Granger | Gryffindor | 100 
Draco Malfoy | Slytherin | 90
```
语法说明： 
1. 不管是哪种方式，第一行为表头，第二行分隔表头和主体部分，第三行开始每一行代表一个表格行； 
2. 列与列之间用管道符号 “|” 隔开，原生方式的表格每一行的两边也要有管道符。 
3. 可在第二行指定不同列单元格内容的对齐方式，默认为左对齐，在 “-” 右边加上 “:” 为右对齐，在 “-” 两侧同时加上 “:” 为居中对齐。

Name | Academy | score 
- | :-: | -: 
Harry Potter | Gryffindor| 90 
Hermione Granger | Gryffindor | 100 
Draco Malfoy | Slytherin | 90
> [利用Markdown创建表格](http://blog.csdn.net/tuxingchen6/article/details/55222951)

## 引用
如果你需要引用一小段别处的句子，那么就要用引用的格式。
`> 例如这样`
只需要在文本前加入 > 这种尖括号（大于号）即可

## 粗体与斜体
用两个 ` * ` 包含一段文本就是粗体的语法，用一个 ` * ` 包含一段文本就是斜体的语法。
例如：** 这里是粗体 ** * 这里是斜体 *

## 图片与链接
插入链接与插入图片的语法很像，区别在一个 ` ! ` 号
### 插入链接
` [Baidu](https://www.baidu.com) `
[Baidu](https://www.baidu.com)
### 插入图片
` ![Baidu](https://www.baidu.com/img/bd_logo1.png) `
![百度](https://www.baidu.com/img/bd_logo1.png)

## 代码块
用3个 \` 把中间的代码包裹起来，如:
\`\`\`
    public function func(){
        //...
    } 
\`\`\`

``` 
    public function func(){
        //...
    } 
```

## 分割线
分割线的语法只需要另起一行，连续输入三个星号 ` *** ` 或者 ` --- ` 即可。

### `***分割线`
***
### `---分割线`
---
