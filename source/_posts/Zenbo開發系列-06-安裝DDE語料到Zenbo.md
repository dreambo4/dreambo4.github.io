---
title: '[Zenbo開發系列] 06-安裝DDE語料到Zenbo'
date: 2021-08-10 14:10:39
tags:
- Zenbo
- DDE
- 13th鐵人賽
---

今天使用的範例出自高煥堂老師的書《AI機器人、藍芽與Android整合開發技術》，需要完整程式碼請參考書中內容喔。
本篇會以 `Ex14-01-ZenboWiFi` 這份程式碼說明如何將語料安裝到 Zenob 中。

<!-- more -->

# 準備材料

你需要
- 一台 Zenbo
- 一份做好的 DDE 語料 (製作方式請參考[上一篇](../../07/Zenbo開發系列-05-DDE回覆規則設計))
- 一份 `Ex14-01-ZenboWiFi` Sample code

在 DDE info 設定的地方，Launch Activity 要填 APP 啟動的第一個 Activity，完整路徑可以看 Manifest。
![project_info](project_info.png)
![launch_activity](launch_activity.png)

# 綁定 Domain

還記得你的 Domain UUID 嗎?
在 DDE info 最上面 點選 `All` 可以查看你所有的 uuid。
![all_uuid](all_uuid.png)

打開 Android 專案，範例中基本都已經打好了，我們只須把自己的 Domain 換上去。
特別注意，總共有 3 個地方要改唷
- Manifest 2 個
- ZenboWiFiActivity 1 個

![manifest_uuid](manifest_uuid.png)
![activity_uuid](activity_uuid.png)

第一次安裝，開啟時應該會自動更新語料。
去 DS Tools 確認是否有更新成功

> DS Tools 可以在 [DDE Tutorial-Links](https://zenbo.asus.com/developer/documents/overview/DDE-Tutorial/Downloads/Links) 找到下載連結。
> 把 APK 裝到 Zenbo 的方法很多，用隨身碟或雲端硬碟都行。

# DS Tools
可以管理自己安裝在 Zenbo 上的語料庫。
如果剛才 DDE 有安裝成功的話，這裡點選 `Show APP List` 會看到 Package name、UUID 和 更新時間。確認一下 PKG 和 UUID 是不是都符合前面的設定。
以後如果要更新 DDE 的話，可以先點選要更新的 APP，讓 UUID 自動帶到上方欄位，再按 `Update by ID`。
![dstools](dstools.png)

# 刪除 Zenbo 中的 DDE

這就是我前幾篇提到，我寫信給客服信箱的問題了。我前面不知道怎麼弄的，PKG 和 UUID 一直對不上，所以沒辦法更新。客服請我先把裝壞的 DS 資料清掉，這邊紀錄一下作法。

1. 先把裝壞的 APP 刪除: 設定 > 應用程式 > [你的APP] > 儲存空間 > 清除資料
2. 把 APP 刪掉
3. 參考 [Zenbo-Scratch-語句聽不懂問題的解決方式](Zenbo-Scratch-語句聽不懂問題的解決方式.pdf)  將 LocalDS 的資料清除
   - 這篇就是客服寄給我的
4. Zenbo 關機重開
5. DDE 重新 Publish、Deploy to Download Server
6. APP 重裝
7. 去 ASUS Update Tools 確認

# 成果
我有改過 `Ex14-01-ZenboWiFi` 的畫面和部份的 code 成品大概像影片這樣。

{% youtube zWkc5L9Ux5o %}

## DDE 的問題
截自我的論文:
> 根據文獻（朱祐萱，2019；白麗等，2018），Zenbo 的語音識別功能，不能清楚辨識指令，是其主要問題。再加上本研究嘗試使用 Zenbo SDK 實作語音回答時，發現 Zenbo 無法處理破音字的發音。例如，「長照」正確唸法是「長（ㄔㄤˊ）照」，但 Zenbo SDK 會唸作「長（ㄓㄤˇ）照」。有時也會跳過句子中的某些字，例如，「台中市政府長期照顧管理中心」的「長」、「原住民」的「民」。
>
> 經過嘗試，最後本研究決定在 APP 中，使用 Android 官方提供的兩個函式庫「android.speech.RecognizerIntent」（以下簡稱 RecognizerIntent）與「android.speech.tts.TextToSpeech」（以下簡稱 TextToSpeech）。根據官方文件 RecognizerIntent（Android Developers, 2021）可以透過 Intent（意圖）啟動語音辨識；TextToSpeech（Android Developers, 2021）可以從文本合成出語音後，立即播放或儲存成音檔。
>
> 為了解決 Zenbo 反應遲鈍，我們在 APP 中提供按鈕，按下按鈕便會觸發 RecognizerIntent 開始聆聽使用者的問題，並將問句顯示在畫面上，使用者可以確認語音輸入的結果是否正確再點選送出（請參考  Youtube  影片：[語音識別與輸出（使用 RecognizerIntent 和 TextToSpeech）](https://youtu.be/iSneVFi9J0I)）。

這就是我最後沒有使用 DDE 和 Zenbo SDK 的原因。

# 參考資料
- Android Developers. (2021). TextToSpeech. Retrieved from https://developer.android.com/reference/android/speech/tts/TextToSpeech
- Android Developers. (2021). RecognizerIntent. Retrieved from https://developer.android.com/reference/android/speech/RecognizerIntent
- 白麗、鄭家凱、林恩如、陳思宇、張譯云、徐業良、華碩電腦智慧機器人產品企劃團隊（2018）。 陪伴型機器人使用者經驗評估─以智慧居家機器人Zenbo 為例。福祉科技與服務管理學刊，6(3)，265-282。DOI：10.6283/JOCSG.201809_6(3).265。檢自：https://www.airitilibrary.com/Publication/alDetailedMesh?DocID=23061790-201809-201810220006-201810220006-265-282。
- 朱祐萱（2019）。銀髮族使用 Zenbo 機器人服務體驗洞察研究。南開科技大學福祉科技與服務管理所碩士論文，南投縣。檢自：https://hdl.handle.net/11296/x4x8c6。
