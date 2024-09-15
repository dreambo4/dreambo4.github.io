---
title: '[版本控管] 03-使用 Merge 和 Rebase 合併的差異'
date: 2024-09-14T16:57:22+08:00
tags:
- 16th鐵人賽
- Git
---

# 情境
在團隊開發中，經常會遇到這樣的情況：當你在某個分支上進行開發並準備推送（push）你的 commit 時，發現同一分支上已經有其他人的 commit 被推送上去了。在這種情況下，你無法直接推送自己的 commit，因為會產生衝突。此時有兩種常見的解決方法：Merge 和 Rebase，這兩者都可以用來整合你和其他人所做的程式變更。
<!-- more -->

# Merge 和 Rebase
![origin](origin.png)

## Merge
Merge 是將另一個分支的變更合併到你當前的分支。Merge 會保留兩個分支的歷史紀錄，並且會產生一個新的 commit，記錄此次合併過程。

- 主要特點：會紀錄合併歷史、衝突檔案。合併的結果會產生一個新的合併 commit，這個 commit 是兩條分支的「交點」。

### 使用 Merge
1. Pull 遠端程式，合併進本地本
![merge1](merge1.png)
2. 可能需要解決衝突
![merge2](merge2.png)
1. Merge 後會有「交點」
![merge3](merge3.png)

## Rebase
會重新改變本地 Commit 點的基準點，變成以遠端最新的異動點為基準，本地 Commit 會變成最新異動點的下一個點，也就相當於整合自己與他人的程式。

- 主要特點：保持分支線簡潔，不會產生額外的合併 commit。

### 使用 Rebase
1. 對著遠端的 Commit 點選 Rebase
![rebase1](rebase1.png)
2. 可能需要解決衝突
![rebase2](rebase2.png)
3. 解決完衝突，完成 Rebase
![rebase3](rebase3.png)
4. Rebase 完不會有交點，也不會有衝突紀錄
![rebase4](rebase4.png)
