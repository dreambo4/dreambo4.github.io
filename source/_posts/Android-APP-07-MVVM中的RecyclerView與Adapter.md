---
title: '[Android APP] 07-MVVM中的RecyclerView與Adapter'
date: 2021-10-13 22:22:29
tags:
- 13th鐵人賽
- Android
- RecyclerView
- MVVM
---

鐵人賽快到尾聲了，今天想介紹在控制 RecyclerView 中回饋按鈕時，遇到的狀況。想想，這篇好像應該和前一篇順序對調，畢竟是先有這些糾結，才有後面自己歸納出的那些寫法。所以先暫時忘掉昨天的寫法，回到 MVVM 的初學者吧。
<!-- more -->

**大家覺得 Adapter 應該屬於 View 層或是 ViewModel 層呢?**

第一次寫 MVVM 搭配 RecyclerView，突然不知道要怎麼用，爬了網路上的文章後，卻又更更更混亂了。
可以先看一下這兩篇:
- [#請益：MVVM架構中，如何串接Adapter？](https://www.facebook.com/groups/523386591081376/permalink/3896247253795276/)
- [Android # Best practice Challenge for MVVM x RecyclerView](https://medium.com/gdg-taipei/android-best-practice-challenge-for-mvvm-x-recyclerview-acd9e9ad0dae)

# Adapter 的歸類

取自第一篇的整理，網路上的寫法大致上有三種
1. VM 持有 Adapter
2. V持有Adapter，但每次資料更新都重建Adapter
3. V持有Adapter，但每次都 notifyDataSetChanged()

我後來又爬了多文章和範例，也和朋友討論過，還是覺得 Adapter 負責資料的顯示應該屬於 View，而我實作的方法偏第 2 種。下面附上我的程式碼:

完整版程式碼: https://gitlab.com/graduate_lab415/chatbot/-/blob/master/app/src/main/java/com/cmrdb/app/chatbot/view/ChatActivity.java

```java
private final Observer<ArrayList<Chat>> mChatListUpdateObserver = new Observer<ArrayList<Chat>>() {
    @Override
    public void onChanged(ArrayList<Chat> chatArrayList) {
        OptionClickCallback optionClickCallback = new OptionClickCallback() {
            @Override
            public void onOptionClick(Option option) {
                mViewModel.sendOptionMessage(option, categoryId);
            }

            @Override
            public void noneOfAbove(Option option) {
                mViewModel.sendOptionMessage(option, categoryId);
            }
        };
        ChatAdapter mChatAdapter = new ChatAdapter(ChatActivity.this, chatArrayList, optionClickCallback);
        mRecyclerView.setLayoutManager(new LinearLayoutManager(ChatActivity.this));
        mRecyclerView.setAdapter(mChatAdapter);
        mRecyclerView.scrollToPosition(mChatAdapter.getItemCount() - 1);
        mProgressLayout.setVisibility(View.GONE);
    }
};
```

我是在聊天紀錄的 Observer 裡，只要聊天紀錄有變動，就重新生成 Adapter 和提供更新後的聊天紀錄。

# Adapter 和 ViewModel 的互動

既然已經決定 Adapter 屬於 View，我遇到的第二個問題是當 **Adapter 要怎麼和 ViewModel 互動?**

我的案例是回饋按鈕被點擊後，需要使用 `ChatViewModel` 中的 `sendOptionMessage()`，要怎麼呼叫呢?

1. Activity 透過 Adapter 的建構子，將 Viewmodel 物件傳入。在 Adapter 中處理監聽事件，並使用傳入的 ViewModel 物件。
2. 在 Adapter 中建立一個 ViewModel 物件，一切由 Adapter 自己操作 (這作法我沒試過，不確定會不會有什麼問題)
3. 維持 ViewModel 的物件只有一個，且由 Activity 操作。讓被點擊的事件，回歸到 Activity 處理。

我不確定第一種作法，將 ViewModel 當參數傳來傳去好不好，不過我自己不是很喜歡。所以，後來是選用第 3 種方式。

這個問題，我也不確定作法好不好，如果你有什麼想法歡迎留言討論哦!!
