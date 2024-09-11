---
title: '[發佈] 02-功能強大的輕量級當機回報 - Crashlytics'
date: 2024-09-11T18:46:52+08:00
tags:
- 16th鐵人賽
- Firebase
- Crashlytics
---

# 情境
接續上篇 [[發佈] 01-快速發佈測試 APP - Firebase App Distribution](https://dreambo4.github.io/2024/09/10/%E7%99%BC%E4%BD%88-01-%E5%BF%AB%E9%80%9F%E7%99%BC%E4%BD%88%E6%B8%AC%E8%A9%A6APP-Firebase-App-Distribution/)，已經可以提供 APP 給他人測試，接下來我們需要追蹤使用者遇到的閃退問題。
<!-- more -->

# Crashlytics 介紹
Firebase Crashlytics 是一款輕量級的即時當機回報器，可協助您追蹤、排序和修正會損害應用程式品質的穩定性問題。Crashlytics 能智慧地將當機事件分組，並找出導致當機的原因，幫您節省寶貴的除錯時間。
- 了解特定當機是否影響大量使用者
- 在問題嚴重性突然升高時收到警報
- 並精準找出導致當機的程式碼

## 設定步驟
開始使用 Crashlytics 之前，需要先建立 Firebase 專案。這部分之前寫過，這篇就不再重複。
- 請參考：[[發佈] 01-快速發佈測試 APP - Firebase App Distribution#將 Firebase 加入專案](https://dreambo4.github.io/2024/09/10/%E7%99%BC%E4%BD%88-01-%E5%BF%AB%E9%80%9F%E7%99%BC%E4%BD%88%E6%B8%AC%E8%A9%A6APP-Firebase-App-Distribution/#%E5%B0%87-Firebase-%E5%8A%A0%E5%85%A5%E5%B0%88%E6%A1%88)

### 專案導入 Crashlytics
參考 [官方文件](https://firebase.google.com/docs/crashlytics/get-started?platform=android&hl=zh-tw#java)，在 Gradle 加入相關設定。或是參考這個 [commit](https://github.com/dreambo4/Notification_LED/commit/56585ed1885cacd4623409e4b76f5ce4332052f0) 點。

接下來只要使用者閃退，我們就能透過 Crashlytics 尋找可能的問題。並且觀察遇到問題的使用者數量。
{% note info %}
應用程式閃退，下次重新開啟時，才會傳送當機事件到 Firebase。
{% endnote %}
![Crashlytics](Crashlytics.png)

### Crashlytics 介面說明
點進問題後，可以看到這樣的頁面
- 右上按鈕
  - 關閉：若確認問題已修正完畢，可以將問題設為關閉。若問題在下一版本再次出現會被標示為「回歸問題」，方便我們追蹤問題修復狀況。
  - 附註：可以附註問題原因、說明等。
- 事件摘要：這邊可以看到 APP版本、作業系統版本、裝置型號、時間，可以幫助工程師快速縮小問題範圍。這就是為什麼回報問題時，都會要求提供這些資訊。
- 問題 Call Stack：這邊的錯誤訊息基本跟 Logcat 看到的相同，可以用來確認＆修正問題。
![Problem](Problem.png)

## 工具優缺
- 優點
  - 可以明確知道使用者閃退位置，不需要在通靈使用者的描述。
  - 可以追蹤每個問題的修復狀況。
- 缺點
  - 初次將 Crashlytics 導入專案，Gradle 配置需要點時間。
  - 學習從 Firebase 過濾出特定問題，需要一點經驗和嘗試。

# 參考資料
- Firebase Crashlytics: https://firebase.google.com/docs/crashlytics?hl=zh-tw
- 開始使用 Firebase Crashlytics: https://firebase.google.com/docs/crashlytics/get-started?platform=android&hl=zh-tw
