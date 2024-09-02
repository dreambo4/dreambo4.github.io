---
title: '[Debug] 03-用 Database Inspetor 即時觀察 SQLite'
date: 2024-09-01T20:37:35+08:00
tags:
- 16th鐵人賽
- Android Studio
- SQLite
---

# 情境
專案中使用到 SQLite，要如何確定資料修改是否成功，或是查看 SQLite 內容。你知道 Android Studio 有提供方便的工具嗎？

Demo 程式 GitHub: https://github.com/dreambo4/messageboard-app
<!-- more -->

# Database Inspetor 介紹
Database Inspetor 是 Android Studio 4.1 版 (2020 年 8 月) 才有的功能。古早時代，我們需要把 SQLite 匯出，再使用 Browser 工具檢查 SQLite 內容。
- DB Browser for SQLite: https://sqlitebrowser.org/

自從有了新工具，這一切就方便多了。Database Inspetor 是 Android Studio 內建的小工具。讓你在應用程式運行時查詢和修改應用程式的資料庫。這對於資料庫除錯特別有用。Database Inspetor 可以與純 SQLite 以及基於 SQLite 的庫（如 Room）一起使用。要特別注意的是，這個工具限制 Android 8.0 (API level 26) 以上的裝置才能使用。

實測只有開 Debuggable 的 APP 才能用，若只有開 Profileable 是看不到的。
- Debuggable 和 Profileable 設定與差異，請參考：[[Trace Code] 01-使用Profiler檢查當前所在Activity/Fragment](https://dreambo4.github.io/2024/06/30/Trace-Code-01-%E4%BD%BF%E7%94%A8-Profiler-%E6%AA%A2%E6%9F%A5%E7%95%B6%E5%89%8D%E6%89%80%E5%9C%A8-Activity-Fragment/#Debuggable-%E5%92%8C-Profileable-%E7%9A%84%E8%A8%AD%E7%BD%AE)

## 使用步驟
1. 在 Android Studio 側邊工具列中選擇 App Inspection
2. 點擊 Database Inspector

只要你的 APP 有用到 SQLite，就能透過工具看到資料庫狀況。
![Database Inspector](DatabaseInspector.png)

### 測試 SQL
主要有兩種測試方式
- 第一種：若你的 Dao 裡有寫 SQL，可以透過左邊的小 icon 執行 SQL。
- 第二種：點選 `Open New Query Tab`，也能自己隨意輸入 SQL 條件。

![Test SQL](TestSQL.png)

### Live Update 功能介紹
- 勾選：此時 Database Inspector 資料是 read-only(只能看不能修改)。資料內容會跟手機資料同步，只要手機資料異動，就會看到更新。
- 未勾選：此時 Database Inspector 資料可以編輯。只要在電腦端修改，手機上的內容就會馬上更新。(建議搭配 LiveData 才能達到即時顯示的效果)

### 操作影片：
{% youtube dsxmOH8Laew %}

# 參考資料
- androidx.room.RoomDatabase: https://developer.android.com/reference/androidx/room/Room
- Debug your database with the Database Inspector: https://developer.android.com/studio/inspect/database