---
title: '[爬蟲] 02-儲存爬蟲資料-CSV格式'
date: 2021-09-14 02:00:13
tags:
- Python
- 爬蟲
- 13th鐵人賽
- CSV
---

接續上一篇，昨天已經把問答集的內容都爬下來了，再來要把內容整理成下一個階段(訓練模型)，方便使用的格式。
完整的程式碼可以參考: [https://github.com/dreambo4/MOHW-QandA](https://github.com/dreambo4/MOHW-QandA)

<!-- more -->

# CSV
什麼是 CSV?
> 逗號分隔值（Comma-Separated Values，CSV），其檔案**以純文字形式儲存表格資料**。純文字意味著該檔案是一個字元序列，不含必須像二進位數字那樣被解讀的資料。
> -- form [wiki](https://zh.wikipedia.org/wiki/%E9%80%97%E5%8F%B7%E5%88%86%E9%9A%94%E5%80%BC)

看圖吧!

原始的 CSV 就只是一個純文字檔，各個欄位以 `,` 隔開。不同筆資料，以換行區隔。
首列通常是欄位名稱。
![csv_text](csv_text.png)

特別的是，剛提過 CSV 儲存的資料是個表格嘛，所以我們也可以使用 Excel 或 LibreOffice Calc 編輯檔案，很方便。
![csv_excel](csv_excel.png)

## 為什麼不用資料庫?
CSV 的優點是好攜帶 & 好轉移，因為是純文字的關係，比較不會有需要用特定軟體開啟的狀況，一般的文字編輯器(記事本、Sublime、Vim...)就可以開啟。本系統資料儲存主要使用 CSV 格式，而非資料庫的原因是，目前沒有需要。爬蟲的步驟只會做一次，不需要每次建置模型都爬蟲一次取得資料，因此初始的資料集內容基本是固定的。而程式建模型的過程，也只會有「讀取全部資料」的動作，沒有條件查詢、新增、修改、刪除。因此評估後，我們使用 CSV 作為資料及儲存的格式。

**這是本系統未使用資料庫的原因，不一定適合你的狀況，請自行評估調整。**

# 主要程式

主要的程式收兩個參數，`filename` 是生成檔案的名字；`datelist` 是要存入檔案的內容，型態是 list。
這個 CSV 的套件，提供很多方便的功能。首先寫入欄位名稱，再用迴圈的方式，一筆一筆將內容寫入檔案。

```python
def writeCsv(filename, dataList):
    with open(filename+'.csv', 'w', newline='') as csvfile:
        # 定義欄位
        fieldnames = ['q', 'a', 'url']

        # 將 dictionary 寫入 CSV 檔
        writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

        # 寫入第一列的欄位名稱
        writer.writeheader()

        # 寫入資料
        for qa in dataList:
            writer.writerow(qa)
```

Colab 另個方便的地方，執行後，檔案可以直接下載~
![get_file](get_file.png)

# 結語
爬蟲的文章告一段落，接下來會是 TF-IDF 和模型建置相關的部分。明天見！

# 參考資料
- Beautiful Soup 4.9.0 documentation. (2021). Beautiful Soup Documentation. Retrieved from 
https://www.crummy.com/software/BeautifulSoup/bs4/doc/