---
layout: post
title:  "qDebug no output on Linux"
date:   2021-11-10 13:50:00 +0800
comments_id: 1
categories: [kb]
---

Sometimes qDebug() cannot print out to console even in debug mode, that's because this function is follow qtlogging.ini file's configuration.
For me, I'm current using CentOS
Firstly, locate the file:
```
[root@localhost build]# locate qtlogging.ini
/usr/share/qt5/qtlogging.ini
```

Secondly, modify the Rules in line 2, modify `*.debug=false` to `*.debug=true`
```
[root@localhost build]# cat /usr/share/qt5/qtlogging.ini
[Rules]
*.debug=true
qt.qpa.xcb.xcberror.warning=false
```

reference:
https://doc.qt.io/qt-5/qloggingcategory.html