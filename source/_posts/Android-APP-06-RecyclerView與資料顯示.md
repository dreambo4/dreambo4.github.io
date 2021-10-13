---
title: '[Android APP] 06-RecyclerView與資料顯示'
date: 2021-10-12 22:33:22
tags:
- 13th鐵人賽
- Android
- RecyclerView
---

這幾天我們已經從 API 取得資料到包裝成物件，再來就是資料顯示囉。

這兩天的範例會以對話頁面為主，也會用到之前設計的 `Chat` 物件。今天要介紹把對話資料顯示到 RecyclerView 上面。
<!-- more -->

# View

Activity 和 Adapter 在 MVVM 屬於 View 的範疇，用來顯示資料，不過他們負責的部分還是有點差別。Activiy 負責跟ViewModel 取得資料，把 List 的資料給 Adapter，還有所有點擊的監聽器。Adapter 只負責將接到的資料顯示到 RecyclerView 上。

物件間的關係圖，可以參考 [[[Android APP] 01-架構介紹-MVVM](https://dreambo4.github.io/2021/10/07/Android-APP-01-%E6%9E%B6%E6%A7%8B%E4%BB%8B%E7%B4%B9-MVVM/)]。

## ChatActivity

```java
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
ChatAdapter mChatAdapter = new ChatAdapter(ChatActivity.this, chatArrayList,
        optionClickCallback);
mRecyclerView.setLayoutManager(new LinearLayoutManager(ChatActivity.this));
mRecyclerView.setAdapter(mChatAdapter);
mRecyclerView.scrollToPosition(mChatAdapter.getItemCount() - 1);
```

`new ChatAdapter(ChatActivity.this, chatArrayList, optionClickCallback);` 這行就是要將整包的資料設置給 Adapter，並且把「回饋按鈕」的監聽器也一起給 Adapter。

## ChatAdapter

```java
private final Context mContext;
private final ArrayList<Chat> mChatList;
private final OptionClickCallback mOptionClickCallback;

public ChatAdapter(Context context, ArrayList<Chat> chatList, OptionClickCallback optionClickCallback) {
    this.mContext = context;
    this.mChatList = chatList;
    this.mOptionClickCallback = optionClickCallback;
}
```

一開始，我們需要一些變數和建構子(Constructor)儲存資料。


```java
private static class RecyclerViewViewHolder extends RecyclerView.ViewHolder {
    ImageView icon;
    TextView text, option_message;
    ConstraintLayout constraintLayout;
    LinearLayout optionsArea, options;
    Button opt1, opt2, opt3;

    public RecyclerViewViewHolder(@NonNull View itemView) {
        super(itemView);

        icon = itemView.findViewById(R.id.img);
        text = itemView.findViewById(R.id.text);
        option_message = itemView.findViewById(R.id.option_message);
        constraintLayout = itemView.findViewById(R.id.constraint_layout);
        optionsArea = itemView.findViewById(R.id.options_area);
        options = itemView.findViewById(R.id.options);
        opt1 = itemView.findViewById(R.id.option1);
        opt2 = itemView.findViewById(R.id.option2);
        opt3 = itemView.findViewById(R.id.option3);
    }
}
```

還需要一個 ViewHoder 用來 bind RecyclerView item 裡的物件。

```java
@Override
public void onBindViewHolder(@NonNull RecyclerView.ViewHolder holder, int position) {
    Chat chat = mChatList.get(position);
    RecyclerViewViewHolder viewHolder = (RecyclerViewViewHolder) holder;

    viewHolder.icon.setImageResource(chat.getIcon());
    viewHolder.text.setText(chat.getText());

    // 奇數列，底色改灰色
    if (position % 2 != 0) {
        viewHolder.constraintLayout.setBackgroundColor(ContextCompat.getColor(mContext, R.color.list_background));
    }

    // 有選項的 Chat，才顯示 Option 區塊
    if (mChatList.get(position).getOptions().size() < 1) {
        viewHolder.optionsArea.setVisibility(View.GONE);
    } else {
        // 取得所有 Option
        ArrayList<Option> options = mChatList.get(position).getOptions();

        // 設置選項的文字
        viewHolder.opt1.setText(options.get(0).getQuestion());
        viewHolder.opt2.setText(options.get(1).getQuestion());
        viewHolder.opt3.setText(options.get(2).getQuestion());

        // 設置三個選項的監聽器
        viewHolder.opt1.setOnClickListener(v -> mOptionClickCallback.onOptionClick(options.get(0)));
        viewHolder.opt2.setOnClickListener(v -> mOptionClickCallback.onOptionClick(options.get(1)));
        viewHolder.opt3.setOnClickListener(v -> mOptionClickCallback.noneOfAbove(options.get(2)));

        // 選項顯示的開關，預設 Gone
        viewHolder.option_message.setOnClickListener(v -> {
            if (viewHolder.options.getVisibility() == View.GONE) {
                viewHolder.options.setVisibility(View.VISIBLE);
            } else {
                viewHolder.options.setVisibility(View.GONE);
            }
        });
    }
}
```

最後把對話訊息的文字、回饋按鈕的內容都設置上去，今天就完工囉!!
