---
title: '[發佈] 01-快速發佈測試 APP - Firebase App Distribution'
date: 2024-09-10T20:21:54+08:00
tags:
- 16th鐵人賽
- Firebase
- APK
---

# 情境
在 APP 正式對外發布前，都會經過好幾輪測試。而這些測試用的 APK，我們通常會用 Firebase 的 App Distribution 來發佈和管理。今天主要說明，如何將 Android APP 發佈到 App Distribution，讓 測試人員下載。

因為我很喜歡以前寫的這個小專案 [Notification_LED](https://github.com/dreambo4/Notification_LED)，希望遇到手機有 LED 燈的人，都可以把 APK 發給他😆，所以今天的目標就是把這個專案上到 App Distribution！
<!-- more -->

# 工具介紹
Firebase App Distribution 可讓您輕鬆將應用程式發行給信任的測試人員。若專案還沒到商店發佈階段，但又有發布 APP 的需求，就很適合使用 App Distribution。**但要特別注意的是，APK 只能在平台上保留 3 個月**。

## 使用步驟
步驟分為兩大部分，第一步是建立 Firebase 專案，需要使用 Firebase 功能的，都可以參考這段步驟。第二段是將 APK 發布到 App Distribution。

### 將 Firebase 加入專案
Firebase Console: https://console.firebase.google.com/

- 第一步，建立 Firebase 專案，Firebase 的介面現在已經比較親民、清楚了，基本上只要照著指示就能成功建立專案。
  - ![建立 Firebase 專案](建立Firebase專案.png)

- 第二步，將 Firebase 新增到應用程式。
  - 5: 若沒特殊需求，可以使用原有的 Firebase 帳號 + 「自動建立新資源」
  - 6: Android 套件名稱要輸入 `build.gradle(:app)` 裡面的 `applicationId`。
  - 7: 依照指示將檔案放到指定位置。因為這個檔案裡放了 APP 的相關資訊，不建議放到公開 Git，建議加入 `.gitignore`。
  - 8: 每個人的 gradle 可能不太一樣，若有問題，建議整段貼給 AI 請他寫。或是參考我專案中的這個 [commit](https://github.com/dreambo4/Notification_LED/commit/ef94c141309a33e6c438785a04ea4b941ce0823f)。
  - ![Firebase 新增到應用程式1](iFirebase新增到應用程式1.png)
  - ![Firebase 新增到應用程式2](iFirebase新增到應用程式2.png)

### 發佈 APK 到 App Distribution
1. 側選欄中找到 App Distribution
2. 直接將檔案拖進網頁上傳
3. 輸入發佈對象的 Email，不限於 gmail，試過 Hotmail、Yahoo 都行，重點是對象手機能收信的信箱。
4. ![App Distribution](AppDistribution.png)
5. 受發布對象會收到一封 Mail，引導下載 `App Tester`，之後就能透過這個 APP 下載 APP Distribution 的 APP 了。 

## 工具優缺
- 優點
  - 發布前，不像商店需要經過審核
  - 快速發佈給測試人員
- 缺點
  - APK 只能保留 3 個月

# 參考資料
- Firebase App Distribution: https://firebase.google.com/docs/app-distribution?hl=zh-tw
- 將應用程式套件版本發布給測試人員 - 程式碼研究室: https://firebase.google.com/codelabs/appdistribution-app-bundles?hl=zh-tw#0
