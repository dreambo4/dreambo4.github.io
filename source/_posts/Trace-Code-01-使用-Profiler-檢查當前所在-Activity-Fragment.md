---
title: '[Trace Code] 01-使用Profiler檢查當前所在Activity/Fragment'
date: 2024-06-30T15:55:28+08:00
tags:
- 16th鐵人賽
- Android
- Trace Code
---

# 情境
- 當收到需求，需要在某一頁多加一個頁籤時，我們需要快速找到需要調整的 Activity 或 Fragment。
- 當某個畫面由多個 Fragment 組合而成時，如何確認畫面上有哪些 Fragment？
- 有多個相像的 Activity 或 Fragment，如何快速確認當下顯示的是哪一個？

要如何快速搜尋到當前 Activity 或 Fragment 以修改程式呢？Profiler 可以幫助我們即時觀察當前頁面。
<!-- more -->
我做了一個 Demo APP，歡迎下載自行嘗試。
GitHub: [https://github.com/dreambo4/NavigationDemo](https://github.com/dreambo4/NavigationDemo)

# 工具介紹
首先，觀察一下頁面。SettingFragment 裡面嵌入了 SubSetting1Fragment 和 SubSetting2Fragment。
![SettingPage](SettingPage.png)

## 使用 Profiler 的步驟
- 確保已安裝 Android Studio 並配置好開發環境。
- 在 Android Studio 中，打開 Profiler 工具，通常位於側邊欄。
- 點擊 + 按鈕(Start a new profiling session.)，然後選取你的裝置和 APP。
    - ![ProfilerPath](ProfilerPath.png)

隨著頁面的切換，我們可以觀察到 Profiler 可以顯示當前的 Activity 與 Fragment。即使頁面上有多個 Fragment，也可以一併顯示。
![Profiler](Profiler.png)

## Debuggable 和 Profileable 的設置
若從 Profiler 觀察不到頁面，建議確認一下 debuggable 和 profileable 的設定

專案在預設狀況下：
- build varient 是 debug 的時候，debuggable 和 profileable 都是 true
- build varient 是 release 的時候，debuggable 和 profileable 都是 false

不過這些設定都是可調整的

**debuggable** 可在 gradle 調整 true/false，用來設定應用程式是否允許使用調試工具（如 Android Studio 的 Debugger）進行調試。但這個模式只應在開發階段使用，因為它使應用程式容易受到攻擊。如果在 release 環境中啟用，可能會暴露敏感資訊和應用程式內部邏輯。
![debuggable](debuggable.png)

**profileable** 可在 manifest 調整，是 Android Q（API 29） 引入的一個 manifest 標籤，用於指定應用程式是否允許在不設置 debuggable 的情況下進行性能分析。與 debuggable 相比，profileable 更加安全，因為它僅限於性能分析，不允許調試操作。因此，它可以在 release 環境中啟用，以便進行現場性能分析而不危及應用程式的安全性。
![profileable](profileable.png)

> 雖然開啟 profileable 允許應用程式性能分析，但經過實測 debuggable = false, profileable = true 的情況下，雖然還是可以從 Profiler 觀察到部分資訊，但無法列出 Activity 或 Fragment。
> 本文介紹的由 Profiler 觀察 Activity 和 Fragment 的方法，僅限於 debuggable = true 的情況下使用。

## 工具優缺
- 優點
    - 幫助我們快速縮小範圍，找到目標 Activity 或 Fragment。
- 缺點
    - 只能找到 Activity 或 Fragment。有時候要找尋的目標程式可能是包在元件 View 裡面或 Adapter 裡，此時就需要再搭配其他工具，像是 Layout Inspector。
    - 僅限於 debuggable 為 true 時使用。

# 參考資料
- https://developer.android.com/studio/profile
