---
title: 关闭Mac系统的SIP
categories: os
date: 2020-10-29 09:56:10
tags: macos
---



### 如何查看SIP状态

在终端中输入csrutil status，就可以看到是enabled还是disabled。（只要显示 disabled 说明已经禁用SIP）![4fdba006ly1g23a3jwla4j211w0qiqbb-768x537](%E5%85%B3%E9%97%ADMac%E7%B3%BB%E7%BB%9F%E7%9A%84SIP/4fdba006ly1g23a3jwla4j211w0qiqbb-768x537.jpg)

### 如何关闭SIP

1. 重启你的Mac，当听到第一声响后（或者说在开机的时候），按住 Command + R键，按住不动，稍待片刻，电脑会进入到恢复模式。

![4fdba006ly1g23a1ikskcj20lc0sgadu](%E5%85%B3%E9%97%ADMac%E7%B3%BB%E7%BB%9F%E7%9A%84SIP/4fdba006ly1g23a1ikskcj20lc0sgadu.jpg)



2. 进入后打开顶部实用工具--终端

![4fdba006ly1g23cb0k7zyj20of0g6q8x](%E5%85%B3%E9%97%ADMac%E7%B3%BB%E7%BB%9F%E7%9A%84SIP/4fdba006ly1g23cb0k7zyj20of0g6q8x.jpg)



3. 输入命令csrutil disable关闭SIP。 (同样的步骤输入命令csrutil enable，即可重新打开SIP)

   ![4fdba006ly1g23cdo22wvj20ko0d7wgy](%E5%85%B3%E9%97%ADMac%E7%B3%BB%E7%BB%9F%E7%9A%84SIP/4fdba006ly1g23cdo22wvj20ko0d7wgy.jpg)

4. 关闭重启进入系统即可;