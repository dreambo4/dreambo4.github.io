---
title: '[追查API] 01-出事的是哪隻API-Network Inspector'
date: 2024-08-11T22:10:55+08:00
tags:
- 16th鐵人賽
- Android
- API
---

# 情境
客戶反應進入某個頁面時出現查詢失敗的錯誤訊息，我們首先要確認可能是哪一隻 API，才能請後端的夥伴調出相關 Log 進行分析。本篇文章主要說明如何使用 Android Studio 內建的 Network Inspector，來查看 Request 和 Response 的詳細內容。
<!-- more -->

Demo 程式 GitHub: [https://github.com/dreambo4/android-basics-kotlin-mars-photos-app](https://github.com/dreambo4/android-basics-kotlin-mars-photos-app)

# 工具介紹
Network Inspector 會在時間軸上顯示即時的網路活動，包括傳送和接收的資料。也可讓你檢查應用程式如何以及何時傳輸資料，並適當地最佳化底層程式碼

## 使用步驟
1. 在 Android Studio 側邊工具列中選擇 App Inspection
2. 點擊 Network Inspector

只要在開著 Inspector 的情況下打 API，就能檢查 Request 和 Response 的內容。
![Network Inspector](NetworkInspector.png)

使用這個工具，我便能快速的確認
- 進入特定頁面，會打哪幾隻 API
- API 使用順序為何
- 檢查當下 Response 的速度，是否可能造成 timeout

## 工具優缺
- 優點
  - 詳細的 Request 和 Response 內容展示
  - 有助於性能優化和問題診斷

- 缺點
  - 只適用 HTTP Protocal 的封包(TCP、UDP、MQTT...的封包都不適用)

# 後記
雖然導致客戶看到錯誤訊息的狀況很多，而且很可能是源自後端的錯誤訊息。但作為最貼近客戶的應用端，APP 開發團隊常常是第一個接到問題反饋的。因此，盡快追查可能的 API，並且提供相關訊息給後端的夥伴確認，就是我們的重要任務啦。

當然比較好的作法，應該考慮在錯誤訊息上印出該API的識別代碼，或是平常就應該做成文件，會更方便查閱。

# 參考資料
- Inspect network traffic with the Network Inspector: https://developer.android.com/studio/debug/network-profiler
