---
layout: post
title:  "Install pymupdf on raspberry pi"
date:   2021-11-18 13:50:00 +0800
comments_id: 1
categories: [kb]
---

Installing pymupdf on raspberry pi may occurs errors because of the version of apt libmupdf and pymupdf are not match:

```bash
root@raspberrypi:~# apt search mupdf
Sorting... Done
Full Text Search... Done
libmupdf-dev/stable 1.14.0+ds1-4+deb10u2 armhf
  development files for the MuPDF viewer
  
root@raspberrypi:~# pip3 show pymupdf
Name: PyMuPDF
Version: 1.19.1
Summary: Python bindings for the PDF toolkit and renderer MuPDF
Home-page: https://github.com/pymupdf/PyMuPDF

```

The following steps is the guide of install latest mupdf and pymupdf
1, install depends libs
`apt install mesa-common-dev libgl1-mesa-dev libglu1-mesa-dev libxi-dev libxrandr-dev`

2，build mupdf source

```bash
#download source code and place it to /usr/mupdf-1.19.0-source.tar.xz:
wget https://mupdf.com/downloads/archive/mupdf-1.19.0-source.tar.xz
tar -xvf mupdf-1.19.0-source.tar.xz
cd mupdf-1.19.0-source
make -j4
make install
#copy ft2build.h headers to mupdf
cp /usr/mupdf-1.19.0-source/thirdparty/freetype/include/* /usr/local/include/mupdf
```

3, install pymupdf
`pip3 install pymupdf`

4, done