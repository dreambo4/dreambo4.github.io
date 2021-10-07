---
title: '[Android APP] 01-架構介紹-MVVM'
date: 2021-10-07 21:40:40
tags:
- 13th鐵人賽
- Android
- MVVM
---

第 23 天，這幾天庫存真的用完了，所以文章都是最新鮮，當天寫的喔!! 剩下 7 天，一起加油吧!

終於來到了最後一個系列「Android APP 系列」，也就是真正裝在 Zenbo 上的「長照小幫手 APP」。很久沒有認真寫一個 APP 了，就當作順便練習，這次我選用了 MVVM 的架構。這個系列會以「長照小幫手」為例，從 MVVM 架構介紹開始，介紹 MVVM 的各個部分和一些系統中比較特別的功能。
<!-- more -->

長照小幫手 完整程式碼: https://gitlab.com/graduate_lab415/chatbot

# MVVM 簡介
Android 目前常見的架構有三種 MVC、MVP、MVVM，而官方目前最推的是 MVVM。
MVVM 官方介紹: [Guide to app architecture](https://developer.android.com/jetpack/guide)

## 轉換架構的心路歷程
其實我早期寫 APP 沒什麼架構的概念，所有程式碼都放在 Activity 裡，造成系統一複雜，程式碼就很髒、很亂。後來接觸了網頁框架(CodeIgniter)，瞭解了 MVC 架構，便也試著把概念放到 Android APP 裡，用類似 MVC 寫了好一陣子。

再後來，專案越來越複雜，經手的人越來越多，程式一樣越改越髒。而且大家一開加入時都是新手，架構分的也不一定那麼清楚，專案還是那麼髒。終於有一天，我們決定正式這個問題，開了個讀書會，瞭解 3 個架構的差異後，我們決定選用 MVVM。大家一起從頭學，確保理解都一樣。

## 模組間的關係

模組化最重要的用意是每個物件職責分明，修改時只要更動相應的 Class，也方便 Class 重複使用。

![mvvm](mvvm.jpg)

- **View**
  - 負責顯示 UI、監聽動作
  - 包含 Layout 的 XML、Activity 類、Fragment 類、Adapter 類
  - 不處理邏輯，只負責顯示資料，接收到點擊事件就請 ViewModel 處理
  - View 和 ViewModel 間通常會使用觀察者模式，由 ViewModel 提供 LiveData 給 View 觀察，只要觀察到有資料變動就更新畫面
- **ViewModel**
  - 負責提供畫面所需資料、邏輯判斷
  - 提供 LiveData
  - 依需求向 Model 存取資料
- **Model**
  - 負責提供資料
  - 通常會叫做 xxxxxRepository
  - 若是資料有多個資料來源(來自 API、來自 SQLite)，Repository 層可以抽象化，變成一個 interface，就像是官方文件上的那樣
  - 圖片取自: https://developer.android.com/jetpack/guide
    ![final-architecture](final-architecture.png)

## 資料夾分類方式
這個好像沒有一定欸，我查過網路上很多資料，分類方式不盡相同，但主要都是以模組類型來分類。這部分不需要太糾結，自己定義清楚，找的到東西就好。

我的分類方式:
- controller: 特殊功能的控制
- repository: 存取 API 相關
- utils: 資料物件
- view: Activity、Adapter
- viewmodel: ViewModel、Callback

# 長照小幫手 程式架構
![架構](架構.png)
