---
title: BMI計算器-取得EditText中的字
date: 2017-12-14 02:02:40
tags:
- Android
- EditText
- 行雲部落格
---

* 本文曾發佈在 [https://blog.cmrdb.cs.pu.edu.tw/?p=626](https://blog.cmrdb.cs.pu.edu.tw/?p=626)

# 設計畫面

在畫面上拉出2個TextView、2個EditText和1個Button
<!-- more -->

可以參考畫面:
![image1](image1.png)

activity_main.xml:
```xml
<?xml version="1.0" encoding="utf-8"?>
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_margin="8dp"
    android:orientation="vertical"
    tools:context="com.example.yr.edittextdemo.MainActivity">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:orientation="horizontal">

        <TextView
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="2"
            android:textSize="20dp"
            android:text="請輸入身高 : " />

        <EditText
            android:id="@+id/etH"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:ems="10"
            android:textSize="20dp"
            android:hint="(公尺)" />
    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_weight="1"
        android:orientation="horizontal">

        <TextView
            android:id="@+id/textView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="2"
            android:textSize="20dp"
            android:text="請輸入體重 : " />

        <EditText
            android:id="@+id/etW"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:ems="10"
            android:textSize="20dp"
            android:hint="(公斤)" />
    </LinearLayout>

    <Button
        android:id="@+id/btnStart"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="20dp"
        android:layout_marginHorizontal="20dp"
        android:layout_weight="1"
        android:textSize="20dp"
        android:text="開始計算" />

</LinearLayout>

```

## 講解
**android:layout_margin="8dp"**
可以用這張圖理解:
![image2](image2.png)
藍色框框是主要內容，padding是指內容與邊框間的距離，margin是指距離外面的框框多少距離，上下左右都可以調整

**android:layout_weight="1"**
當使用LinearLayout排版時，可以調整每個物件在畫面上顯示的比重
![image3](image3.png)
比重越小，所分配到的範圍就越大

**android:textSize="20dp"**
設定字型大小

**android:hint="(公斤)"**
設定提示訊息

# 撰寫程式碼

## 宣告物件
```android
EditText etH,etW;
Button btnStart;
```

## 取得 View 物件
```android
etH = findViewById(R.id.etH);
etW = findViewById(R.id.etW);
btnStart = findViewById(R.id.btnStart);
```

## 設置監聽器
```android
btnStart.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {

    }
});
```

## 取得EditText中資料
```android
double h = Double.parseDouble(etH.getText().toString());
double w = Double.parseDouble(etW.getText().toString());
```

## 計算BMI
BMI的公式是 **體重/身高^2** $(\frac{kg}{m^2})$
```android
double bmi = w/(Math.pow(h,2));
```

## 顯示出BMI
```android
Toast.makeText(getApplicationContext(),String.valueOf(bmi),Toast.LENGTH_LONG).show();
```
> Toast可以顯示提示訊息

## 參考程式碼
```android
package com.example.yr.edittextdemo;

import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    //宣告物件
    EditText etH,etW;
    Button btnStart;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // 取得 View 物件
        etH = findViewById(R.id.etH);
        etW = findViewById(R.id.etW);
        btnStart = findViewById(R.id.btnStart);

        // 設置監聽器
        btnStart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                // 取得EditText中資料
                double h = Double.parseDouble(etH.getText().toString());
                double w = Double.parseDouble(etW.getText().toString());

                // 計算BMI
                double bmi = w/(Math.pow(h,2));

                // 顯示出BMI
                Toast.makeText(MainActivity.this,String.valueOf(bmi),Toast.LENGTH_LONG).show();

            }
        });


    }
}
```

# 執行畫面
![image4](image4.png)
