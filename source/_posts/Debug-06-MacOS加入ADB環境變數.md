---
title: '[Debug] 06-MacOS 加入 ADB 環境變數'
date: 2024-09-04T19:28:21+08:00
tags:
- 16th鐵人賽
- ADB
- Android
---

# 情境
偶爾開發遇到電腦跟手機之間的問題，網路的教學常用到 `adb xxx` 的指令。每次突然要用，就發現自己還沒設好環境變數。今天就趁這個機會把環境配置好！
<!-- more -->

# ADB 介紹
Android Debug Bridge (adb) 是一種多功能的指令列工具，可讓您與裝置通訊。adb 指令會執行各種裝置動作 (例如安裝應用程式及偵錯應用程式)。adb 提供 Unix 殼層，可讓您在裝置上執行各種指令。

# 環境設定
今天的介紹以 MacOS 為主，Windows 的設定大同小異，可以參考網路上其他教學。

## 1. 找到 SDK 路徑
若已安裝 Android Studio，不需要另外下載，已經內建了，路徑：
- MacOS
```shell
/Users/[使用者名稱]/Library/Android/sdk/platform-tools
```
- Windows
```shell
C:\Users\[使用者名稱]\AppData\Local\Android\sdk\platform-tools
```

## 2. 設定環境變數
[以下的設定檔都放在家目錄]
> 補充：
> 1. `家目錄` = `~` = `/Users/[使用者名稱]`
> 2. 檔名前面有 `.`，代表是隱藏檔。`ls -a` 才看得到。

網路上看到有人會把環境變數寫在 `.bash_profile`。但 MasOS 主要的 shell 是 **zsh**，所以其實直接寫在 `.zshrc` 就可以了。

```shell
# 切換到家目錄
cd ~

# 編輯 `.zshrc` 檔案，若無此檔案，請建立一個。我習慣用 vim，你可以用任何編輯器。
vim .zshrc

# 在 `.zshrc` 加入以下內容
export PATH=${PATH}:/Users/[使用者名稱]/Library/Android/sdk/platform-tools

# 重新載入設定檔，讓變更生效
source .zshrc

# 測試設定是否成功，若能查到版本資訊就算成功！
adb version
```

# 總結
今天只介紹，adb 的環境變數配置。更多 adb 指令的用法，請參考[官方文件](https://developer.android.com/tools/adb?hl=zh-tw)，或是我之前的文章([ADB - 在你的手機上下指令](https://dreambo4.github.io/2017/10/26/ADB-%E5%9C%A8%E4%BD%A0%E7%9A%84%E6%89%8B%E6%A9%9F%E4%B8%8A%E4%B8%8B%E6%8C%87%E4%BB%A4/))。

# 參考資料
- Android Debug Bridge (adb) : https://developer.android.com/tools/adb?hl=zh-tw
