---
title: 在Ubuntu中安装chrome和chromedriver
date: 2020-11-7 14:39:26
tags: ubuntu
categories: os
---
**下载chrome**
```
sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
**安装chrome**
```
sudo dpkg -i google-chrome*; sudo apt-get -f install
/opt/google/chrome/chrome
```
**下载chromedrive**
```
wget http://npm.taobao.org/mirrors/chromedriver/2.41/chromedriver_linux64.zip
```
**解压**
```
unzip chromedriver_linux64.zip
```
**复制**
```
cp chromedriver /usr/local/bin/
```
**设置执行权限**
```
chmod +x /usr/local/bin/chromedriver
```
