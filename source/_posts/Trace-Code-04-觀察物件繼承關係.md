---
title: '[Trace Code] 04-觀察物件繼承關係'
date: 2024-07-27T19:11:27+08:00
tags:
- 16th鐵人賽
- Android Studio
- Trace Code
- Hierarchy
---

# 情境
閱讀程式碼是工程師的日常，當程式碼規模日漸成長，許多程式不可避免的被封裝在底層/共用層。當問題被藏的越底層，追查問題就會變得更困難。

為此，Android Studio 也有提供方便的工具讓開發者能夠輕鬆觀察物件的繼承關係。
<!-- more -->

本文推薦自備具有多層繼承結構的專案。或是可以使用我的 android-basics-kotlin-mars-photos-app，但我的範例只有一層繼承，較無法凸顯物件多層繼承的複雜關係。
Github: [https://github.com/dreambo4/android-basics-kotlin-mars-photos-app](https://github.com/dreambo4/android-basics-kotlin-mars-photos-app)

# 工具介紹
Hierarchy 是由 IntelliJ 提供的功能，透過這個工具開發者可以檢查類別、方法和呼叫的層次結構，並探索原始碼的架構。工具通常在側邊工具列，但我建議直接使用快捷鍵。
![position](position.png)

快捷鍵(MacOS)：
- Type Hierarchy: Ctrl + H
- Method Hierarchy: Shift + Cmd + H
- Call Hierarchy: Ctrl + Opt + H

只需對著 Class 或 Method/Function 直接按下快捷鍵，就可以可以看到物件繼承的關係。有時候，某個 function 不一定是在當下這個 class 被呼叫，而是在更底層的 parrent class。這個工具就能幫助我們省去一層一層點擊，尋找繼承關係或是 function 呼叫時機的功夫。

![demo](demo.png)

## 工具優缺
- 優點
  - 快速視覺化查看複雜的繼承結構
  - 節省追蹤 Function 定義和呼叫的時間
  - 提供清晰的程式碼結構概覽

- 缺點
  - 初次使用時可能需要一點時間學習

# 參考資料
- https://www.jetbrains.com/help/idea/2024.1/viewing-structure-and-hierarchy-of-the-source-code.html?reference.toolWindows.hierarchy

