---
title: 我的Android工具箱 大綱
date: 2024-04-15 22:33:00
tags:
- Android
- 大綱
- 16th鐵人賽
---

# View

## Day01-Layout Inspector
簡介Layout Inspector 使用

## Day02-手機 顯示佈局界線

## Day03-Profiler


# Network

## Day04-App Inspector-Network Inspector

## Day05-Burp Suite

## Day06-Wireshark

## Day07-Postman


# Decoder

## Day08-JWT

## Day09-JSON Pretty

## Day10-PACAndroid


# Local Storage

## Day11-App Inspector-Database Inspector

## Day12-Share Preference

## Day13-File Explorer


# Trace Code

## Day14-Hierarchy

## Day15-Debugger
- 斷點
    - 斷點的基本操作
    - Exception 的斷點
    - Condition
- Evaluater


# Logcat

## Day16-自定 Filter

## Day17-Log 格式

## Day18-ADB 環境變數

## Day19-Max Line

## Day20-Log 分析
- 從crash list或剪貼簿


# Git 工具

## Day21-Change List + Shelf

## Day22-GUI SourceTree

## Day23-Merge & Rebase


---

30天鐵人賽的目標?
- 整理工作以來，幫助我寫code的那些工具

工作時我最常做的事？
- 開新檔案、寫新功能、寫新需求
- 寫元件
- 拉UI、檢查對齊
- 因應需求改程式、修bug
- 參考同事的code
- 找有沒有同事寫好的元件可以拿來用
- 參考網路上的資料，改成自己的
- 找bug發生原因
- 卡關，插斷點，看原因
- 開Base架構
- 組 Request、拆 Response

這些工具可以幫助什麼？
講Code的文夠多了，這次不講Code，來講工具
# Trace Code: 
- 發現問題後，第一步就是找到事發地點
- 幫助我在收到一個需求和bug時，可以快速定位，知道當前的Layout、Activity、Fragment 程式在哪裡
- 通常以下幾種方式會混著用
    - **Day01 - [Trace Code] 使用 Profiler 檢查當前所在 Activity/Fragment**
        - 快速縮小範圍，如果有幾個Activity/Fragment長得很像，那麼使用 Profiler 就能很快確定究竟是哪一個
        - 缺點：只能找到Activity或Fragment，有時候要找尋的目標程式，可能是包在元件或Adapter裡
    - **Day02 - [Trace Code] 使用 Layout Inspector 找所在 Layout**
        - 可以快速找到顯示錯誤資訊的元件，並且反查，該文字或數字是何時、如何被寫上去，快速往下追查問題
        - 注意：新版已整合進 Running Device，需要獨立的話，可調整設定
    - **Day03 - [Trace Code] 搜尋大法**
        - 以上兩種只能用在有插線的狀況下，很多時候，只有一張截圖
        - 找畫面上固定不會變動的字來搜尋(ex: 標題文字)，通常就能很快找到 Layout或使用的字串資源
    - **Day04 - [Trace Code] Hierarchy**
        - 繼承階乘、Call Stack
- UI
    - 通常會由設計提供 Figma、Zepline 等設計圖
    - 在拉畫面要注意的通常是對齊與顏色是否正確、大小手機跑版滑動範圍
    
    - **Day05 - [UI] 通過UI設計師嚴格的檢查-排版**
        - 「顯示版面配置界限」，手機上簡易檢查 UI 是否對齊、點擊範圍、padding
        - Layout Inspector，檢查元件長寬、visibility
    - **Day06 - [UI] 通過UI設計師嚴格的檢查-文字Baseline**
        - 有時候不能完全照 Figma 上的 Padding 或 Margin，會有中文和英數字型 Baseline 不一樣高的問題
    - **Day07 - [UI] UI設計師不在家，自立自強用滴管取顏色**
        - 有時候設計圖沒有 Figma，只有一張 PNG，又沒給顏色的狀況下，只能用滴管工具，Mac 內建滴管工具，分享哪個選項最準
    - **Day08 - [UI] 使用 Android Studio 內建的 Color Picker 設定顏色**
        - 好處：透明度百分比直接換算 16 進制
    - **Day09 - [UI] Android的原罪-大小不一的裝置**
        - 要注意小手機的滑動範圍，Layout有使用絕對高，需要特別注意
        - 借 Firebase 手機，https://firebase.google.com/docs/test-lab/usage-quotas-pricing?hl=zh-tw#device-streaming 
