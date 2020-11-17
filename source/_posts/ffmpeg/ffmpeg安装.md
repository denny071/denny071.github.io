---
title: ffmpeg安装
date: 2020-08-27 14:43:57
tags: ffmpeg
---
### 1.升级系统
```
sudo yum install epel-release -y
sudo yum update -y
sudo shutdown -r now
```

### 2.安装Nux Dextop Yum 源

> 由于CentOS没有官方FFmpeg rpm软件包。但是，我们可以使用第三方YUM源（Nux Dextop）完成此工作。

##### 1) CentOS 7
```
sudo rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm
```

##### 2) CentOS 6
```
sudo rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro
sudo rpm -Uvh http://li.nux.ro/download/nux/dextop/el6/x86_64/nux-dextop-release-0-2.el6.nux.noarch.rpm
```
### 3.安装FFmpeg 和 FFmpeg开发包
```
sudo yum install ffmpeg ffmpeg-devel -y
```

### 4.测试是否安装成功
```
ffmpeg
```
### 5.其他
> 如果你想了解更多关于FFmpeg使用方面的资料，可以输入：
```
ffmpeg -h
```

> 例子：
使用FFmpeg将mp3转为ogg
```
ffmpeg -i MLKDream_64kb.mp3 -c:a libvorbis -q:a 4 MLKDream_64kb.ogg
```
> 使用FFmpeg将flv转为mp4
```
ffmpeg -i beeen.flv -y -vcodec copy -acodec copy beeen.mp4
```
