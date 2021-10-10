---
title: '[Android APP] 04-MVVM - Repository與API串接'
date: 2021-10-10 21:39:42
tags:
- 13th鐵人賽
- Android
- Repository
- MVVM
- API
- Callback
---

前幾天介紹的 MVVM 架構，可以參考這篇 [[[Android APP] 01-架構介紹-MVVM](https://dreambo4.github.io/2021/10/07/Android-APP-01-%E6%9E%B6%E6%A7%8B%E4%BB%8B%E7%B4%B9-MVVM/)]。今天要講的是其中 Repository 的部分，Repository 通常用來提供資料，因為我的資料來源只有 API，就不那麼複雜了，直接在 Repository 串接 API。
<!-- more -->

本系統中有 2 個 Repository、3 支 API，這次以 JSON 結構比較簡單的 CategoryRepository 來作範例。

# CategoryRepository

我在這邊用的是 Volley，當然你想用 Retrofit 或其他的 http client 也都可以。
關於 Volley 的使用可以參考我之前的文章: [[Workshop記錄-Volley與API](https://dreambo4.github.io/2019/07/13/Workshop%E8%A8%98%E9%8C%84-Volley%E8%88%87API/#more)]

完整程式碼: https://gitlab.com/graduate_lab415/chatbot/-/blob/master/app/src/main/java/com/cmrdb/app/chatbot/repository/CategoryRepository.java

```java
public void get(CategoryVolleyCallback callback) {
    StringRequest stringRequest = new StringRequest(Request.Method.GET,
            "http://120.110.112.177:83/Chatbot/getCategories.php",
            response -> {
                Log.d(TAG, "onResponse: " + response);
                ArrayList<Category> categoryList = new ArrayList<>();
                try {
                    JSONObject json = new JSONObject(response);
                    JSONArray categories = json.getJSONArray("categories");

                    for (int i = 0; i < categories.length(); i++) {
                        JSONObject category = categories.getJSONObject(i);
                        categoryList.add(new Category(
                                category.getString("id"),
                                category.getString("name")));
                    }

                    callback.onSuccess(categoryList);
                } catch (JSONException e) {
                    callback.onFail("發生一些錯誤\n" + e.getLocalizedMessage());
                }

            },
            error -> {
                Log.e(TAG, "onErrorResponse: ", error);
                callback.onFail("發生一些錯誤\n" + error.toString());
            });
    mRQ.add(stringRequest);
}
```

因為從 API 取得資料是非同步運行的，所以參數中有個 Callback。Callback 的用意就是，當資料都收到之後，再透過 `callback.onSuccess(categoryList);` 回傳給 ViewModel。如果不是使用 Callback 而是直接 `return categoryList;` 的話，會造成物件回傳了，但物件裡還是空的、ViewModel 沒有拿到資料的狀況。瞭解 Callback 的概念是很重要的哦!!

# 資料提供流程

![flow](flow.jpg)
