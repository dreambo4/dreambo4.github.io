---
title: '[Zenbo開發系列] 07-DDE與App Builder'
date: 2021-08-10 16:42:53
tags:
- Zenbo
- DDE
- 聊天機器人
- 13th鐵人賽
---

研究過程中，要把 DDE 安裝到 Zenbo 的時候，卡關超久...🙃
試過好多方法，當然也包括 App Builder (下面簡稱 AB)。AB 就是像 App Inventor 或 Scrach 的積木程式，可以讓小朋友玩，訓練邏輯。可能是身為 Android 工程師的堅持(?)，本來很抗拒使用積木程式的，但實在卡關太久了，隨便啦，就試試看吧!
<!-- more -->

先說結論，AB 不適合我的使用情境，因為我題庫很多，一個個建積木太累，也很占版面，不好維護。但如果你的對話不多或有比較複雜的槽狀判斷，我會覺得用積木會比在 DDE Input/Output Context 設計，看起來更清楚。

# 註冊專案
Developer > Console > App Management
要選 App Builder 哦！
得到的 APP ID，等下要用。
![project_register](project_register.jpg)

# DDE 語料建置

這部份請參考前面的文章，就不再多說明了。

Concepts 和 Intents 的內容都跟前面要搭配 Zenbo SDK 裝到 Zenbo 的時候一樣，只有 Plans 有點不同。
除了 `ThisPlanLaunchingThisApp` 不用 Input Context 以外，每個 Plan 的 Input Context 都要是不同的字串。Action 不用填，用不到，要回覆的內容寫在 AB 那邊。

## 設定參考

### Info
設定方式參考前面的文章。建立一個新的 Domain UUID。Domain UUID 等下要用。
![info](info.png)

### Plans
![plans1](plans1.png)
![plans2](plans2.png)
![plans3](plans3.png)

# App Builder 專案建置
打開 [App Builder](https://zenbo.asus.com/developer/tools/app-builder.jsp) 建立一個新專案。
彈個手指！就好啦～

![AB](AB.png)

放大圖:
![AB1](AB1.png)
![AB2](AB2.png)
![AB3](AB3.png)
> 因為沒辦法只放圖片，它一定要搭配 Music Sorce，所以就隨便挑一個音樂，音量填 0 就好。
![AB4](AB4.png)

## 專案儲存
![save](save.jpg)
APP ID 和 Domain UUID 在上面註冊專案和 Info 的時候都建好了，複製貼上。

# 安裝
專案儲存後，會得到 ZBA 檔，可以想成是 APK，就是 App 的安裝檔。
可以使用任何方式，只要你能把 ZBA 傳到 Zenbo，影片中我使用的是雲端硬碟。

{% youtube 5J5_-64-Foo %}

## 更新語料(DS Tools)
安裝的時候就會更新一次了，如果 DDE 有修改可以再來這邊更新一次。

{% youtube Qko4bVNGnl4 %}
