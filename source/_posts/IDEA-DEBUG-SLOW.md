---

title: IDEA DEBUG SLOW
comments: true
tags:
  - IDEA
  - DEBUG
categories:
  - IDEA
date: 2017-08-22 09:55:37
update: 2017-08-22 09:55:37

---


hi, all 

我之前做单元覆盖率时遇到了两个问题。
1.跑测试时，运行特别慢。
2.debug根本进入不了断点。无法debug。

之前以前一直知道不到解决方法，昨天在苦苦查寻下，找到了，解决方法。如果你的test跑的很慢可以借鉴，希望对大家有帮助，帮大家节约一些宝贵的时间。

## 问题一

### 产生的原因：
升级到macOS Sierra后，造成的。

### 解决方法：

命令行运行一下命令：
sudo sed -i bak "s^127\.0\.0\.1.*^127.0.0.1 localhost $(hostname)^g" /etc/hosts
sudo sed -i bak "s^::1.*^::1 localhost $(hostname)^g" /etc/hosts
sudo ifconfig en0 down
sudo ifconfig en0 up

其他方法参考下面链接

[参考链接：](https://stackoverflow.com/questions/39636792/jvm-takes-a-long-time-to-resolve-ip-address-for-localhost/39698914#39698914)




## 问题二

### 产生的原因：

设置了方法断点，idea会提示：method breakpoint may dramatically slow debugging

### 解决方法：

去除所有方法断点

[参考链接：](http://blog.csdn.net/yanziit/article/details/73459795)
