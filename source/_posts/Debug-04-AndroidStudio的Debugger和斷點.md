---
title: '[Debug] 04-Android Studio 的 Debugger 和斷點'
date: 2024-09-02T20:07:14+08:00
tags:
- 16th鐵人賽
- Android Studio
- 偵錯
---

# 情境
前面幾天介紹了 Log，但其實除了用 Log 將變數印下來以外，還可以使用 Debugger 即時觀察變數當下的狀況。今天主要會介紹 Android Studio 基本的 Debugger 和 Breakpoint 操作。
<!-- more -->

# Debugger（除錯器）
Debugger 是一種用來測試和除錯程式碼的工具，開發者可以通過它逐步執行程式碼、檢查變數、設置中斷點，並即時觀察程式的行為。這個工具對於識別和修復程式中的錯誤非常有幫助，讓開發者能夠深入理解程式的運行流程，確保程式碼能按照預期的方式運作。

# Breakpoint（斷點）
Breakpoint 是開發者在程式碼中設置的一個特殊標記，用來指示除錯器在程式執行到該點時暫停。當程式停止在中斷點時，開發者可以檢查當前的變數狀態、呼叫堆疊，以及其他相關資訊。這使得開發者能夠逐步執行程式，並且通過檢查程式在某些特定狀態下的表現來縮小問題的範圍，進一步診斷錯誤的根本原因。

## 斷點種類
你可以在需要測試的程式之前插入斷點(參考圖片⬇️)
1. **行斷點(Line breakpoints)**
這兩個都是一般的 `行(ㄏㄤˊ)斷點`，行斷點可以加上條件判斷，例如：我想要斷點停在第二筆訊息的時候。
![Line breakpoints](LineBreakpoints.png)

2. **屬性斷點(Field watchpoints)**
可以觀察 Menber Field 何時被賦值或取值。
![Field watchpoints](FieldWatchpoints.png)

3. **方法斷點(Method breakpoints)**
可以觀察方法何時被呼叫。
![Method breakpoints](MethodBreakpoints.png)

**屬性斷點、方法斷點會大大影響 APP 執行速度**，除非不得已，不然少用，或搭配等下介紹的 `Attach Debugger to Android Process` 使用。

# 啟動偵錯
![Start Debugger](StartDebugger.png)
啟動偵錯工作的按鈕有兩個，可以依據自己的情境搭配使用。
1. Debug 'app': 會重新 build，安裝 APP
2. Attach Debugger to Android Process: 如果應用程式已在裝置上執行，您不必重新啟動應用程式，就可以開始偵錯

而通常開著偵錯模式，會讓 APP 反應稍慢。所以，除非是一開啟 APP 就需要開始偵錯，否則大多時候我會選擇第二種。使用第二種，你可以操作 APP 直到快接近斷點，再開啟偵錯。

# 小結
今天內容很多了，讓我分兩天吧，明天再介紹 Debugger 的各種按鈕。

# 參考資料
- Breakpoints: https://www.jetbrains.com/help/idea/2024.1/using-breakpoints.html
- Debug your app: https://developer.android.com/studio/debug
