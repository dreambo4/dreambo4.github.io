---
title: '[UI] 03-UI設計師不在家-用滴管工具取得色碼'
date: 2024-08-02T19:26:20+08:00
tags:
- 16th鐵人賽
- Android
- UI
- 色碼
- 滴管工具
---

# 情境
當團隊的設計師不在，你沒有 Figma 或 Zeplin 等方便的工具，只有一張 設計圖.png，要如何取得設計圖上的色碼，順利完成今天的開發任務呢？

這個專案用的色碼比較多，可以拿這個測試。
GitHub: [https://github.com/dreambo4/NavigationDemo](https://github.com/dreambo4/NavigationDemo)
<!-- more -->

# 工具介紹
今天要介紹的是 Mac 內建的「數位測色器」工具，可以幫助你尋找螢幕上顏色的顏色數值。

![數位測色器](數位測色器.png)

## 使用步驟
從 Mac 的啟動台，找到並開啟數位測色工具，再來只要把滑鼠移到想要查看顏色的地方，就能查看色碼。

但受限於圖片的解析度，測色計的結果只能說很非常接近，不一定能完全等於原始色碼。純色色塊越大較能取到精準的顏色。實測下，色彩空間選擇「**以sRGB顯示**」是最接近原始顏色的。

在 工具列 > 顯示方式 > 顯示數值，可以選用合適的色碼表示方式。
![數值顯示方式設定](數值顯示方式設定.png)

接下來實測，原始色碼是 `#FFF59D`，以測色計測出來的結果也是 `#FFF59D`！
![專案實測](專案實測.png)

## 鎖定光圈快捷鍵
參考自[官方使用手冊](https://support.apple.com/zh-tw/guide/digital-color-meter/welcome/mac)
- 水平鎖定光圈: Command + X
- 垂直鎖定光圈: Command + Y
- 同時雙向鎖定光圈: Command + L

## 工具優缺
- 優點
  - 在沒有原始色碼的狀況下，取得最接近的色碼
- 缺點
  - 測色計結果受限於，圖片解析度、色塊大小
  - 若原始色碼帶有透明度，由測色計無法得知

# 參考資料
- 數位測色計使用手冊: https://support.apple.com/zh-tw/guide/digital-color-meter/welcome/mac