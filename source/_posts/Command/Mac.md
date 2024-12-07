---
title: Mac
date: 2022-07-13
category: Command
---
<!--more-->

# Mac 

## 1. brew
我们使用linux下有yum，mac相应的是brew，直接使用中科大源安装brew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://cdn.jsdelivr.net/gh/ineo6/homebrew-install/install)"

#  换源
# $ 指返回 brew --repo 的结果
cd "$(brew --repo)"

git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" // ? homebrew-cask

git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```

## 2. 问题

- import torch 出现如下问题

```bash
renrendeMacBook-Pro-3:NoteBook_PyTorch renren$ /Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 /Users/renren/NoteBook/NoteBook_PyTorch/1.tensor.py
Traceback (most recent call last):
  File "/Users/renren/NoteBook/NoteBook_PyTorch/1.tensor.py", line 1, in <module>
    import torch
  File "/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/torch/__init__.py", line 202, in <module>
    from torch._C import *  # noqa: F403
ImportError: dlopen(/Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/torch/_C.cpython-39-darwin.so, 2): Library not loaded: @loader_path/../.dylibs/libomp.dylib
  Referenced from: /Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/torch/lib/libtorch_cpu.dylib
  Reason: no suitable image found.  Did find:
        /Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/torch/lib/../.dylibs/libomp.dylib: cannot load 'libomp.dylib' (load command 0x80000034 is unknown)
        /Library/Frameworks/Python.framework/Versions/3.9/lib/python3.9/site-packages/torch/lib/../.dylibs/libomp.dylib: cannot load 'libomp.dylib' (load command 0x80000034 is unknown)

# 解决方法
brew install libomp
```