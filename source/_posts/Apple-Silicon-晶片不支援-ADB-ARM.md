---
title: Apple Silicon 晶片不支援 ADB ARM
date: 2022-10-27 01:09:22
tags:
- Android
- Apple Silicon
---

![err_msg](err_msg.jpeg)

<!-- more -->

重點是這句
```
java.io.IOException: error=86, Bad CPU tyoe in executable
```

原因是 ADB 不支援 ARM 架構
參考 [Stockoverflow](https://stackoverflow.com/questions/56553879/android-studio-cause-error-86-bad-cpu-type-in-executable)
輸入這行指令就可以解決
```shell
softwareupdate --install-rosetta
```