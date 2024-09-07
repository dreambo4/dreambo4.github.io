---
title: ADB - 在你的手機上下指令
date: 2017-10-26 01:20:06
tags:
- Android
- ADB
- 資安
- 行雲部落格
---

> 2024/09/07 更新：
> 原本本文所寫「ADB指令參考」，應該是 Shell 指令。

* 本文曾發佈在 [https://blog.cmrdb.cs.pu.edu.tw/?p=432](https://blog.cmrdb.cs.pu.edu.tw/?p=432)

相信大家或多或少都知道Android是一個基於Linux開發的作業系統，既然是Linux，你有沒有想過要在你的手機上下指令呢?

# ADB

ADB(Android Debug Bridge)是一個可以讓你和裝置(虛擬機或實體手機)溝通的工具，透過這個工具，你可以以指令的方式直接在電腦與手機間傳輸檔案、安裝/移除應用程式、讀取手機的SQLite資料庫…等。
<!-- more -->

# 開啟偵錯模式 (使用虛擬機可以跳過)
首先，要開啟**開發人員選項**，手機的開發人員選項預設是關閉的，開啟的方式也因廠牌和型號有些微差異，以 SAMSUNG A5 為例:
 1. 設定 > 關於裝置 > 版本號碼
    連續按七下**版本號碼**，就會發現下方跳出提示訊息，說明你已經成功成為開發人員了!!
    ![image1](image1.png)
    回到上一頁後，就會發現多了一個選項!!
    ![image2](image2.png)
 2. 設定 > 開發人員選項 > USB偵錯 開啟
     偵錯模式主要是用來研發，它可以用來複製電腦和手機間的數據
     ![image3](image3.png)

# 開啟ADB工具
如果已經安裝好Android Studio，ADB的預設路徑在
``` shell
C:\Users\[使用者名稱]\AppData\Local\Android\sdk\platform-tools
```
特別注意，`AppData`資料夾預設是隱藏的，所以在一般情況下看不到的喔!
1. 將手機接上電腦 / 開啟虛擬機
1. 開啟cmd
2. 移到上面的目錄
    ```shell
    cd C:\Users\[使用者名稱]\AppData\Local\Android\sdk\platform-tools
    ```
3. 查詢可用的指令
    ```shell
    adb
    ```
4. 查詢已連接的裝置
    ```shell
    adb devices
    ```
    ![image4](image4.png)
5. 進入手機
    ```shell
    adb shell
    ```
    ![image5](image5.png)

接下來你可以在裡面到處逛逛，你會發現當你想對一些較重要的檔案存取時，會顯示Permission denied，這表示你權限不足。一般沒有root過的手機是不會有最高權限的。如果想嘗試，可以試試開一些版本較低的虛擬機，有些預設有root權限。

# 手機 Shell 指令參考
Shell 是跟 Linux 溝通的介面。製造商不同，手機內建的 shell 也可能不同。以 Pixel 6a 為例，內建 shell 是 sh。

- 列出目錄/檔案
    ```shell
    ls
    ```
- 移動
    ```shell
    cd [路徑]
    ```
- 查看目前所在路徑
    ```shell
    pwd
    ```
- 查看檔案內容
    ```shell
    cat [檔案名稱]
    ```
- 新增資料夾
    ```shell
    mkdir [資料夾名稱]
    ```
- 查看裝置cpu和內存占用情況
    ```shell
    top
    ```
    
# 補充

這邊列出幾個大家可能比較有興趣的路徑

- 手機內建的App
```
/system/app/
```
- 可用的指令
```
/system/bin/
```
- SDCard
```
/sdcard/
```
- 使用者的檔案、照片
```
/storage/sdcard0/
```
