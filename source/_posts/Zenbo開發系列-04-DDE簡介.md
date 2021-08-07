---
title: '[Zenbo開發系列] 04-DDE簡介'
date: 2021-08-07 01:26:56
tags: 
- Zenbo
- DDE
---

這篇主要是我之前看官方文件的筆記，還有對於幾個 Basic Concepts 的理解，可能比較沒有結構一點。建議以官方文件的教學為主，再參考我的筆記，這篇紀錄了我之前不懂地方，希望也能幫到你。

為了寫這篇文章，今天又上去翻了一下官方文件，發現還有在更新呢!

想想之前做要做 DDE 語料，看官方文件踩了不少雷💣
<!--more-->

> 官方文件使用方法:
> - 如果有時間，可以中英文互相參照，有時候兩個版本內容不太相同。
> - 如果有在官方文件找不到說明，嘗試把不同版本的文件互相參照。曾經發現一個我找很久的說明，在舊版本有寫，但在新版本被移除了。
>   - 可是這個功能在系統上還存在欸! 😡
> - 遇到官方文件也沒說明清楚的時候，就只能自己摸索了，加油!

# 筆記開始

> 紀錄時間: 2020/04/25

**<<以下是當初研究時，隨手紀錄不完整也不一定完全正確的筆記，請以官方文件為主>>**

這次是根據這兩份教學文件
- [Template: Hello World](https://zenbo.asus.com/developer/documents/Overview/DDE-Tutorial/Templates/Hello-World)
- [Hello-City-(zh)](https://zenbo.asus.com/developer/documents/Overview/DDE-Tutorial/Quick-Start/Hello-City-(zh))

建置完後發現，上次不能送出應該是因為瀏覽器(firefox🦊)的問題，改用chrome後可以正常送出。

# How to start 導論

[How to start](https://zenbo.asus.com/developer/documents/Overview/DDE-Tutorial/Quick-Start/How-to-start(zh))

> Zenbo 內部因為有口語理解模組 (Spoken Language Understanding / SLU)，將語音辨識資訊轉化為結構化的語意資料，並提供給適當的Domain 處理。

> 人類與Zenbo的對話是透過一連串的Intent(意圖)語句組成。Concept(概念)則是語句的詞彙，而Plan(流程)則是負責串起語句之間的流程來建立一段完整對話。

User在問答中的語句為Intent，Intent中的詞彙為Concept。

# Info

![Untitled.png](Untitled.png)

塗掉的那幾欄如果需要發佈才要填的

![Untitled1.png](Untitled1.png)

# Plans

撰寫這份筆記時，最新版文件是 `v1.1.4` 。( [ASUS DDE - Plans](https://zenbo.asus.com/developer/documents/Overview/DDE-Tutorial/Basic-Concepts/Plans) )

因舊文件的說明較詳細，部分筆記有參考v1.1.3、v1.1.2。

這邊就是要回答的文字，應該翻叫「計畫」，「計畫」是將一組事件對應到一系列的動作。

UtteranceToLaunchApp 是要開啟 APP 的 Plans

![Untitled2.png](Untitled2.png)

## PlanID

每個plan要有唯一id

## Is the plan able to launch the app?

- true: 可以啟動App
- false: 不行

## Event
event的CSR是「語音辨識結果」

![Plans1](Plans1.png)
![Plans2](Plans2.png)

# Intents

撰寫這份筆記時，最新版文件是 `v1.1.4` 。( [DDE Tutorial - Intents](https://zenbo.asus.com/developer/documents/Overview/DDE-Tutorial/Basic-Concepts/Intents) )

可以設定多種句型，應該翻叫「意圖」。

因舊文件的說明較詳細，部分筆記有參考v1.1.3、v1.1.2。

人們可能使用不同句子來表達自己的意圖，因此開發人員有責任枚舉所有可能的句子。 <- 官方文件寫的

> BrandName = 品牌名，ex: 華碩

> VoiceTag(App Name) = APP名稱，ex: 長照

![Untitled3.png](Untitled3.png)

![Untitled4.png](Untitled4.png)

# Concepts

撰寫這份筆記時，最新版文件是 `v1.1.4` 。( [DDE Tutorial - Concepts](https://zenbo.asus.com/developer/documents/Overview/DDE-Tutorial/Basic-Concepts/Concepts) )

我會把他翻作「概念」，大概就是可以將很多同意詞群組起來的。在 Dialoflow 叫 Entities。

![Untitled5.png](Untitled5.png)
![Untitled6.png](Untitled6.png)
![Untitled07.png](Untitled7.png)

## Type
選項有： `Class` 和 `Phrase`
文件建議選 `Class` ，但未解釋`Phrase` 的用途。

> 文件 v1.1.3 提到，若是使用class，所有的實例都要是類別；若使用phrase，所有實例都要是片語。

# Publish

右上有publish按鈕

![Untitled8.png](Untitled8.png)

# Tests

右方有輸入框可以測試

要用Chrome!!

![Untitled9.png](Untitled9.png)

# 參考資料
## 學習資源
- [Home Robot / Zenbo (APP Builder / DDE Editor)](https://sites.google.com/site/goofoo777/106_1-jiao-xue-ke-cheng/home-robot)
- [Zenbo機器人開發者社群](https://www.facebook.com/groups/zenbo.dev)
- [分享_基於Zenbo語音的多機協作開發技術_ok](https://www.facebook.com/groups/zenbo.dev/permalink/1567101126726820)

## 相關文獻
- [AI機器人、藍芽與Android整合開發技術](https://www.books.com.tw/products/0010809325)
  - 推這本書👍，裡面有介紹不同機器人間互動時程式設計的架構，還有 Zenbo SDK 的 Sample Code。可以寄信向作者高煥堂老師索取完整原始碼。
- [智慧家庭陪伴系統 (專題)](https://www.csie.nuu.edu.tw/wp-content/uploads/2019/09/2018-%E7%8E%8B%E8%83%BD%E4%B8%AD-%E5%B0%88%E9%A1%8C.pdf)
- [銀髮族使用Zenbo機器人服務體驗洞察研究](https://hdl.handle.net/11296/x4x8c6)
- [陪伴型機器人使用者經驗評估─以智慧居家機器人Zenbo為例](https://www.airitilibrary.com/Publication/alDetailedMesh?DocID=23061790-201809-201810220006-201810220006-265-282)
