---
title: 将macos的python进行升级
date: 2020-08-27 14:41:19
tags:
---
```
sudo mv /Library/Frameworks/Python.framework/Versions/3.7 /System/Library/Frameworks/Python.framework/Versions
sudo chown -R root:wheel /System/Library/Frameworks/Python.framework/Versions/3.7
sudo rm /System/Library/Frameworks/Python.framework/Versions/Current s
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.7 /System/Library/Frameworks/Python.framework/Versions/Current
sudo rm /usr/bin/pydoc
sudo rm /usr/bin/python
sudo rm /usr/bin/pythonw
sudo rm /usr/bin/python-config
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.7/bin/pydoc3.7 /usr/bin/pydoc 
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.7/bin/python3.7 /usr/bin/python 
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.7/bin/pythonw3.7 /usr/bin/pythonw 
sudo ln -s /System/Library/Frameworks/Python.framework/Versions/3.7/bin/python3.7m-config /usr/bin/python-config

```