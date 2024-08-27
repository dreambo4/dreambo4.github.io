---
title: '[Debug] 01-Android Studio Logcat 使用技巧：寫好 Log、找對 Log'
date: 2024-08-26T18:42:33+08:00
tags:
- 16th鐵人賽
- Android Studio
- Log
---

# 情境
寫程式除了要會寫 Log，還要會找 Log、看 Log、整理 Log。今天會介紹幾個我寫 Log 的原則，希望對你也有幫助。

# Logcat 介紹
Android Studio 在 2022 年的 Electric Eel 版，為 Logcat 工具做了大更新。修正了以往一閃退(APP關閉)，就看不到 Log 的問題，不同的篩選條件也能組合使用。雖然比以前的版本學習難度更高，但熟練後就能更精準的篩選需要的 Log。
<!-- more -->

> Android Studio 的「Logcat」視窗可即時顯示裝置記錄，協助您對應用程式進行偵錯。這些記錄包括您以 Log 類別加到應用程式中的訊息、在 Android 執行的服務的訊息，或在執行垃圾收集等作業時顯示的系統訊息等。只要應用程式擲回例外狀況，Logcat 就會顯示訊息，然後提供內有該行程式碼連結的相關堆疊追蹤記錄。

## 看 Log
![Logcat介面功能介紹](Logcat介面功能介紹.png)
**介面功能介紹：**
- 分頁：可以新增多個分頁，追蹤不同 Filter
- 裝置：有多個裝置時，可以切換裝置
- Filter：Filter 條件，等下會詳細介紹
- 加入常用 Filter：可以儲存常用的 Filter 組合
- 置底：快速滑動到最底部，追蹤最新一筆 Log
- 文字過長是否換行：Log 過長時，切換是否自動換行，於可是範圍內顯示完整內容
- Log 模式切換：Log 有 Standard(詳細)模式、Compact(精簡)模式，並且可以透過 `Modify Views` 調整輸出欄位
- 分割視窗：在同一個分頁中可以分割成多個視窗，方便比較
- 截圖、螢幕錄影：兩個很方便的小功能，讓你不需要在手機上截圖或錄影再傳到電腦上，一且都可以在電腦操作解決

## 寫 Log
- **無意義的 Log 不留**
在開發期間，寫了一堆 Debug 用的 Log 在所難免，但請勿將這些無意義的 Log 推上 Git。舉例：你可能會把一個 ArrayList 的內容用迴圈一個一個 Log 出來，但這些內容只在你當下開發時有用，對於後續維護沒有意義的 Log 不需要保留。</br></br>建議大家設定一個專屬的 Tag(如 `YRYR`)來標示臨時的 Log，在推 Code 之前全域的搜尋一下，確定是否有遺漏未刪除的 Log。(建議你也可以自己定一個喔)

- **保留關鍵狀態 Log**
通常我只會保留需要明確知道當下狀態的 Log，例如：打 API 的 Request/Reponse、存檔成功/失敗。

- **Tag 取檔名、物件名**
通常確定要保留的 Log，會取檔名或物件名當作 Tag，這樣即使 Log 變多，也能快速定位 Log 來源。

## 查 Log
Debug 期間，我寫的所有 Log，基本上都會用我專用的 Tag。
所以我的 Filter 會寫這樣：
```
package:mine tag:YRYR
```
再來，只看特定 Tag 的話，可能會不小心忽略錯誤訊息，所以再加上顯示 Error Message：
```
package:mine tag:YRYR level:error 
```
而通常功能都會搭配 API 使用，所以我還要再看一些 XXXRepository 的內容。而且前面有提到，每個 Repository 的 Tag 都是使用檔名標示，所以當我寫 `tag:Repository`，就包含所有 Repository 的內容：
```
package:mine tag:YRYR level:error tag:Repository
```
或是今天就只想看 API 相關的 Log:
```
package:mine tag:Repository
```

### 組合使用
若今天有兩組資料想同時查看，也可以使用 `分割視窗` 功能。通常我會下兩組 Tag，`YRYR1`、`YRYR2`，那麼左右的分割視窗可以個別看兩個標籤：
```
# 視窗一
package:mine tag:YRYR1
# 視窗二
package:mine tag:YRYR2
```
會分別將兩個標籤定成 `YRYR1`、`YRYR2`，是因為若當我需要一個視窗同時看到兩個 Tag 的時候，就能使用這樣的搜尋條件：
```
package:mine tag:YRYR
```
{% note info %}
tag:YRYR 是指 Tag 包含 "YRYR" 的標籤，自然也包含 "YRYR1"、"YRYR2"
{% endnote %}

# 小結
本篇著重於介紹專案中的 Log 規則與篩選應用，條件篩選還有很多進階的寫法，例如下圖中的 `=`、`~`、`-`。建議有空把 [官方文件](https://developer.android.com/studio/debug/logcat?hl=zh-tw) 讀一遍。
![篩選條件](篩選條件.png)

# 參考資料
- 使用 Logcat 查看記錄: https://developer.android.com/studio/debug/logcat?hl=zh-tw