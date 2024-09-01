---
title: '[追查API] 05-使用 Postman Proxy 快速建立 API 文件與範例'
date: 2024-08-29T19:05:10+08:00
tags:
- 16th鐵人賽
- API
- Postman
- Proxy
---

# 情境
接手舊專案，但沒有 API 文件，有時候註解寫的 Request 欄位也不完全正確。一個一個查很花時間，不如就讓 Postman Proxy 來幫你整理 API 文件吧。
<!-- more -->

# Postman 介紹
Postman 是一個開發者常用的工具，可以用來模擬、測試使用者打 API 的情境。也可以用來整理 API 文件，和他人共享。除此之外，他還提供很多附加功能，像是今天要介紹的 Proxy，他可以紀錄流經 Proxy 的封包內容，讓開發者可以 Debug、重現問題。

## 使用步驟
電腦端要啟用 Proxy Server，手機端要設定 Proxy 連線。

### 電腦端-啟動 Proxy Server
下載Postman: https://www.postman.com/downloads/

1. 打開 Postman，右下角的工具列有一個 `Start Proxy`
2. Proxy 預設是 `5559` port，也可自行調整
3. 啟動 Proxy

![Start Proxy](StartProxy.png)

**啟動之後要特別注意**，你的電腦網路可能也會「貼心」的被指向 Proxy，造成一般網頁無法開啟。本篇的主題，只有要紀錄手機端的 API，電腦本身的連線不需經過 Proxy。因此若遇到相同問題，請到 `系統設定 > 網路 > 詳細資訊 > 代理伺服器 > 關閉「安全網頁代理伺服器」`。

![System Proxy Setting](SystemProxySetting.png)

### 手機端-設定連向 Proxy
Proxy 原理和的手機端的設定方式，在之前的文章([[追查API] 02-Burp Suite 監聽封包](https://dreambo4.github.io/2024/08/14/%E8%BF%BD%E6%9F%A5API-02-BurpSuite%E7%9B%A3%E8%81%BD%E5%B0%81%E5%8C%85/))說明過，這邊就不再重複。

![Android Setting](AndroidSetting.png)

### 開始紀錄封包
以上都設定好，之後之要手機有任何 Http Request 封包，都會被 Postman Proxy 紀錄。API 資訊，包含 URL、Http Method、Reqest、Response，相當完整。
![Postman Proxy Result](PostmanProxyResult.png)

最後，也是最重要的一步，將完整 API 紀錄儲存起來，再為他們改個名，你就擁有完整的API文件(包含真實的 Request/Response 範例)。很棒吧！！
![Postman Save Result](PostmanSaveResult.png)

操作影片：
{% youtube i6V6Su7HoyA %}

## Postman Proxy vs Burp Suite Proxy
參考前幾天的 Burp Suite Proxy：[[追查API] 02-Burp Suite 監聽手機封包](https://dreambo4.github.io/2024/08/14/%E8%BF%BD%E6%9F%A5API-02-BurpSuite%E7%9B%A3%E8%81%BD%E6%89%8B%E6%A9%9F%E5%B0%81%E5%8C%85/)

首先，兩者都是方便好用的 Proxy 工具，都可以用來紀錄並觀察 HTTP 封包。

差異就在，Burp Suite 的特色是可以一包一包的觀察，並且由你決定放行、竄改、丟棄每一個 Request。適用情境應該偏向資安領域，可以檢測封包內是否包含敏感資訊(身分證ID、電話等)。或是檢測後端程式有沒有做好檢核，竄改 Request 內容可能做到提權、獲取他人資料等。(好的檢核，不能只有前端做，後端也要做喔)

而 Postman Proxy 的功能相對單純，只有讓手機封包經過 Proxy 時，紀錄相關 Request/Response 內容。但這些資訊搭配 Postman 原有的 Collection 功能就能快速整理出漂亮的 API 文件。適用對象應該偏向開發者。

# 後記
追查 API 的主題告一段落了，API 是我所有小主題中，最有心得的一塊。因為寫 APP 基本離不開 API，不連網的 APP 應該很少很少了吧？再加上以前和朋友參加過幾次 CTF 比賽，我沒有資工朋友的那些硬底子，PWN、Reverse 這類題目基本直接跳過，只能主攻網頁題，也因此練就攔截封包的各種技能XD

最後，感謝朋友提供現成的 Restful API，讓我順利完成本文的 Demo！

# 參考資料
- Capture traffic using the Postman built-in proxy: https://learning.postman.com/docs/sending-requests/capturing-request-data/capture-with-proxy/