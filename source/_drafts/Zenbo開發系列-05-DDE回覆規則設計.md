---
title: '[Zenbo開發系列] 05-DDE回覆規則設計'
date: 2021-08-07 15:52:45
tags:
- Zenbo
- DDE
---

# 在 ASUS 平台註冊 APP
有完成這個步驟才能呼叫「嘿，Zenbo，我要用 `App name`」
首先需要先建立一個 Android 專案，要特別注意 Package name 等下會用到，所以請盡量取個不會跟別人重複的。
<!--more-->

> 習慣上 Package name 會用公司會學校或學校的 domian 相反過來。
> 例如: google.com -> com.google

再來你還需要一個 ASUS 帳號，就可以在 [Console](https://zenbo.asus.com/developer/console/) 註冊自己的 APP。
依序輸入打 * 號的幾個欄位，送出後可以看到生成好的 App ID 和 App Key。APP ID 會在設定 DDE 專案的地方用到。

![console_config](console_config.png)

# 建立 DDE 專案
從這邊 [DDE Editor](https://zenbo.asus.com/developer/tools/ds-editor.jsp) 建立一個新的 Project。

## 設定專案資訊
點選畫面上方的 info 設定
![info](info.png)
![project_info](project_info.png)

- **DDE Domain ID**: 如果是第一次使用，需要先註冊 (Register) 一個 DDE Domain ID，創建好點選 All 可以看到你所有的 DDE Domain 和相應的 UUID。UUID 之後在 Zenbo 端會用到。這個欄位是下拉式選單，記得選擇剛註冊的 Domain 哦。
- **Developer App ID**: 要選擇前面註冊好 Package name 的那組，下面的三個欄位會自動跟著填滿。
  - 確定 Developer App ID(App ID)、Package Name(Package Name)、Brand(Brand Name)、App Name(App Name) 和上一步驟一樣
- **Launch Activity**: 填寫你 APP 首頁 Activity 完整的 package 路徑。
- 剩下都預設就好~

## 設計 DDE 規則
各個 Basic Contexts 的說明可以看我的上一篇文章 [[Zenbo開發系列] 04-DDE簡介](../../07/Zenbo開發系列-04-DDE簡介)

### 流程
因為我做的是一個 Q&A 的聊天機器人，我希望使用使用者可以一直問完一題再問下一題，但是 Zenbo 一般問題流程會比較像樹狀結構，一條路走到底就結束了，沒辦法接下一題。

所以我後來借用 Plans 的 Input/Output Contexts 參數達到可以一題接一題的效果。流程大致如下圖。

![flow](flow.jpg)

### Concepts
把同樣概念的詞，做成一個個 Concepts，我截幾個作範例。

![concepts1](concepts1.png)
![concepts2](concepts2.png)

- Concept ID: 這個 Concepts 的名稱，可以用中文。
- Instances: 先不用建，等下在 Concept 有用到的時候再加就好。

### Intents
舉出一個「意圖」所有可能的說法。例如說，我今天想申請長照，就可以有很多種說法，「我要申請長照」、「申請長照」、「我想申請長照」、「如何申請長照」、「申請長照的流程」，盡可能把各種你想得到、想不到的講法都寫上去。

> 官方文件:
> 人們可能使用不同句子來表達自己的意圖，因此開發人員有責任枚舉所有可能的句子。

![Intents1](Intents1.png)
![Intents2](Intents2.png)

圖中可以看到詞分種 3 種顏色，藍色、橘色、淺橘，代表不同的用意


#### 藍色
一定要出現的常數，而且一定要相同。像 applyLTC 的第一個例句中"我"，如果輸入的句子中是"你"，就比對不到，一定要是"我"。

可以在這裡建立新的 Concept，或是加入一個原有的 Concept
![Intents3](Intents3.png)
![Intents4](Intents4.png)

#### 橘色
和 Concept 綁定的詞。

#### 淺橘
和橘色一樣，但是 optional 的，可以不用出現。
![Intents5](Intents5.png)