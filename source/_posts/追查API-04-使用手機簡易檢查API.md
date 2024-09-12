---
title: '[追查API] 04-使用手機簡易檢查API-PCAPdroid'
date: 2024-08-20T18:33:50+08:00
tags:
- 16th鐵人賽
- API
---

# 情境
在先前的文章中，我們介紹了如何使用電腦獲取網絡封包。今天要介紹的這個工具，可以讓你只使用手機，就簡易的檢查APP用了哪些 API、Domain、Protocal、Port。

PCAPdroid Google Store 下載:
https://play.google.com/store/apps/details?id=com.emanuelef.remote_capture
<!-- more -->

先前文章參考：
- [[追查API] 01-出事的是哪隻API-Network Inspector](https://dreambo4.github.io/2024/08/11/%E8%BF%BD%E6%9F%A5API-01-%E5%87%BA%E4%BA%8B%E7%9A%84%E6%98%AF%E5%93%AA%E9%9A%BBAPI-Network-Inspector/)
- [[追查API] 02-Burp Suite 監聽封包](https://dreambo4.github.io/2024/08/14/%E8%BF%BD%E6%9F%A5API-02-BurpSuite%E7%9B%A3%E8%81%BD%E6%89%8B%E6%A9%9F%E5%B0%81%E5%8C%85/)

# PCAPdroid 介紹
> PCAPdroid 是一款注重隱私的開源應用程式，讓你可以追蹤、分析並阻擋裝置中其他應用程式的連線。它還可以導出流量的 PCAP 檔案、檢查 HTTP、解密 TLS 流量等更多功能！
> 
> PCAPdroid 透過模擬 VPN 來捕捉網路流量，無需 root 權限。它不使用遠端 VPN 伺服器，而是在本地裝置上處理資料。

PCAPdroid 開源專案: https://github.com/emanuele-f/PCAPdroid

## 功能介紹
安裝並打開 PCAPdroid，右上角有開始/結束檢查封包的按鈕。點擊開始後就能在隔壁的 Connections 頁籤查看捕獲的內容。

![功能介紹](功能介紹.png)

### Dump 選項
PCAPdroid 提供很多種將封包 dump 出來的方式，一般選擇 `No dump` 即可。

如果需要更深入的分析，可以選擇 `PCAP file` ，將所有封包資料導出為 PCAP 檔。這樣就可以將文件導入 Wireshark 進行全面分析，無需像之前那樣讓手機通過電腦的 Proxy Server 來截獲封包。

### Target apps
考慮到手機裡可能同時運行很多個 APP，透過這個設定我們可以只捕獲所需的 APP 封包。 

### 查看封包內容
切換到 Connections 頁籤，我們可以觀察到所有 Request/Response 的基本資訊。
![Connections](Connections.png)

需要注意的是，若沒有特別設定的情況下，只能在手機上查看 HTTP(明碼) 內容。想要查看 HTTPS(加密) 的資料，請參考 APP 裡面的說明。
![查看封包內容](查看封包內容.png)

操作影片：
{% youtube Ecow7zBuS6k %}

## 工具優缺
- 優點
  - 使用方便，只需要一隻手機
  - 支援封包導出
  - 可選擇性地過濾特定 APP
- 缺點
  - 預設情況下無法查看 HTTPS 內容
  - 手機上的分析能力可能不如電腦上的專業工具強大
