---
title: '[Zenbo開發系列] 03-DDE Editor vs Dialogflow'
date: 2021-08-05 21:44:20
tags:
- Zenbo
- DDE
- Dialogflow
- 聊天機器人
---

DDE(dialogue development environment) Editor [[官方文件](https://zenbo.asus.com/developer/documents/overview/DDE-Tutorial/Welcome)] 是由 ASUS 提供，可以設計自己的回覆規則的工具，製作好之後可以把語料安裝到 Zenbo。

以我有用到的功能來說，Dialogflow 和 DDE 都是 Rule-base 的方式，但我覺得相比 Dialogflow，DDE 就比較工人智慧一點😂。
<!--more-->

對了，DDE **建議搭配 Chrome**。使用 Firefox 的話，右側的對話測試區會沒有反應 ~~(被雷到💣)~~

# Dialogflow 比較強大
舉例來說，Dialogflow 可以做到這樣

我先在 Entities 定義了台中「區」的名稱
![DF_entities](DF_entities.png)

然後設計對話語句
![DF比較強大](DF比較強大.png)

## 測試對話
Dialogflow 應該有支援**模糊比對**句子之類的功能，像是「我要找長照站」、「哪裡有據點」都沒有完全符合前面設計的句子規則。而且句中如果沒提到地點，Dialogflow 可以再補問「你要找哪裡的長照站?」。相較之下，DDE 就要把句子規則定好定滿，沒有符合就不會回覆相應的句子。

![DF1](DF1.png)
![DF2](DF2.png)
> "..." 是我還沒把真正的地址加上去，先暫代的，應該是要跟 Fulfillment 串接，但我沒有做完這部份

# DDE 工人智慧
DDE 雖然是 ASUS 做的，但官方文件卻是以英文為主，中文的版本相對沒那麼齊全。然後建議，文件看過最好順手存下來，他們網站不知道在搞什麼，有一陣子上去找資料發現文字都變成亂碼，還好之前有先用 Notion 存起來。

不過還是有一些優點的，開發遇到問題的時候，寫信給客服信箱，會有他們的工程師回答你，這部分 Dialogflow 應該就無法了。
> 他也只回我一兩次而已，後面我再接著問的部分，就沒再回了。不過我那時候的主要問題有解決，就不跟他計較啦~

Dialogflow 可以模糊比對句子，DDE 話就沒那麼方便，相關的句子規則都要訂清楚，如果設計不好，句子間有可能撞關鍵字。

![DDE1](DDE1.png)
![DDE2](DDE2.png)
![DDE3](DDE3.png)

## 和 Zenbo 的搭配

和 Zenbo 的配合方面，DDE 還是要比 Dialogflow 好一點。DDE 做好的語料庫，可以發布到伺服器，在 Zenbo 就可以透過官方提供的 APP 來更新/下載語料。這些語料會跟其他原先就存在的語料放在一起，等於是裝在 Zenbo 腦袋裡。Dialogflow 比較像腦袋在雲端上，只把 Zenbo 當作是一個介面，回傳什麼句子給 Zenbo 他就照唸。

另外，如果要做到「Hey, Zenbo 我要用`APP名稱`」的話，要到 Zenbo 開發者平台註冊 [Developer Console](https://zenbo.asus.com/developer/console/)。

# 結語
最後，如果沒有真的一定要用 DDE 的話，我會比較建議 Dialogflow。因為 Dialogflow 支援比較多平台，常見的平台都可以串接，如果想裝在 Zenbo 上也可以用 API(不過這部份我沒有實作)，走跟一般 Android 的路線。

好了，比較完了，那你說我最後是用那一個？我只能說都沒有🤦‍♂️
論文中，我的語料庫模型是用 TF-IDF 自己建的，之後有時間再補這部份的文章吧！
