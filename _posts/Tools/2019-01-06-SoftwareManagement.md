---
layout: "post"
title: "Software Management"
date: "2019-01-06 15:32"
---

# Linux

## Tools Config

### Linux Env

```sh
yubao@yubao-Z370M-S01:~/GitProject/yubaoliu.github.io$ uname -a
Linux yubao-Z370M-S01 4.15.0-43-generic #46~16.04.1-Ubuntu SMP Fri Dec 7 13:31:08 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```

### python

- python2.7
```sh
sudo apt install python2.7 python-pip
```
Don't delete current python3, otherwise Ubuntu OS will BROKE.


### software-center

```sh
sudo apt-get install software-center
```

### Atom
[Install Guide](http://tipsonubuntu.com/2016/08/05/install-atom-text-editor-ubuntu-16-04/)


### Pandoc
- [pandoc-fignos](https://github.com/tomduck/pandoc-fignos)

```sh
pip2 install --user  pandoc-fignos
```
- [pandoc-tablenos](https://github.com/tomduck/pandoc-tablenos)
```sh
pip install pandoc-tablenos
pip install --upgrade pandoc-tablenos  #for upgrade
```
- [pandoc-eqnos](https://github.com/tomduck/pandoc-eqnos)

```sh
pip2 install --user pandoc-eqnos
```

- [pandoc-citeproc](https://github.com/jgm/pandoc-citeproc)


### LaTeX

```sh
sudo apt-get install perl-tk
sudo apt-get install texlive-full
sudo apt-get install texlive-fonts-recommended #maybe not need
```
