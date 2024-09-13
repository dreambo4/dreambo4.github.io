---
title: '[版本控管] 02-暫存程式碼-Git Stash vs IntelliJ Shelf'
date: 2024-09-13T19:22:54+08:00
tags:
- 16th鐵人賽
- Git
---

# 情境
常常功能寫到一半，突然來了插件，功能寫到一半，也不適合 commit。只能把寫到一半的程式暫存起來，切換工作任務。今天就要來介紹暫存程式的方法～
<!-- more -->

# Shelf 和 Stash 介紹
其實 Shelf 和 Stash 都可以用來暫存檔案。今天要來介紹兩者差異，和平常適合應用的場景。

## Stash
Stash 是 Git 提供的功能，可以將尚未 commit 的異動都暫存起來。缺點是 Stash 的範圍預設是所有異動內容，而且 Sourcetree GUI 沒有提供直覺的操作介面，只能全部暫存。

Stash 的優點是，可以將 Stash 點推上 Git，這部分我沒使用過，若有特殊情境可以嘗試看看。

## Shelf
Shelf 是 IntelliJ 提供的功能，可以針對檔案或檔案中的每塊異動，選擇暫存範圍。

也可以搭配 IntelliJ 的 Change List 使用。例如可以建立包版專用的 Change List，有些設定平常不需要開，可以把整個 Change List 存到 Shelf，包版時再拿出來，就不影響日常開發。

![Change List 1](ChangeList1.png)
![Change List 2](ChangeList2.png)

# 參考資料
- Shelve or stash changes: https://www.jetbrains.com/help/idea/shelving-and-unshelving-changes.html