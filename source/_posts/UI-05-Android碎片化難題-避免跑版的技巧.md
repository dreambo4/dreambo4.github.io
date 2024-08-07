---
title: '[UI] 05-Android碎片化難題-避免跑版的技巧'
date: 2024-08-06T20:31:48+08:00
tags:
- 16th鐵人賽
- Android
- 裝置
- UI
---

# 情境
Android 手機，廠商多、機型多、長寬比例也各式各樣，確保 UI 在不同裝置上的一致性是一大挑戰。本文將介紹兩個避免 UI 跑版的重要概念。

Demo 程式：GitHub: [https://github.com/dreambo4/LayoutInspectorDemo](https://github.com/dreambo4/LayoutInspectorDemo)

## 由內而外構建 UI
> Do: 外層 View 的大小應隨著內層 View 的寬高縮放
> Don't: 不應由外而內的設定 View 的寬高

<!-- more -->
讓我們用下方的程式碼來舉例說明：
- `constraintLayoutA` 寬高都用 `wrap_content`，TextView 與 ConstraintLayout 的間距用 TextView 的 margin 設定。
- `constraintLayoutB` 寬高都設為固定值。

乍看之下，兩種寫法的結果相似。然而，一旦文字內容變長或字型變大，`constraintLayoutB` 就會出現嚴重跑版。

因此，即使 UI 設計稿上標示這個 View 的長寬為一個固定數值。開發還是要特別注意，考量 View 的擴充性與內容的預期的呈現方式，選擇合適的寫法。

![兩種寫法比較](兩種寫法比較.png)

程式碼：
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".UIDemoActivity">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toTopOf="@id/guidelineHalf"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <!-- 外層 ConstrainLayout，隨著內層 TextView 縮放 -->
        <androidx.constraintlayout.widget.ConstraintLayout
            android:id="@+id/constraintLayoutA"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:background="#00BCD4"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent">

            <TextView
                android:id="@+id/textViewA"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_margin="20dp"
                android:background="#FFEB3B"
                android:text="TextViewA"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />
        </androidx.constraintlayout.widget.ConstraintLayout>

    </androidx.constraintlayout.widget.ConstraintLayout>

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guidelineHalf"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.5" />

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/guidelineHalf">

        <!-- 外層 ConstrainLayout 設定固定寬高 -->
        <androidx.constraintlayout.widget.ConstraintLayout
            android:id="@+id/constraintLayoutB"
            android:layout_width="100dp"
            android:layout_height="60dp"
            android:background="#00BCD4"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent">

            <TextView
                android:id="@+id/textViewB"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:background="#FFEB3B"
                android:text="TextViewB"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />
        </androidx.constraintlayout.widget.ConstraintLayout>

    </androidx.constraintlayout.widget.ConstraintLayout>
</androidx.constraintlayout.widget.ConstraintLayout>
```

## 較長的頁面添加滑動功能
> 當頁面內容較長，務必考慮小手機用戶的體驗，添加滑動功能。

以註冊頁面為例，通常需要輸入多項資訊。沒注意的話，落落長的欄位與輸入框，可能在某些裝置上無法完整顯示。身為專業的工程師，開發時應當考慮小手機的滑動範圍、可視範圍呈現。

添加 `NestedScrollView` 的用法看可參考下方程式碼。

建議平常準備多種尺寸的測試機。若無實體機，也可使用模擬器或 Android 裝置串流(見文末參考資料)。

![不同尺寸手機呈現差異](不同尺寸手機呈現差異.png)

程式碼：
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".LongContentDemoActivity">

    <androidx.core.widget.NestedScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:fillViewport="true"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical">

            <TextView
                android:id="@+id/textView5"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginHorizontal="20dp"
                android:layout_marginTop="60dp"
                android:gravity="center"
                android:text="當內容有一定長度，\n要記得考慮小手機用戶"
                android:textSize="30sp"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

            <ImageView
                android:id="@+id/imageView2"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="60dp"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@id/textView5"
                app:srcCompat="@drawable/ic_launcher_foreground"
                app:tint="#4FAF53" />

            <Button
                android:id="@+id/button"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="60dp"
                android:text="Button"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@id/imageView2" />

            <TextView
                android:id="@+id/textView"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginHorizontal="20dp"
                android:layout_marginTop="60dp"
                android:gravity="center"
                android:text="稍長的頁面都要\n考慮添加滑動功能"
                android:textSize="30sp"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@id/button" />

            <TextView
                android:id="@+id/textView4"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginHorizontal="20dp"
                android:layout_marginTop="60dp"
                android:gravity="center"
                android:text="看得到這行嗎🤫"
                android:textSize="30sp"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@id/textView" />
        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.core.widget.NestedScrollView>
</androidx.constraintlayout.widget.ConstraintLayout>
```

# 總結
- UI 開發要**由內往外**自動縮放，而非由外往內固定尺寸
- 開發任何頁面，都要考慮小手機的呈現效果
- 建議準備多種尺寸的測試機，確保 UI 在各種裝置的彈性

# 參考資料
- 採用 Firebase 技術的 Android 裝置串流: https://developer.android.com/studio/run/android-device-streaming