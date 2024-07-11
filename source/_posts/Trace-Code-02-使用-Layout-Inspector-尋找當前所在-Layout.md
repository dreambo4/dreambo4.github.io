---
title: '[Trace Code] 02-使用Layout Inspector尋找當前所在Layout'
date: 2024-07-01T20:02:11+08:00
tags:
- 16th鐵人賽
- Android
- Trace Code
---

# 情境
- 可以快速找到顯示錯誤資訊的元件，進而查詢錯誤原因。
- 確認元件當前的 Attribute，例如：textSize, textColor, background, visibility...等。

在Android開發中，有時我們會遇到畫面上某些元件未如預期顯示的問題。例如，一個應該顯示文字的TextView突然消失了。這時，我們該如何診斷問題呢？

我製作了一個範例，其中應該顯示三個TextView，但實際上一個都看不到。在不偷看 Layout 程式碼的狀況下，試試你能找出問題嗎？
<!-- more -->

GitHub: [https://github.com/dreambo4/LayoutInspectorDemo](https://github.com/dreambo4/LayoutInspectorDemo)

# 工具介紹
Layout Inspector是一個強大的工具，可以即時觀察元件的狀態，若會在程式中動態調整元件狀態，這個功能就很實用。

## 使用 Layout Inspector 的步驟
1. 在 Android Studio 的工具列中找到"Running Device"選項。
2. 連接實體設備或啟動虛擬機。
3. 在右上角找到並開啟Layout Inspector。

對 Component 連點兩下就就可以快速導航到 Layout，很方便。早期還要另外搜尋 id 再自己尋找對應 Layout，現在已經改進很多了！

![Layout Inspector 位置](LayoutInspector.png)

即使某些元件在畫面上不可見，Layout Inspector仍能顯示它們的當前狀態。

以範例中的三個TextView為例，它們不可見的原因如下：
1. textView1: 寬度和高度均為0
2. textView2: 文字顏色與背景顏色相同（白色）
3. textView3: visibility 屬性設為 invisible

在實際開發中，可能因為 Layout 沒拉好、visibility 控制判斷邏輯有誤，導致元件不可見，這些都是常見原因！

![使用 Layout Inspector 觀察 Component](watchComponent.png)

## Layout Inspector 的新舊版本比較
舊版的 Layout Inspector 是一個獨立的工具。

新版Layout Inspector已整合到Running Device功能中。但如果你更喜歡舊版的獨立工具，還是可調整設定
`Setting > Tools > Layout Inspector > Enable embedded Layout Inspector`。
- 勾選: 在 Running Devices 中使用 Layout Inspector
- 取消勾選: Layout Inspector 作為獨立工具使用

![Layout Inspector Setting](LayoutInspectorSetting.png)

## 工具優缺
- 優點
    - 快速定位目標 Layout
    - 即時觀察元件狀態
- 缺點
    - 需要在debug模式下使用，且需要電腦
    - 在沒有電腦的情況下，可以使用 Android 裝置的「顯示版面配置界限」功能進行簡單測試（這部分將在後續文章中詳細介紹）

# 參考資料
- https://developer.android.com/studio/debug/layout-inspector
