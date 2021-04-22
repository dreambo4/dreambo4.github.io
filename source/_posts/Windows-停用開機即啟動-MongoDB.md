---
title: Windows 停用開機即啟動 MongoDB
date: 2021-04-22 14:21:32
tags:
---

最近發現之前裝的 MongoDB，會在電腦開機時執行，還找不到地方關掉開機啟動的設定，只能手動關閉。網路上大家問的都是如何在 Windows 上開機執行 MongoDB，沒有人跟我一樣，有如何關閉的問題嗎？Google 了好久，才找到這篇 [How to stop mongodb server on Windows startup?](https://stackoverflow.com/questions/45011195/how-to-stop-mongodb-server-on-windows-startup)

## 手動開啟/關閉

以管理員身份執行 cmd
```shell
net start MongoDB
net stop MongoDB
```

## 停用開機執行

### 打開 services.msc

按下 `win+R` 顯示執行視窗，輸入 `services.msc`

![執行](services_msc.png)

![服務](服務.png)

### 修改啟動類型

將啟動類型更改為 **手動**

![mongodb_內容](mongodb_內容.png)

### 完成
以後電腦重啟，就不會再看到 MongoDB 被默默啟動囉！