- Work with Legacy Code
    - 很多時候 Code 不是自己寫的，這時候就需要看別人的 Code
    - **Day10 - [Coding] Android Studio Code Template**
        - PPPP
        - PP
    - **Day11 - [Coding] 寫註解**
        - 寫 Java doc 格式註解的好處
        - 快速看註解
        - 常用 tag
- 追查 API
    - 有時候要快速的追，這頁打了什麼 API，Request、Response 的內容如何、耗時
    - 追 Request、Respone
    - **Day12 - [追查 API] 出事的是哪隻 API**
        - 情境：客戶傳來一張截圖，說明進入頁面時跳出查詢失敗的錯誤訊息，我們需要先確認是哪一隻API，才能請後端 Server 調出相關Log
        - App Inspection > Network Inspector，看那頁打的API是哪隻，Req/Resp 是什麼
        - 當然比較好的作法應該是在錯誤訊息上印出該API的代碼，或是平常就應該做成文件，哪一頁使用哪些API
    - **Day13 - [追查 API] Burp Suite 監聽封包**
        - 介紹原理、使用方式，Https的受限
    - **Day14 - [追查 API] 好用的 Pretty 工具推薦**
        - 格式化、解碼、編碼工具
        - API 來的資料有時候不乾淨，json 需要排版，或去雙引號、解base64之類的
    - **Day15 - [追查 API] PACAndroid**
        - Relaese 版的 APP(或是別人的APP😏)，看不到 Log 或 Layout Inspector，這個像是 在手機上的 Wireshark
- Debug: 
    - **Day16 - [Debug] Log Cat**
        - Log Filter、Log Tag、Log Level
        - 好的 debug filter 可以過濾掉過多的 log 資訊，我只想看我要的
        - 管理專案中的Log，開發時，可以下一個自己專用的TAG，filter 就只要濾這個自己專用的TAG，不會看到過的無用資訊。
        - 程式推上git前，全域的搜尋一下自己的TAG，避免不需要的內容被推上去
        - 若確定是要保留的TAG，就將TAG改名成檔案名或Class名，避免 Logcat 中有一堆不知道哪裡印出的 Log
    - **Day17 - [Debug] Log vs Toast**
        - Log 不需要 Context，Toast 需要 Context
        - Log 比較通用，可以觀察執行緒的順序
        - Toast 不需要插線，方邊觀察，也方便非工程師觀察
    - **Day18 - [Debug] Device Exploer**
        - APP 寫檔的儲存位置
        - 寫檔、看檔
    - **Day19 - [Debug] SQLite**
        - App Inspection > Database Inspector
    - **Day20 - [Debug] Debugger、斷點**
    - **Day21 - [Debug] Share Preference**
        - 其實是寫檔、檔案位置
    - **Day22 - [Debug] ADB 環境變數**
- 版本控管
    - **Day23 [版本控管] 被插件怎麼辦**
        - 工程師免不了被插件，被插件的時候，可能要放下開發到一半的功能，切去其他分支修bug，這時候要用shelf或stash
    - **Day24 [版本控管] 忍不住順手修掉其他 Bug (Shelves)**
        - 有時候寫需求的過程中，順手修掉bug，但推code的時候不想兩段不相關的code混在一個commit裡面。
        - 或是可能只想先推一部分的code，還沒寫好的部分不想推上去。這時候可以用 change List
    - **Day25 [版本控管] Git GUI介面**
        - 方便的 Git GUI，可以視覺化的了解 Commit、Branch 之間的關係
    - **Day26 [版本控管] Merge vs Rebase**
        - 工程師的小堅持，在同個分支，遠端的code比較新要用Rebase，不要用Merge，保持線的乾淨
- Demo
    - 開會時免不了要投影
    - **Day27 - [Demo] Ｖysor**
        - 將手機螢幕投影到電腦 Demo
        - 將多台手機投影到電腦 深淺色一起做
- 發佈
    - **Day28 - [發佈] Crashlytics**
        - 追蹤用戶閃退紀錄
    - **Day29 - [發佈] APP Distrobution**
        - 發布測試版本
    - **Day30 - [發佈] Varient**
        - Gradel 配置
        - package, url config xml


---

template:
# 情境

# 工具介紹
## 使用步驟

## 工具優缺
- 優點

- 缺點

# 參考資料
