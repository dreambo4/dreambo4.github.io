---
title: 逆向工程-反編譯APK
date: 2018-01-26 00:32:15
tags:
- 反編譯
- 資安
- 逆向工程
- APK
---

* 本文曾發佈在 [https://hackmd.io/@yrw/BJeYauKdBz](https://hackmd.io/@yrw/BJeYauKdBz)

> **編輯紀錄**:
> 2020/09/24
> 補齊dex2jar詳細步驟、加入jd-gui

<!-- more -->
# 環境&材料
- 一台 Kali Linux
- 一個 APK

# 1. 解壓縮Apk檔

```shell=
$ unzip OOXX.apk
```
得到 `classes.dex`
![classes](classes.png) 

# 2. Dex to Jar

## 下載
https://sourceforge.net/projects/dex2jar/

## 解壓縮
解壓縮後，要讓裡面的程式都「可執行」
```shell=
unzip dex2jar-2.0.zip
cd dex2jar-2.0/
chmod +x d*
```
![unzip](unzip.png)

## 執行
轉檔成jar格式

```shell=
$ ./d2j-dex2jar.sh classes.dex
```

得到`classes-dex2jar.jar`

![classes-dex2jar](classes-dex2jar.png)

# 3. Jar to Java

有 gui 和 cmd 兩種版本，依需求取用
gui 可以 trace code 可能方便一些

## jd-gui

### 下載
http://java-decompiler.github.io/
![jd-gui](jd-gui.png)

### 執行
kali 預先有安裝 java 了，省略安裝步驟
```shell=
java -jar jd-gui-1.6.6.jar
```
開啟剛反編譯完的 `classes-dex2jar.jar`
![open-file](open-file.png)

就能看到java程式碼
![result](result.png)

## jd-cmd
https://github.com/kwart/jd-cmd

### 下載 

```shell=
$ git clone https://github.com/kwart/jd-cmd.git
```

### 安裝

下載後，可以在資料夾中找找到`hackingOnJdCmd.md`，裡面有安裝步驟

1. 首先要安裝Maven工具
```shell=
$ sudo apt-get install maven
```
> https://www.facebook.com/teacherchi/posts/830539233634000
> Maven 是一個「軟體開發流程」的「自動化工具」，一般人會撰寫時下一些指令、編譯時下另外一些指令、測試／除錯／版本維護又是下另外一些指令。
> Maven 可以讓你把每個流程輸入的指令，分門別類地記錄下來（當然，第一次還是要你用手工把它 Key 進去）。等於它有能力「模仿」你、把你每個流程打入的指令無限次「重現」。以後你只要一聲令下，就能把這一大堆指令，一口氣執行完畢。更棒的是，呼叫 Maven 時，可以從外部下一些小指令，客製化這些「每個流程要輸入的指令」的執行順序。因為軟體開發流程的「撰寫 --> 編譯 --> 測試 --> 除錯 --> 原始碼版本維護 --> ...」並非永遠依照固定順序執行、一成不變的。正因 Maven 可以彈性調整組合軟體開發過程中那一大堆鬼畫符般的指令，讓你不必背誦，它才會那麼受歡迎。
> **Maven之於Java，相當於Makefile之於C**
2. 安裝jd-cmd
```shell=
$ cd jd-cmd
$ mvn clean package
```

### 使用

1. 測試
```shell=
$ java -jar jd-cli/target/jd-cli.jar
```
2. 建立一個存放反編譯結果的資料夾
```shell=
$ mkdir ~/dex2jarTest/apk/OOXX/decompile 
```
3. 反編譯!
```shell=
$ java -jar jd-cli/target/jd-cli.jar [.jar路徑] -od [輸出路徑]
$ java -jar jd-cli/target/jd-cli.jar ~/dex2jarTest/apk/OOXX/classes-dex2jar.jar -od ~/dex2jarTest/apk/OOXX/decompile/
```
接著在decompile資料夾裡就可以看到反編譯完的結果囉~
