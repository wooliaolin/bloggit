---
title: PHP office文档预览 《OpenOffice篇》
date: 2017-10-18
categories: 
- PHP
- openoffice
- jodconverter
description: php + openoffice + jodconverter 实现word转pdf 
---

## 概要 
### linux centos7安装 openoffice 
* OpenOffice 下载：http://www.openoffice.org/download/index.html

### linux centos7安装 JDK 1.7  
首先是jdk 1.7 64bit & 32bit的下载地址：
* jdk-7u79-linux-x64.tar.gz (http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.tar.gz)
* jdk-7u79-linux-i586.tar.gz (http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-i586.tar.gz)

### 安装步骤
1. 查看系统要求
2. 下载Apache OpenOffice你最喜欢的Linux版本
3. 使用下面的命令：tar -xvzf “linux包的名字”.tar.gz
4. 这将创建一个安装目录。
5. 安装目录的名称很可能会有语言名的缩写，例如，en-US.
6. su到 root 用户,如果有必要，浏览到Apache OpenOffice的安装目录（解压缩后的档案的位置）.
7. cd到安装目录下RPMS子目录.
8. 你应该能看到许多rpm包和一个名为"desktop-integration"的子目录.
9. 输入` rpm -Uvih *rpm ` ，安装新版本. 默认将会安装/升级Apache OpenOffice到/opt目录.
10. 在安装目录下cd 到 desktop-integration,根据软件包管理器/系统，安装相应的桌面界面的RPM
（我安装的是 ` rpm -Uvih desktop-integration/openoffice4.1.3-redhat-menus-4.1.3-9783.noarch.rpm ` ）。
11. 最后，启动 Apache OpenOffice 3.4.x确保它正常工作.
12. 启动OpenOffice ` cd /opt/openoffice4/program/  ` ` soffice --headless --accept="socket,host=127.0.0.1,port=8100;urp;" --nofirststartwizard &`
---

注意 [openoffice4 不能正常启动，参考解决方案](http://blog.csdn.net/laoyang360/article/details/77342583)

---

### 输入：` openoffice4 ` 启动报错
` javaldx: Could not find a Java Runtime Environment!
/opt/openoffice4/program/soffice.bin: error while loading shared libraries: libXext.so.6: cannot open shared object file: No such file or directory `
表明没有安装JDK。

### yum安装JDK
1. ` yum -y list java* ` 查看yum库是否有java安装包
2. ` yum -y install java-1.8.0-openjdk* ` 我这里安装的是java-1.8.0 的jdk
3. ` java -version ` 查看安装结果

### 下载jodconverter 安装了这个之后就已经可以实现DOC转PDF了

### 测试

启动 ` /opt/openoffice4/program/soffice --headless --nologo -nofirststartwizard -accept="socket,host=0.0.0.0,port=8100;urp;"  & `
> [openoffice参数选项说明](http://blog.csdn.net/liangpz521/article/details/14522045)
> 查看服务是否启动（端口8100是否被soffice占用）：netstat -lnp |grep 8100
测试 ` java -jar /opt/jodconverter-2.2.2/lib/jodconverter-cli-2.2.2.jar /opt/1.docx /opt/13.pdf `
报错：` ERROR:connection failed. Please make sure OpenOffice.org is running and listening no port 8100. `
<font color=#ec502b>提示openoffice.org 没有启动或是没有绑定8100端口.</font>
### 开启8100端口
[添加端口——参考](http://blog.csdn.net/c233728461/article/details/52679558)
我这里用的是阿里云ecs，直接添加安全组规则
![添加安全组规则](http://pic.signalonline.cn/20171017celue01.png)
<font color=#ec502b>重新启动、测试、成功！</font>

### 解决中文乱码
1. 直接将windo下的 ` 黑体、宋体 ` 等中文字体文件 上传到 ` /opt/openoffice4/share/fonts ` 
2. 重启openoffice


### openoffice服务自启动
[参考资料](http://blog.csdn.net/zouqingfang/article/details/44460823)
1. 创建自启动脚本/etc/init.d/openoffice,并添加以下脚本内容
```
#!/bin/bash   
#chkconfig: 2345 80 90  
#description:auto_run  
#openoffice4 start service  
/opt/openoffice4/program/soffice -headless -accept="socket,host=127.0.0.1,port=8100;urp;" -nofirststartwizard & 

```
2. 设置openoffice为linux服务模式
```
chmod 755 openoffice  
chkconfig  ––add openoffice  
chkconfig openoffice on  
chkconfig –list  
ps aux|grep openoffice  

```

### php实现代码
> [参考资料](http://blog.csdn.net/xu5733127/article/details/49863069)
word转换PDF
```
/**
*
* @param unknown $wordpath  要转换为PDF的word文件路径，全路径 如F://duanxin.doc
* @param unknown $outPdfPath  转换成功后的PDF文件路径
* @param unknown $jodconverterPath 安装的jodconverter的jodconverter-cli-2.2.2.jar所在路径，我的为：D://jodconverter//jodconverter-2.2.2//lib//jodconverter-cli-2.2.2.jar
* @return boolean
*/
function word2pdf ($wordpath, $outPdfPath, $jodconverterPath) {
    if (empty($wordpath)) return false;    
    try {
        //这里是因为我吧Java（jdk/jre）加入了环境变量,故可直接写出下面这样， 
        //相当于cmd窗口下直接写 java -jar jodconverter-cli-2.2.2.jar所在路径 word文件 PDF文件
        $p = "java -jar ". $jodconverterPath . ' ' . $wordpath . ' ' . $outPdfPath;
        // 否则该前面应该加入jre/jdk的路径
        exec($p);
        return true;
    } catch (Exception $e) {
        return false;
    }
}

```
