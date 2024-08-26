---
title: '[UI] 04-使用 Android Studio 內建的 Color Picker 設定顏色'
date: 2024-08-03T17:42:02+08:00
tags:
- 16th鐵人賽
- Android Studio
- 色碼
- 透明度
- 滴管工具
---

# 情境
開發的時候，使用 Figma 的設計圖，常會遇到帶有透明度的顏色。那麼，如何將這些顏色的透明度從百分比轉換為 16 進制呢？

除了前一篇介紹的的「數位測色器」工具，Android Studio 也有內建的 Color Picker，這個工具不僅方便設定顏色，還能輕鬆處理透明度問題。

<!-- more -->
這個專案用的色碼比較多，可以拿這個測試。
GitHub: [https://github.com/dreambo4/NavigationDemo](https://github.com/dreambo4/NavigationDemo)

看「數位測色器」介紹，往這邊：[[UI] 03-UI設計師不在家-用滴管工具取得色碼](https://dreambo4.github.io/2024/08/02/UI-03-UI%E8%A8%AD%E8%A8%88%E5%B8%AB%E4%B8%8D%E5%9C%A8%E5%AE%B6-%E7%94%A8%E6%BB%B4%E7%AE%A1%E5%B7%A5%E5%85%B7%E5%8F%96%E5%BE%97%E8%89%B2%E7%A2%BC/)

# 工具介紹
Android Studio 的 Color Picker 用法很簡單，當你為一個 View 設定顏色，行號的右側會出現一個小色票。
![開啟ColorPicker](開啟ColorPicker.png)

## 使用步驟
1. 點擊小色票就能開啟 Color Picker
2. Color Picker 接受多種輸入格式
   - 可以直接輸入色碼，也能用滴管、調色盤選擇顏色
   - 10進制、16進制兩種格式色碼
   - 透過 A% 欄位可以設定透明度
![ColorPicker](ColorPicker.png)

### 帶有透明度的顏色
Figma 中的透明度通常以百分比表示。使用 Color Picker，你可以直接在 A% 欄位直接輸入百分比數值(ex: `15`)，系統會直接換算成對應的16進制數值(ex: `26`)。
![AlphaSetting](AlphaSetting.png)

## 工具優缺
- 優點
  - 操作簡單
  - 支援多種色碼輸入方式、格式
  - 支援色碼透明度設定
- 缺點
  - 只能在 Android Studio 使用(若非 Android 開發情境，可以考慮「數位測色器』)
