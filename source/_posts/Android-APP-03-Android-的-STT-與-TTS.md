---
title: '[Android APP] 03-Android 的 STT 與 TTS'
date: 2021-10-09 16:46:29
tags:
- 13th鐵人賽
- Android
- STT
- TTS
---

用鍵盤輸入訊息，對年輕人或許稀鬆平常，但對長者而言，使用語音的方式或許更輕鬆。所以除了畫面字體放大外，我們也使用語音識別與輸出技術，提供長者更友善的工具。

上次的文章 [[Zenbo開發系列] 06-安裝DDE語料到Zenbo](https://dreambo4.github.io/2021/08/10/Zenbo%E9%96%8B%E7%99%BC%E7%B3%BB%E5%88%97-06-%E5%AE%89%E8%A3%9DDDE%E8%AA%9E%E6%96%99%E5%88%B0Zenbo/) 有講到 DDE 的問題和使用 Android 語音識別與輸出的原因。那麼，今天就要來介紹 Android 這邊的實作囉!
<!-- more -->

# STT 語音轉文字

> STT (Speach to Text)

完整程式碼: https://gitlab.com/graduate_lab415/chatbot/-/blob/master/app/src/main/java/com/cmrdb/app/chatbot/view/ChatActivity.java

語音轉文字的功能用在左下的麥克風按鈕，點擊之後會有個對話框請使用者說出問句。

![對話頁面](對話頁面.png)

我們讓麥克風按鈕被點擊後，執行一個 Intent。

```java
ImageButton btnSpeak = findViewById(R.id.speak);
btnSpeak.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Intent sttIntent = new Intent(RecognizerIntent.ACTION_RECOGNIZE_SPEECH);
        sttIntent.putExtra(
                RecognizerIntent.EXTRA_LANGUAGE_MODEL,
                RecognizerIntent.LANGUAGE_MODEL_FREE_FORM
        );
        sttIntent.putExtra(RecognizerIntent.EXTRA_LANGUAGE, Locale.getDefault());
        sttIntent.putExtra(RecognizerIntent.EXTRA_PROMPT, getString(R.string.start_to_speak));

        try {
            startActivityForResult(sttIntent, REQUEST_CODE_STT);
        } catch (ActivityNotFoundException e) {
            Log.d(TAG, "onClick: " + e.getLocalizedMessage());
            Toast.makeText(ChatActivity.this, "Your device does not support STT.", Toast.LENGTH_LONG).show();
        }
    }
});
```

之後我們就能在 `onActivityResult` 取得語音辨識的結果，並把文字顯示到 EditText 上。
這樣設計的原因是想解決 DDE 常辨識不到文字的狀況，使用者可以確認語音識別的內容是否正確，再點選送出紐。

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, @Nullable Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (requestCode == REQUEST_CODE_STT) {
        if (resultCode == Activity.RESULT_OK && data != null) {
            ArrayList<String> result = data.getStringArrayListExtra(RecognizerIntent.EXTRA_RESULTS);
            if (result != null) {
                String recognizedText = result.get(0);
                mUserInput.setText(recognizedText);
            }
        }
    }
}
```

# TTS 文字轉語音

> TTS (Text to Speach)

我是在 ViewModel 的呼叫使用 TTSSpeaker。

## ChatViewModel

完整程式碼: https://gitlab.com/graduate_lab415/chatbot/-/blob/master/app/src/main/java/com/cmrdb/app/chatbot/viewmodel/ChatViewModel.java

這邊參數需要傳兩個 Callback 給 TTSSpeaker。
- 第一個 `TTSCallback` 是我自己寫的，主要用來確認 TTS 初始化是否成功，`onReady` 才能執行將句子唸出來的動作。
- 第二個 `UtteranceProgressListener` 是要確認 TTS 目前的狀況，`onStart`(開始)、`onDone`(唸完)、`onError`(錯誤)。

```java
private void speak(String message) {
    TTSCallback ttsCallback = new TTSCallback() {
        @Override
        public void onReady() {
            mSpeaker.speak(message);
        }

        @Override
        public void onFail() {
            Log.d(TAG, "ttsCallback onFail");
        }
    };
    UtteranceProgressListener speakingStatus = new UtteranceProgressListener() {
        @Override
        public void onStart(String utteranceId) {
            Log.d(TAG, "speakingStatus onStart");
        }

        @Override
        public void onDone(String utteranceId) {
            Log.d(TAG, "speakingStatus onDone");
            mSpeaker.destroy();
        }

        @Override
        public void onError(String utteranceId) {
            Log.d(TAG, "speakingStatus onError");
            mSpeaker.destroy();
        }
    };

    mSpeaker = new TTSSpeaker(mApplication, ttsCallback, speakingStatus);
}
```

## TTSSpeaker

完整程式碼: https://gitlab.com/graduate_lab415/chatbot/-/blob/master/app/src/main/java/com/cmrdb/app/chatbot/controller/TTSSpeaker.java

```java
public class TTSSpeaker {
    private TextToSpeech mTTS;
    private TTSCallback mCallback;
    private Application mApplication;

    public TTSSpeaker(Application application, TTSCallback callback, UtteranceProgressListener utteranceProgressListener) {
        mApplication = application;
        mCallback = callback;
        mTTS = new TextToSpeech(mApplication, new TextToSpeech.OnInitListener() {
            @Override
            public void onInit(int status) {
                if (status == TextToSpeech.SUCCESS) {
                    int result = mTTS.setLanguage(Locale.TAIWAN);    //設定語言為中文
                    if (result == TextToSpeech.LANG_MISSING_DATA
                            || result == TextToSpeech.LANG_NOT_SUPPORTED) {
                        Log.e("TTS", "This Language is not supported");
                    } else {
                        mTTS.setPitch(1);    //語調(1為正常語調；0.5比正常語調低一倍；2比正常語調高一倍)
                        mTTS.setSpeechRate(1);    //速度(1為正常速度；0.5比正常速度慢一倍；2比正常速度快一倍)
                    }
                    mTTS.setOnUtteranceProgressListener(utteranceProgressListener);
                    mCallback.onReady();
                } else {
                    Log.e("TTS", "Initialization Failed!");
                    mCallback.onFail();
                }
            }

        });
    }

    public void speak(String message) {
        mTTS.speak(message, TextToSpeech.QUEUE_FLUSH, null, "tts1");
//        destroy();
    }

    public void destroy() {
            mTTS.shutdown();
    }
}
```

# Demo

{% youtube iSneVFi9J0I %}