---
title: '[Trace Code] 03-搜尋大法'
date: 2024-07-24T17:34:39+08:00
tags:
- 16th鐵人賽
- Android
- Trace Code
---

# 情境
前面介紹了兩種快速找到問題源頭方法，還沒看過的可以先參考：
- [[Trace Code] 01-使用Profiler檢查當前所在Activity/Fragment](https://dreambo4.github.io/2024/06/30/Trace-Code-01-%E4%BD%BF%E7%94%A8-Profiler-%E6%AA%A2%E6%9F%A5%E7%95%B6%E5%89%8D%E6%89%80%E5%9C%A8-Activity-Fragment/)
- [[Trace Code] 02-使用Layout Inspector尋找當前所在Layout](https://dreambo4.github.io/2024/07/01/Trace-Code-02-%E4%BD%BF%E7%94%A8-Layout-Inspector-%E5%B0%8B%E6%89%BE%E7%95%B6%E5%89%8D%E6%89%80%E5%9C%A8-Layout/#more)

在偵錯模式下，工具可以幫助我們快速找到問題的發生地。但更多時候，客戶回報問題只會有錄影或截圖。這時候要找問題發生地，就只能使用強大的搜尋功能啦～
<!-- more -->

這次可以使用這個範例來練習
GitHub: [https://github.com/dreambo4/NavigationDemo](https://github.com/dreambo4/NavigationDemo)

# 工具介紹
我常用的搜尋工具主要有兩個
1. Search Everywhere
   - 快捷鍵：連點兩下 Shift
   - 快速搜尋並開啟 Class
   - 不一定需要輸入完整，"HomeActivity" 只需要輸入 "HA"就能找到
   - ![Search Everywhere](SearchEverywhere.png)
2. Find in Files
   - 快捷鍵：Cmd + Shift + F (Windows: Ctrl + Shift + F)
   - 可以針對字串搜尋
   - 右上角的 File mask 可以只針對某副檔名搜尋。例如你很確定這個字串應該是在 layout 中使用，可以限定 `*.xml`；或是很確定有某個註解關鍵字在程式中，可以限定 `*.kt` 或 `*.java`。
   - 漏斗符號：可以過濾是否為字串或註解的內容。
   - ![Find in Files](FindInFiles.png)

## 使用步驟
這邊分享幾個我平常搜尋過程中的想法

以這個APP畫面為例，如果要你使用搜尋法找到這個頁面，你會搜尋什麼關鍵字呢？

![Practice](practice.png)

### 第一種 - 使用 Search Everywhere
首先，這是登入畫面，所以我會先用 Search Everywhere 搜尋 `Login` 相關的頁面。幸運的話，或許可以找到 `LoginActivity` 或 `LoginFragment`。

### 第二種 - 使用 Find in Files
若頁面不是可以直觀猜到名稱的，那麼我會使用 Find in Files 搜尋關鍵字，這時挑選合適的關鍵字就很重要了。

1. 我會先淘汰 A、E，因為這些詞很常出現在註解或是 API 欄位的描述中
2. H 的的內容，很明顯來自 API，不是 APP 端定義的字串
3. 再來 B、D、G，這三個詞在 APP 中很可能有其他入口，或在其他頁面也有使用，所以也不會是第一首選
4. 剩下 C、F，這兩個看起來比較像只有在登入頁才會出現的字串

關鍵就是盡量挑選「固定不變動」、「獨一無二」的字串。只要找對關鍵字，很快就能順藤摸瓜找到 Layout，再找到相關 Class。

## 工具優缺
- 優點
  - 手邊沒有偵錯工具時，依然可以使用
- 缺點
  - 需要依靠經驗，挑選合適的搜尋關鍵字
