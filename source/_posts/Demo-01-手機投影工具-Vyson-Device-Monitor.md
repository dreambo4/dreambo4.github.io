---
title: '[Demo] 01-手機投影工具-Vyson & 內建 Device Mirroring'
date: 2024-09-15T19:57:43+08:00
tags:
- 16th鐵人賽
- Android Studio
- Vysor
---

# 情境
在進行開會演示或開發測試時，我們經常需要將 Android 手機螢幕投影到電腦上。雖然 Android 沒有像蘋果的 AirPlay 那樣內建的方便功能，但我們仍有多種方式可以達到相同效果。本文將介紹兩種實用的工具：Vysor 和 Android Studio 的 Device Mirroring。
<!-- more -->

# Vysor 介紹
Vysor 是一個支援多系統的軟體，你可以自由選擇安裝桌面版或 Chrome 的套件版。Vysor 可以將 Android 或 iOS 裝置的畫面投影至電腦螢幕。

## Vysor 使用步驟
本文以 Mac 桌面版為例，展示 Vysor 的使用方法：

1. 依照指示下載 Vysor
   - Download Vysor: https://www.vysor.io/download/
2. Android 手機開啟偵錯模式
3. 將手機連接到電腦
4. 在 Vysor 上看到裝置，點選最右邊的紅色按鈕，將手機螢幕投影到電腦
![Vysor](Vysor.png)

## Vysor 優缺
- 優點
  - 支援同時投影多個設備，方便進行分割視窗操作
  - 跨平台支援，適用於多種作業系統
- 缺點
  - 免費版畫質較差

# Android Studio-Device Mirroring
您可以在 Android Studio 的「Running Devices」視窗中，為實體裝置建立鏡像。只要將裝置的畫面直接串流至 Android Studio，即可利用 Studio IDE 本身執行常用操作，例如啟動應用程式並與其互動、旋轉螢幕、折疊及展開手機，以及調整音量。

## Device Mirroring 使用步驟
1. Android 手機開啟偵錯模式
2. 將手機連接到電腦
3. 在 Android Studio 中，打開側邊工具列，選擇 "Running Devices"
4. 上方的「+」按鈕，可以選擇要投影的裝置
![Device Mirroring](DeviceMirroring.png)

## Device Mirroring 優缺
- 優點
  - 畫質清晰
  - 與 Android Studio 緊密集成，適合開發者使用
- 缺點
  - 雖然可以將 Tools 視窗獨立顯示，但同時顯示多個設備的鏡像時不如 Vysor 方便。

# 總結
在開發 UI 的階段，為了同時觀察深色、淺色的配置，我通常會將兩個設備同時投影到螢幕上。由於這個階段主要重點是顏色配置而非畫質，Vysor 更適合進行分割視窗操作，因此在這種情況下我會選擇 Vysor。

在電腦有安裝 Android Studio 的情況下，若有會議投影需求，基於畫質考量，我會優先選擇 Device Mirroring。

總之，Vysor 和 Android Studio 的 Device Mirroring 功能都能將 Android 手機螢幕投影到電腦，建議依據使用情境，挑選合適工具。

# 參考資料
- Vysor: https://www.vysor.io/
- 裝置鏡像功能: https://developer.android.com/studio/run/device?hl=zh-tw#device-mirroring