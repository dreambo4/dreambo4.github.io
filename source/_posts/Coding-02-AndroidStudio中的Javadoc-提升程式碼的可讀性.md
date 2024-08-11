---
title: '[Coding] 02-Android Studio 中的 Javadoc-提升程式碼的可讀性'
date: 2024-08-08T00:30:35+08:00
tags:
- 16th鐵人賽
- Android
- 註解
---

# 情境
註解是為了讓人閱讀的，無論是其他同事還是兩個禮拜後的自己。因此，註解必須清晰地描述方法的參數和作用。本文將著重於如何在 Android Studio 寫好用的註解，和方便快速的建立註解。至於 Javadoc 詳細的撰寫規範可以參考文末資料(How to Write Doc Comments for the Javadoc Tool#A Style Guide)。
<!-- more -->

本文可隨意搭配有撰寫 Javadoc 的專案使用，或參考下方 Demo 程式中的 Javadoc。
Demo 程式：GitHub: [https://github.com/dreambo4/android-basics-kotlin-mars-photos-app](https://github.com/dreambo4/android-basics-kotlin-mars-photos-app)

# Javadoc 註解介紹
根據Oracle的官方文件，註解分為兩種：
- 實作註解(Implementation Comments): 主要用於註解程式碼或對具體實作進行說明。使用 `/*...*/` 和 `//` 符號，與 C++ 的註解相似。
- 文件註解(Documentation Comments): 用於描述程式碼的規範。是 Java 特有的，使用 `/**...*/` 符號。

# 在 Android Studio 中使用
在 Android Studio 中提供方便查看註解的方式，只要將滑鼠指到一個物件、變數或方法上，就能查看相關的註釋內容。寫文件註解的好處就是，開發時不需要再一層一層點回變數宣告處，即可確認變數用途。

但要注意的是，只有文件註解的寫法，才會被解析成 Documentation。
- 實作註解，比較適合用於程式碼中的說明。
- 文件註解，適合寫類別、成員變數、方法的說明。
![兩種註解寫法](兩種註解寫法.png)

在 Android Studio 很方便的是，只要輸入 `/**`，按下 `Enter` 鍵，就會自動自動建立文件註解模板。
![文件註解模板](文件註解模板.png)

# 後記
另外，若專案的 Javadoc 寫得夠完整，還可參考這篇教學，將整個專案的文件註解匯出。
- How to create JavaDoc using Android Studio without R and BuildConfig?: https://stackoverflow.com/questions/29162820/how-to-create-javadoc-using-android-studio-without-r-and-buildconfig

# 參考資料
- How to Write Doc Comments for the Javadoc Tool#A Style Guide: https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html#styleguide
- 貢獻者的 AOSP Java 代碼風格#使用 Javadoc 標準註釋: https://source.android.com/setup/contribute/code-style?hl=zh-tw#use-javadoc-standard-comments
- Oracle 官方文件#Comment: https://www.oracle.com/java/technologies/javase/codeconventions-comments.html