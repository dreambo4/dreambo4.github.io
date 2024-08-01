---
title: '[UI] 02-通過UI設計師嚴格的檢查-文字Baseline'
date: 2024-07-31T01:02:09+08:00
tags:
- 16th鐵人賽
- Android
- 排版
- Baseline
- ConstraintLayout
---

# 情境
有時候看著設計師拉的 Figma 拉完 TextView，View 對齊了但字好像沒有真的對齊。這是因為中文字和英數字 Baseline 不一樣高。在使用 ConstrainLayout 拉 TextView 的時候不妨多注意看看。

Demo 程式：GitHub: [https://github.com/dreambo4/LayoutInspectorDemo](https://github.com/dreambo4/LayoutInspectorDemo)
<!-- more -->

# Baseline說明
Baseline 是文字的基線，可以參考維基百科的說明：
https://zh.wikipedia.org/zh-tw/%E5%9F%BA%E7%B7%9A

標明Baseline的紅色線即為基線(圖片來源：由 <a href="//commons.wikimedia.org/w/index.php?title=User:Max_Naylor&amp;action=edit&amp;redlink=1" class="new" title="User:Max Naylor (page does not exist)">Max Naylor</a> - <span class="int-own-work" lang="zh-tw">自己的作品</span>, 公有領域, <a href="https://commons.wikimedia.org/w/index.php?curid=2138205">連結</a>)
![標明Baseline的紅色線即為基線](https://upload.wikimedia.org/wikipedia/commons/3/39/Typography_Line_Terms.svg)

## 有無使用 Baseline 對排版的影響
- 「顯示版面配置界限」使用方法請參考上一篇：[[UI] 01-通過UI設計師嚴格的檢查-排版&點擊範圍](https://dreambo4.github.io/2024/07/29/UI-01-%E9%80%9A%E9%81%8EUI%E8%A8%AD%E8%A8%88%E5%B8%AB%E5%9A%B4%E6%A0%BC%E7%9A%84%E6%AA%A2%E6%9F%A5-%E6%8E%92%E7%89%88-%E9%BB%9E%E6%93%8A%E7%AF%84%E5%9C%8D/#more)

比較 A、B 兩組 TextView 對齊的方式，右下圖有開啟「顯示版面配置界限」，更能看清楚量兩種排版方式下 View 的位置。
實測兩種排法，上下大概差2~3dp，足以看出文字並無完全對齊。
![兩種ContraintLayout比較](ConstraintLayoutDemo.png)

- A: 使用 constraintTop、constraintBottom 對齊。
雖然使用了上下 constraint，使 `tvTopBottom` 位於 `chineseChar1` 中間位置，但中文字與英文字，字體的 baseline 本就不一樣高。所以只是將 View 置中，並不能完全對齊文字。
```xml
<TextView
    android:id="@+id/tvTopBottom"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_marginEnd="20dp"
    android:text="constraint top and bottom"
    android:textSize="20sp"
    app:layout_constraintBottom_toBottomOf="@id/chineseChar1"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toEndOf="@id/chineseChar1"
    app:layout_constraintTop_toTopOf="@id/chineseChar1" />
```

- B：使用 constraintBaseline 對齊。
中文字與英文字，字體的baseline 不一樣高，所以應該要讓前後兩個 TextView 的 Baseline 對齊，才不會看起來一邊高一邊低。
```xml
<TextView
    android:id="@+id/tvBaseline"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_marginEnd="20dp"
    android:text="constraint baseline"
    android:textSize="20sp"
    app:layout_constraintBaseline_toBaselineOf="@id/chineseChar2"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toEndOf="@id/chineseChar2" />
```

# 參考資料
- 設計師常說我們的文字沒對齊
- 使用 ConstraintLayout 打造回應式 UI https://developer.android.com/develop/ui/views/layout/constraint-layout?hl=zh-tw
