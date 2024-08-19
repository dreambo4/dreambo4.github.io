---
title: '[追查API] 03-好用的 Pretty 工具推薦'
date: 2024-08-19T19:33:39+08:00
tags:
- 16th鐵人賽
- Android
- API
- Json
---

# 情境
前兩天講的工具主要是撈取 Request/Response 。今天要介紹的是如何將這些撈到的資料快速排版，讓它們變得更易於閱讀，特別是當資料量很大、格式又很雜亂的時候。

本文主要介紹兩款 Formatter 工具。一個是我自己用 Python 編寫的工具，專門處理公司內部雜亂的 API 格式。另一個是推薦的好用 Json Formatter 工具。
<!-- more -->

# 自己寫 Formater
自製 API Formatter 小工具，Github 連結如下: 
https://github.com/dreambo4/API-Formater/blob/main/ML%E9%9B%BB%E6%96%87%E6%A0%BC%E5%BC%8FFormatter.ipynb

早期網路還不普及，流量受到諸多限制，因此許多 API 開發僅使用 pipeline 分隔欄位，盡量壓縮封包長度。如今的 Json、XML 這麼多冗詞贅字、重複的 Tag 標籤，在當時都是不可能存在的。然而，許多古老未翻新的程式留用至今，格式就變得不是那麼直觀，而且也沒有專用的 Parser，閱讀起來相當麻煩的。

例如(以下舉例，我隨便寫寫)：
```
|TXO|202408|22000|P|B|120|5|

|>STKID=TXO|>DATE=202408|>STRIKEPRICE=22000|>CP=P|>BS=B|>PRICE=120|>AMT=5

stk_id="TXO",date="202408",strike_price="22000",cp="P",bs="B",amt="5"
```

由於這種奇怪的格式，每次都要自己斷句非常麻煩，所以我就自己寫了小工具，而且各個小工具還能互相搭配使用真的很方便。

有興趣的朋友可以到 Github 上 fork 一份，這個工具可以在 Google Colab 上直接使用，無需額外安裝環境，十分方便。

![Colab Pipline Formatter](colabPiplineFormater.png)

![Colab Comma Formatter](colabCommaFormater.png)

# 好用的 JSON Formatter
JSON Formatter & Validator:
https://jsonformatter.curiousconcept.com/#

網路上有許多 Json Formatter 工具，而今天介紹的這個網站優點在於：
1. 可以 Parse 不完整或缺少成對括號的 Json
2. 可以嘗試 Parse toString 的 Java/Kotlin 物件

可以看到這個 Json 遺失了後半部分的資料，但 Formatter 還是盡量幫忙呈現出應有的樣子。
```json
{"store":{"book":[{"category":"reference","author":"Nigel Rees","title":"Sayings of the Century","price":8.95},{"category":"fiction","author":"Evelyn Waugh","title":"Sword of Honour","price":12.99},{"category":"fiction","author":"J. R. R. Tolkien","title":"The Lord of the Rings","isbn":"0-395-19395-8","price":22.
```
![Format Invalid Json](formatInvalidJson.png)

或是平常 debug 的時候，將 ArrayList、HashMap toString 印出來，只要選擇 "Skip Validation"，這個工具也能幫忙將資料整理得還不錯。
```
bindRecyclerView: [MarsPhoto(id=424905, imgSrcUrl=https://mars.jpl.nasa.gov/msl-raw-images/msss/01000/mcam/1000MR0044631300503690E01_DXXX.jpg), MarsPhoto(id=424906, imgSrcUrl=https://mars.jpl.nasa.gov/msl-raw-images/msss/01000/mcam/1000ML0044631300305227E03_DXXX.jpg), MarsPhoto(id=424907, imgSrcUrl=https://mars.jpl.nasa.gov/msl-raw-images/msss/01000/mcam/1000MR0044631290503689E01_DXXX.jpg), MarsPhoto(id=424908, imgSrcUrl=https://mars.jpl.nasa.gov/msl-raw-images/msss/01000/mcam/1000ML0044631290305226E03_DXXX.jpg), MarsPhoto(id=424909, imgSrcUrl=https://mars.jpl.nasa.gov/msl-raw-images/msss/01000/mcam/1000MR0044631280503688E0B_DXXX.jpg), MarsPhoto(id=424910, imgSrcUrl=https://mars.jpl.nasa.gov/msl-raw-images/msss/01000/mcam/1000ML0044631280305225E03_DXXX.jpg), MarsPhoto(id=424911, imgSrcUr
```
![Format Java Object](formatJavaObject.png)

# 後記
收到資料後要如何整理也是一門學問。將資料格式化後，無論是討論問題還是進行分析都更加方便。希望今天分享的 Formatter 工具對你有所幫助，如果你也有推薦的工具，歡迎與我分享！
