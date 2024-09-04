---
title: '[Debug] 02-在 Debug 時，靈活運用 Log & Toast'
date: 2024-08-27T23:11:44+08:00
tags:
- 16th鐵人賽
- Android
- Log
- Toast
---

# 情境
Log 和 Toast 都很常被用來印出資訊，本篇會比較兩個物件的使用差異，分別介紹適合的情境。
<!-- more -->

# Log 介紹
用於印出 Log，並可在 Logcat 工具中觀察。
Log 有不同等級 Assert、Error、Warning、Info、Debug、Verbose，我們可以依重要程度使用相應等級的 Log。等級是我們用來篩選 Log 的重要依據之一，隨意使用可能會造成後續維護的困擾。

{% note info %}
## WTF 小彩蛋🥚
你用過這個嗎？
```java
Log.wtf(String tag, String msg) 
```
`wtf` 絕對不是你想的那個 WTF，官方說明是 **What a Terrible Failure**，用來表示**不可能發生的狀況**，會印出 Assert 等級的 Log。
{% endnote %}

# Toast 介紹
![Toast 介紹](Toast.png)

Toast 是在螢幕下半部，一個可以顯示資訊的小小 View。通常用來在盡量不影響使用者的操作下，通知某些狀態或訊息。雖然在使用者體驗方面，官方已經不那麼推薦 Toast，但這不妨礙我們拿它來 debug!

> 官方：</br>如果您的應用程式位於前景，請考慮使用 [snackbar](https://material.io/components/snackbars) 而不要使用浮動式訊息。Snackbar 包含使用者可操作的選項，可為應用程式提供更優質的使用體驗。</br>如果應用程式在背景執行，而您希望使用者採取某些動作，請改為傳送通知。

# Log vs Toast 使用差異
| **功能/特性**    | **Log**                            | **Toast**                                                |
| ---------------- | ---------------------------------- | -------------------------------------------------------- |
| **Context 需求** | 不需要 Context，任何地方皆可使用   | 需要 Context，僅能在有 Context 的地方使用                |
| **執行緒要求**   | 可在任何執行緒中使用               | 必須在主執行緒（UI 執行緒）中使用                        |
| **主要用途**     | 記錄日誌供開發者除錯               | 向使用者顯示短暫的通知或操作結果                         |
| **輸出位置**     | 在 Logcat 中查看，需要開發環境支持 | 直接在手機螢幕上顯示，使用者（包括非工程師）可以直接看到 |
| **顯示效果**     | 不影響使用者介面                   | 會在螢幕上短暫顯示，可能干擾使用者操作                   |

## 實際案例
有些資訊其實對於整個系統的運作很重要，但不一定會顯示在 UI 上(例如，訊息id)。有時候，後端或QA的夥伴在比對資料時需要這些資訊，那我就會考慮用 Toast 的方式將這些資訊印出來。
![實際案例](實際案例.png)

前面是在前端的案例，接下來舉個適合使用 Log 的案例。若是在底層打 API 的部分，想要加個 Timmer 自行控制 Timeout 時間。因為不是在 UI 執行緒，那麼印出當前秒數的功能就比較適用 Log。

# 參考資料
- Log: https://developer.android.com/reference/android/util/Log
- 浮動式訊息總覽: https://developer.android.com/guide/topics/ui/notifiers/toasts?hl=zh-tw

