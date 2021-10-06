---
title: '[API] 使用 PHP 執行 Python 腳本'
date: 2021-10-06 21:18:11
tags:
- 13th鐵人賽
- PHP
- Python
- API
---

嗨! 昨天終於結束了語料庫模型建置的部分，再來就要建立 API 了。這個系統中我採用了一個比較特別的架構，伺服器是 Ubumtu + Apache + PHP，API 主要使用 PHP 撰寫，並由 PHP 去執行 Python 腳本(也就是前面建置的 TF-IDF 語料庫模型)，再回傳結果。可以參考下圖。
<!-- more -->

![系統架構](系統架構.png)

其實 Python 也是可以寫後端的，但我缺少建置 Python 伺服器的經驗，期間我嘗試搭配 Python + Apache、用 Python 的框架建置服務，一直沒有成功。哀，這又是另一個走錯路的故事了。

後來聽了朋友建議，採用一個比較像繞過問題的方式，使用 PHP + Apache 作為 API 端服務，PHP 去執行 Python 腳本。換句話說，就是把 PHP 當作是 Android 與 TF-IDF 語料庫之間的橋樑。不過，我覺得這不是一個最好的寫法。

做都做了，還是要記錄一下啊，今天這篇就來介紹使用 PHP 執行 Python 腳本的方法吧。

# 程式碼

以編號 001 這支來說明
完整程式碼: https://gitlab.com/graduate_lab415/chatbot-api/-/blob/master/getAnswer.php

```php
<?php
/**
 * 001 [POST] /Chatbot/getAnswer.php
 * 以使用者輸入的語句查詢，回傳資料集中與輸入最相似的 3 筆問答組合。
 * 
 * q: 使用者輸入的問句
 * category_id: 使用者選擇的類別編號
 */
header('Content-Type: application/json; charset=utf-8');
$q = $_POST['q'];
$category_id = $_POST['category_id'];
$output = exec('/home/yr/PycharmProjects/nlp/venv/bin/python3 /home/yr/PycharmProjects/nlp/main.py ' . $q . ' ' . $category_id . ' 2>/home/yr/PycharmProjects/nlp/output/log.txt', $output2);
print($output);
```

首先，會收兩個 Post 參數 `$_POST['q']`、`$_POST['category_id']` 執行 Python 腳本時，再把參數帶進去。

`$output` 會得到 Python 印出的 JSON 內容，再印出來給 Android 端。

簡略一點，就是這個樣子。因為我用的是 Pycharm 的 venv 所以路徑要複雜一點。
```shell
python3 main.py "我想申請長照" 2 2>log.txt
```
> `2>log.txt`: 把標準錯誤寫到檔案中

# API

本系統總共有 3 支 API: getAnswer、addAdjustment、getCategories。
各自的詳細說明與程式碼在這: https://gitlab.com/graduate_lab415/chatbot-api
