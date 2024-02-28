---
title: 透明的Activity
date: 2024-02-28 19:49:29
tags:
- Android
- Android-Activity
- Android-Dialog
---

之前遇到的需求是，有一連串的 Dialog 要依據一定的步驟與邏輯顯示，所以我希望有個 Activity 來控制流程。而各步驟畫面都是 Popup Dialog 樣式，為了達到 Dialog 浮在上層的效果，**我需要一個透明的 Activity**。
<!-- more -->
# 透明的 Activity

這邊採用的作法是將 Activity 的主題(Theme)設成 Dialog 樣式。在 Manifest 可以為 Activity 設定主題，`android:theme="@style/xxx"`。

嘗試過 `android:theme="@style/Theme.AppCompat.Dialog"`，但畫面上會留有一塊黑黑的 Dialog 內建的標題文字，參考 [对话框样式的activity-去标题栏](https://blog.csdn.net/u010243044/article/details/53504816) 後客製一個新的 Style。另外要注意 Style 要加在 `styles.xml`，不要放在 `themes.xml`，背景會變成不透明。

## Styles.xml
```xml
<style name="Popup" parent="Theme.AppCompat.Dialog">
    <item name="windowActionBar">false</item>
    <item name="windowNoTitle">true</item>
</style>
```

## AndroidManifest.xml
```xml
<activity
    android:name=".view.ui.tutorial.DemoActivity"
    android:exported="true" 
    android:theme="@style/Popup" />

```

# 使用方式

上面的參考連結提到：

> 對話框大小由里面内容决定，而不是頂層 layout 决定。頂層 layout 的 match_parent（或設置其他固定高寬）沒有作用，textview 的大小才起作用

由於我們的 Activity 只用來控制 Popup Dialog 的顯示，所以在 `activity_demo.xml` 中什麼都不用放，我們只取他的半透明效果，對其他 Popup Dialog 的大小不會有影響。

另外需注意的是，在最後一個步驟的 Dialog 關掉時，要記得把 `DemoActivity` 一起 `finish()` 掉，才不會留下黑黑的背景！

# 參考資料
- [对话框样式的activity-去标题栏](https://blog.csdn.net/u010243044/article/details/53504816) 
