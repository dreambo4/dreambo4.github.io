---
title: '[Coding] 01-Android Studio快速程式碼模板'
date: 2024-07-07T22:34:11
tags:
- 16th鐵人賽
- Android
- 程式碼模板
---

# 情境
在 Android 開發中，我們經常會遇到需要重複輸入或複製貼上某些程式碼片段的情況。這不僅耗時，還容易出錯。而 Android Studio 提供了一個強大的功能——程式碼模板，它可以幫助我們大大提高開發效率。
<!-- more -->

# 工具介紹
Live Templates 是由 IntelliJ 提供的功能，可以快速插入預定義的程式碼模板。IntelliJ 內建就已經提供了許多常用模板，如迴圈、條件判斷、變數宣告等。而 Android Studio 又多了更多 Android 相關的 Templates。

舉例來說，只要輸入 `logd` 並按下 `Enter鍵` 就，會自動出現 Log.d 的模板程式碼。善用這些快速模板，可以加快開發速度。

![Live Template 示意](liveTemplateSample.png)

## 常用範例

| 輸入縮寫 | 自動補齊程式碼模板                              |
| :------- | :---------------------------------------------- |
| logd     | Log.d(TAG, "onCreate: ")                        |
| toast    | Toast.makeText(, "", Toast.LENGTH_SHORT).show() |

## 使用步驟
但你有想過這些好用的補齊功能都設定在哪裡嗎?

1. 打開 `Setting > Editor > Live Templates`

2. 在這裡，你可以看到所有預定義的模板!

![預定義的模板](預定義的模板.png)

## 新增自訂模板
當內建模板不夠用時，我們也可以自行新增常用的程式碼片段

1. 點擊「+」新增程式碼模板
2. Abbreviation: 輸入模板的簡稱，這也是之後要使用該模板的縮寫
3. Description: 輸入模板的說明
4. Template text: 輸入模板內容
5. Change: 勾選此模板的適用範圍。每個模板的適用範圍都不同，就像 Kotlin 的程式模板不應出現在 XML 一樣。

舉個例子，在使用 Constraint Layout 時，我們常遇到要將元件的四邊都拉到 parent。這時就能新增一個模板，解決重複輸入的問題。設定方式可以參考下圖：

![新增模板](新增模板.png)

```xml
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent"
```

新增完成後，在 Layout 中，我就只需要輸入 `pppp`，就能自動補齊程式碼。

![在layout中使用](inLayout.png)

## 工具優缺
- 優點
  - 大幅提高開發效率
  - 減少重複性工作
  - 降低程式碼錯誤率

- 缺點
  - 需要一定時間學習和記憶模板縮寫
  - 過度依賴可能會影響對程式碼的理解

# 參考資料
- https://www.jetbrains.com/help/idea/using-live-templates.html




