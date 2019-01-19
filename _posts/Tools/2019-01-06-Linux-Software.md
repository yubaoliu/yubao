---
layout: "post"
title: "Software Management"
date: "2019-01-06 15:32"
---

# Linux

## System Info

```sh
yubao@yubao-Z370M-S01:~/GitProject/yubaoliu.github.io$ uname -a
Linux yubao-Z370M-S01 4.15.0-43-generic #46~16.04.1-Ubuntu SMP Fri Dec 7 13:31:08 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```

## Quick build from zero

```sh

# OpenCV
#Remove any previous installations of x264</h3>
sudo apt-get remove x264 libx264-dev
sudo apt-get install build-essential checkinstall cmake pkg-config yasm
sudo apt-get install git gfortran
sudo apt-get install libjpeg8-dev libjasper-dev libpng12-dev
sudo apt-get install libtiff5-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libdc1394-22-dev
sudo apt-get install libxine2-dev libv4l-dev
sudo apt-get install libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev
sudo apt-get install qt5-default libgtk2.0-dev libtbb-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libfaac-dev libmp3lame-dev libtheora-dev
sudo apt-get install libvorbis-dev libxvidcore-dev
sudo apt-get install libopencore-amrnb-dev libopencore-amrwb-dev
sudo apt-get install x264 v4l-utils

# Optional dependencies
sudo apt-get install libprotobuf-dev protobuf-compiler
sudo apt-get install libgoogle-glog-dev libgflags-dev
sudo apt-get install libgphoto2-dev libeigen3-dev libhdf5-dev doxygen

# Python
sudo apt-get install python-dev python-pip python3-dev python3-pip
sudo -H pip2 install -U pip numpy
sudo -H pip3 install -U pip numpy
pip install --user numpy scipy matplotlib scikit-image scikit-learn ipython

```

## DESKTOP
### check current desktop environments
```bash
yubao@yubao-Z370M-S01:~$ echo $DESKTOP_SESSION
ubuntu


yubao@yubao-Z370M-S01:~$  ls /usr/bin/*session*
/usr/bin/dbus-run-session       /usr/bin/gnome-session-inhibit     /usr/bin/session-installer  /usr/bin/xfce4-session-logout
/usr/bin/gnome-session          /usr/bin/gnome-session-properties  /usr/bin/session-migration  /usr/bin/xfce4-session-settings
/usr/bin/gnome-session-classic  /usr/bin/gnome-session-quit        /usr/bin/xfce4-session      /usr/bin/x-session-manager

```

### Remove DESKTOP

```sh
sudo apt-get purge gnome*
sudo apt-get purge xfce4-*

sudo apt-get autoclean
```

## python

```sh
sudo apt-get install python-dev python-pip python3-dev python3-pip
sudo -H pip2 install -U pip numpy
sudo -H pip3 install -U pip numpy
pip install --user numpy scipy matplotlib scikit-image scikit-learn ipython
```

Don't remove current python3, otherwise Ubuntu OS will BROKEN.


## software-center

```sh
sudo apt-get install software-center
```

## Atom
[Install Guide](http://tipsonubuntu.com/2016/08/05/install-atom-text-editor-ubuntu-16-04/)


## Pandoc

```sh
sudo apt install pandoc pandoc-citeproc
pip install --user  pandoc-fignos
pip install --user pandoc-tablenos
pip install --upgrade pandoc-tablenos  #for upgrade
```

- [pandoc-fignos](https://github.com/tomduck/pandoc-fignos)
- [pandoc-tablenos](https://github.com/tomduck/pandoc-tablenos)
- [pandoc-eqnos](https://github.com/tomduck/pandoc-eqnos)
- [pandoc-citeproc](https://github.com/jgm/pandoc-citeproc)

## Markdown

```sh
sudo apt-get install markdown
```

## LaTeX

```sh
sudo apt-get install perl-tk perl-doc
sudo apt-get install texlive-full
sudo apt-get install texlive-fonts-recommended #maybe not need
sudo apt install texlive-latex-extra
```


## grive

```sh
sudo add-apt-repository ppa:nilarimogard/webupd8
sudo apt-get update
sudo apt-get install grive
```

## ibus

[iBus](http://wiki.ubuntu.org.cn/IBus)

## Screenshot

- gnome-screenshot
- Shutter
- Scrot
- Deepin-ScreenShot
