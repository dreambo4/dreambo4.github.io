---
title: 第一個 Kotlin 專案
date: 2017-07-10 20:43:00
tags:
- Kotlin
- Android
- 行雲部落格
---

* 本文曾發佈在 [https://blog.cmrdb.cs.pu.edu.tw/?p=291](https://blog.cmrdb.cs.pu.edu.tw/?p=291)

2020/11/09 更新:
現在的 Android Studio 安裝時，都附帶有 Kotlin 了，不需要再另外安裝。
<!-- more -->
---

在Google I/O 2017 開發者大會中，Kotlin已被宣布成為Android 程式的官方一級開發語言（First-class language）。Android Studio 3.0之後的版本更直接內建支援Kotlin。

Kotlin能與Java在專案中並存，讓開發者能保有原本的專案，也能以Kotlin繼續開發。 

# 安裝外掛
由於目前的Android Studio還沒內建支援Kotlin，所以我們要安裝Plugin

1. 點選右下 Configure > Plugins
    ![image13](image13.png) 

1. 點選 Browse repositories...
    ![image12](image12.png) 

1. 搜尋 Kotlin
    ![image11](image11.png) 

1. 點選 Install，安裝完成後點 Restart Android Studio，重新開啟 Android Studio
    ![image10](image10.png) 

# 第一支Kotlin程式

1. 開新專案
    ![image8](image8.png) 
    ![image7](image7.png) 
    ![image6](image6.png) 

2. 目前的專案還是Java
    ![image5](image5.png) 

1. 接著我們要把 Java 轉換成 Kotlin，點選上方工具列中 Code > Convert Java File to Kotlin File
    ![image4](image4.png) 

1. 稍待幾秒鐘，轉換完成!!
    ![image3](image3.png) 

1. 在 activity_main.xml 中新增一個 Button 和 TextView
    ![image2](image2.png) 

1. 切換至 MainActivity.kt，宣告變數
```kotlin
var btn = findViewById(R.id.button) as Button
var txv = findViewById(R.id.textView) as TextView
```

1. 設置監聽器，改變TextView文字內容
```kotlin
btn.setOnClickListener { 
            txv.setText("Hello World !")
}
```

1. 執行畫面參考
    ![image1](image1.png) 
    ![image](image.png) 

# 程式碼參考

- activity_main.xml

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="com.example.yr.kotlinfirst.MainActivity">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="TextView" />

    <Button
        android:id="@+id/button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button" />

</LinearLayout>
```

- MainActivity.kt

```kotlin
package com.example.yr.kotlinfirst

import android.os.Bundle
import android.support.v7.app.AppCompatActivity
import android.widget.Button
import android.widget.TextView

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        var btn = findViewById(R.id.button) as Button
        var txv = findViewById(R.id.textView) as TextView

        btn.setOnClickListener {
            txv.setText("Hello World !")
        }
    }
}
```
