---
title: '[Debug] 05-Android Studio 的 Debugger 操作'
date: 2024-09-04T19:03:32+08:00
tags:
- 16th鐵人賽
- Android Studio
- 偵錯
---

# 情境
接續前一篇，昨天介紹啟動斷點的種類和偵錯的啟動方式，今天要介紹 Debugger 的基本操作方式。
<!-- more -->

# Debugger 介紹 & 使用步驟
1. 首先在想要偵錯的地方插上斷點，開啟偵錯模式
2. 當程式跑到斷點的行數，就會卡住
3. 接下來就能用下方介紹的按鈕，一行一行觀察程式執行狀況。

![Debugger](Debugger.png)
功能按鈕的介紹(由左而右):
![Buttons](Buttons.png)
1. Rerun 'app': 以偵錯模式，重新執行 APP
2. Stop 'app': 停止偵錯
3. Resume Program: 卡在斷點時，繼續執行到下一個斷點
4. Pause Program: 程式運行到一半，但還沒卡在斷點，可以暫停到現在執行的地方
5. Step Over: 下一行
6. Step Into: 進入 function
7. Step Out: 離開現在的function，往上一層
8. View Breakpoints...: 顯示所有斷點
9. Mute Breakpoints: 暫時略過所有斷點

在程式旁邊可以直接看到
![LineWatch](LineWatch.png)

上面的輸入框可以讀取到現有的變數，也可以對變數執行一些程式。或是按一下右邊的 Add to Watches，可以加入下方區塊，隨時觀察變數狀態。
![AddToWatch](AddToWatch.png)

# 參考資料
- Debug code: https://www.jetbrains.com/help/idea/2024.1/debugging-code.html
- 為應用程式偵錯: https://developer.android.com/studio/debug?hl=zh-tw
