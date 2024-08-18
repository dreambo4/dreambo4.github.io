---
title: '[追查API] 02-Burp Suite 監聽封包'
date: 2024-08-14T23:40:05+08:00
tags:
- 16th鐵人賽
- Android
- API
- Burp Suite
- 資安
---

# 情境
在上一篇文章中，我們介紹了 Android Studio 內建的 Network Inspector。若是今天想撈的是別人的 APP 或網頁的 Request，Burp Suite 會是一個更適合的工具。Burp Suite 有很多版本，一般建議裝社群版(Community)就夠用了。

下載 Burp Suite Community Edition：https://portswigger.net/burp/communitydownload
<!-- more -->

# Burp Suite 介紹
我第一次知道 Burp Suite 這個工具是因為資安的 CTF(Capture The Flag) 搶旗賽，Burp Suite 提供非常多輔助 "安全性測試" 的工具。今天要介紹的是眾多工具的其中之一--Proxy。

Burp Proxy 可以讓手機的流量經過 Proxy 再代理發送出去，這樣我們就能攔截、查看、修改所有的 Request/Response。其實這個作法，若攔截者有惡意意圖，已經是「中間人攻擊」（Man-in-the-middle attack），所以請不要對未經所有者授權的網站進行測試或攻擊。

在 HTTP 的時代，Proxy 攔截封包相對簡單。然而，隨著 HTTPS 的普及和各種 CA 驗證技術的應用，現代使用 Proxy 代理並攔截封包變得有一定門檻。網路上有很多這類教學，詳細說明就留給參加資安主題的同學了。

![Proxy 原理](Proxy原理.png)

## 使用步驟
1. 在電腦上安裝 Burp Suite，作為 Proxy Server，並且讓 Client 和 Proxy 在同一個測試網段下。
2. 建立 Burp Suite 預設專案。
   ![建立專案](建立專案.png)
3. 切換到 Proxy 頁籤，設定 Proxy 監聽的 Port。只要不和已使用的 Port 衝突，Port 號可以自由設置。
    ![Proxy Rule Setting](ProxyRuleSetting.png)
4. 手機設定連線到 Proxy。
   ![Android Setting](AndroidSetting.png)

## 功能介紹
完成上述設定後，就能透過 Burp Suite 攔截封包了。
![按鈕功能](按鈕功能.png)

主要按鈕功能：
- Forward: 讓攔截到的流量通過(送到 Server)
- Drop: 丟棄攔截到的流量
- Intercept is on/off: 開啟/關閉攔截功能

成功攔截到的流量紀錄，也可以在 HTTP History 查看。但我的 Post 內容有關個資，不方便 show 給大家看，留給大家自行嘗試囉。
![HTTP History](HttpHistory.png)

## 工具優缺
- 優點
  - 相較於前篇介紹的 Network Inspector，Burp Suite 可攔截非 debuggable 的 APP 或是 WebView 的封包

- 缺點
  - 需要理解 Proxy 基本原理。
  - 只適用 HTTP、WebSocket Protocal，對於 TCP 或 UDP 封包，建議使用 Wireshark 等其他工具
  - 遇到有驗證 CA 或是用 HTTPS 的 Server，需要額外設定

# 參考資料
- 中間人攻擊-維基百科: https://zh.wikipedia.org/zh-tw/%E4%B8%AD%E9%97%B4%E4%BA%BA%E6%94%BB%E5%87%BB
- Mobile testing - PortSwigger: https://portswigger.net/burp/documentation/desktop/mobile
- Intercepting HTTP traffic with Burp Proxy - PortSwigger: https://portswigger.net/burp/documentation/desktop/getting-started/intercepting-http-traffic

**!! 請勿對未經所有者授權的網站進行測試或攻擊 !!**