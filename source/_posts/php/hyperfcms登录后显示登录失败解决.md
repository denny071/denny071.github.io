---
title: hyperfcms登录后显示登录失败解决
categories: php
date: 2020-10-24 10:30:43
tags: hyperfcms
---



hyperfcms登录后显示登录失败，是因为配置引起的问题，需要修改配置。

打开`hyperfcms/cms_php/config/autoload/server.php`

将 `static_handler_locations`下面注释 

```php
<?php
  
// 'static_handler_locations' => ['/'],
```



