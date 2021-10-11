---
title: '[Android APP] 05-API與物件'
date: 2021-10-11 21:59:31
tags:
- 13th鐵人賽
- Android
- API
- 物件
---

昨天講的是 API 傳遞資料的流程，今天就來介紹怎麼把資料包裝成物件，方便傳遞吧。
<!-- more -->

一樣，會使用 JSON 結構比較簡單的 CategoryRepository 來作範例。

# 寫法演變

在還沒有用物件操作資料以前，我們的專案都是用 `ArrayList<HashMap<String, String>>` 來儲存資料的。

大概會像這樣:
```java
ArrayList<HashMap<String, String>> categoryList = new ArrayList<>();
try {
    JSONObject json = new JSONObject(response);
    JSONArray categories = json.getJSONArray("categories");

    for (int i = 0; i < categories.length(); i++) {
        JSONObject category = categories.getJSONObject(i);

        HashMap<String, String> category = new HashMap<>();
        category.put("id", category.getString("id"));
        category.put("name", category.getString("name"));

        categoryList.add(category);
    }
    callback.onSuccess(categoryList);
} catch (JSONException e) {
    callback.onFail("發生一些錯誤\n" + e.getLocalizedMessage());
}
```

一開始這是簡單又方便的解決方式，不需要自己建立物件。試想，若是欄位變多了之後呢?

在不同 Class 中傳遞物件時，你需要一直對照、複製貼上，確認兩邊的 key 是一致的、數量是一致的，而且 IDE 不會自動幫你補齊!!若是今天有不同格式的資料，但型態卻都是一樣的 `ArrayList<HashMap<String, String>>`，那又要如分辨呢?

所以後來我才漸漸改成使用物件來包裝傳遞資料，可以為物件設置 Constructor，或是每個欄位的 getter、setter，這樣就能使用 IDE 的全功能囉。而且傳遞物件的時候就能清楚的知道，物件裡面裝的是什麼內容。甚至是 `Chat` 這種比較複雜(裡面還有包一個 `ArrayList`)的資料結構，也能輕鬆存取。

![chat](chat.png)

# 程式碼

好了，那來介紹一下物件的建立吧!!

JSON 格式是這樣的，可以觀察一下，其實每個物件都是由 `id`、`name` 組成的。

```json
{ 
    "categories": [ 
        { 
            "id": 0, 
            "name": "全部" 
        }, 
        { 
            "id": 1, 
            "name": "長照據點與機構" 
        }, 
        { 
            "id": 2, 
            "name": "長照服務介紹與申請" 
        }, 
        { 
            "id": 3, 
            "name": "輔具服務" 
        }, 
        { 
            "id": 4, 
            "name": "外籍看護相關規範" 
        }, 
        { 
            "id": 5, 
            "name": "長照服務人員培訓與任用" 
        } 
    ] 
}
```

對應到物件上，我設計了兩個字串，分別來儲存 `id` 和 `category`。

```java
public class Category {
    private final String mId;
    private final String mName;

    public Category(String id, String name) {
        mId = id;
        mName = name;
    }

    public String getId() {
        return mId;
    }

    public String getName() {
        return mName;
    }
}
```

如此一來，在 Repository 就能使用物件的方式來包裝資料了。可以比較一下，和前面的寫法有什麼不一樣哦。

```java
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
```

在 [Activity](https://gitlab.com/graduate_lab415/chatbot/-/blob/master/app/src/main/java/com/cmrdb/app/chatbot/view/CategoryActivity.java) 和 [ViewModel](https://gitlab.com/graduate_lab415/chatbot/-/blob/master/app/src/main/java/com/cmrdb/app/chatbot/viewmodel/CategoryViewModel.java) 中，都有使用到這個物件唷。
