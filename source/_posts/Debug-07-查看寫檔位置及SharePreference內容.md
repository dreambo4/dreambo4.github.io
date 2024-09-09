---
title: '[Debug] 07-查看 APP 檔案儲存位置及 SharePreference 內容'
date: 2024-09-07T17:32:20+08:00
tags:
- 16th鐵人賽
- Android Studio
- SharePreference
---

# 情境
有些情境，需要把某些資料儲存在手機本地，寫過存取檔案或 SharePreference，但他實際儲存在哪裡？可以查看檔案內容嗎？
<!-- more -->

# Device Explore 介紹
開啟開發人員模式，就能用 Device Explore 存取手機裡面的檔案。例如，直接從手機抓出截圖、將檔案直接放到手機的資料夾。

而 SharePreference 的背後其實也是寫檔，今天就一併介紹檔案儲存位置了。

## 使用步驟
1. 在 Android Studio 側邊工具列中選擇 Device Explorer
2. 找到 `/data/data/[APP Package Name]`，這就是 APP 的資料夾。需要特別注意的是，APP 需要是 debuggable。
3. 展開後，可以看到這個 APP 的所有檔案
![Device Explore Demo 1](DeviceExploreDemo1.png)
![Device Explore Demo 2](DeviceExploreDemo2.png)

## 查看 SharePreference 檔案
完整 Demo 專案 Github: https://github.com/dreambo4/Restful-Api-Demo-Todo-Project

首先我們先測試寫入 SharePreference
```kotlin
class MainActivity : BaseActivity<ActivityMainBinding>() {
    // SharePreference 物件
    private val sharedPreferences: SharedPreferences by lazy {
        getSharedPreferences("app_prefs", Context.MODE_PRIVATE)
    }

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        val defaultBaseUrl = "http://192.168.0.12:8080/"
        
        // 取得已儲存的 SharePreference
        var newBaseUrl = sharedPreferences.getString("base_url", defaultBaseUrl) ?: defaultBaseUrl
        
        sharedPreferences.edit().putString("base_url", newBaseUrl).apply()
        
        binding.apply {
            etBaseUrl.setText(newBaseUrl)
            etBaseUrl.addTextChangedListener(object : TextWatcher {
                override fun afterTextChanged(s: Editable?) {
                    newBaseUrl = s.toString()
                    // 使用者編輯過的話，就儲存 SharePreference
                    sharedPreferences.edit().putString("base_url", newBaseUrl).apply()
                }

                override fun beforeTextChanged(s: CharSequence?, start: Int, count: Int, after: Int) {}

                override fun onTextChanged(s: CharSequence?, start: Int, before: Int, count: Int) {}
            })
        }
    }
}
```

![SharePreference 內容](SharePreference內容.png)

可以發現 SharePreference 的檔名，就是先前寫在 `getSharedPreferences("app_prefs", Context.MODE_PRIVATE)` 的名稱。並且也能用 key 存取 value 內容。
```kotlin
sharedPreferences.edit().putString("base_url", newBaseUrl)

sharedPreferences.getString("base_url", defaultBaseUrl)
```

## 工具優缺
- 優點
  - 可以方便查看手機內檔案內容
- 缺點
  - APP 需要是 Debuggable

# 參考資料
-  View on-device files with Device Explorer: https://developer.android.com/studio/debug/device-file-explorer
- Debuggable 和 Profileable 設定與差異：https://dreambo4.github.io/2024/06/30/Trace-Code-01-%E4%BD%BF%E7%94%A8-Profiler-%E6%AA%A2%E6%9F%A5%E7%95%B6%E5%89%8D%E6%89%80%E5%9C%A8-Activity-Fragment/#Debuggable-%E5%92%8C-Profileable-%E7%9A%84%E8%A8%AD%E7%BD%AE
