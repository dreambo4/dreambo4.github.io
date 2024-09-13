---
title: '[版本控管] 01-從 Git CLI 到 GUI'
date: 2024-09-11T23:55:42+08:00
tags:
- 16th鐵人賽
- Git
---

# 情境
使用 Git 可以算是工程師的基本功，是管理版本和團隊開發的基礎。而 Git 的操作介面基本上分為兩種：CLI、GUI。
<!-- more -->

# Git 工具介紹
## Git CLI - 文字指令介面
其實我推薦新手先從 CLI 指令學起(就如同我被訓練的那樣)
- 使用指令，可以讓你更專注了解目前的步驟，了解 Git 的整個流程。
- GUI 工具其實也是基於 CLI，先學會指令，未來比較能了解原理融會貫通。
- 使用 CLI 比較沒有工具限制，未來若有機會在主機上部署程式，Linux Server 是不可能裝 GUI 的。

Git 基本指令教學(請跳過 Merge):
https://hackmd.io/LSFaNQyYRK23AGneWYitsA#/

## Git GUI - 漂亮圖形化介面
### GitKraken
我第一次接觸 Git GUI 是實習的時候，那時候使用 Github Student Pack 獲得一年的 GitKraken Pro，也是第一次完整的跑 Gitflow。

![GitKraken](GitKraken.png)
圖片來源：https://www.gitkraken.com/blog/best-git-%e5%ae%a2%e6%88%b7-%e7%ab%af-windows-macos-linux

- 優點
  - 直覺的 Undo/Redo 按鈕，可以復原動作，讓人覺得安心。
  - 在分支圖上面，可以清楚看到 Stash 紀錄。
- 缺點
  - 免費版限制多，基本非公開專案不太能用

### SourceTree
到公司上班後，開始改用 SourceTree。我覺得是一個簡單、基本功能齊全的工具。若沒預算訂閱，SourceTree 也會是一個不錯的工具。

![SourceTree](SourceTree.png)
圖片來源：https://www.sourcetreeapp.com/

# 參考資料
- GitKraken: https://www.gitkraken.com/
- GitHub Student Developer Pack: https://education.github.com/pack
  - 可以獲得超多學生專屬優惠，學生們一定要記得上去領取。
- Sourcetree: https://www.sourcetreeapp.com/
