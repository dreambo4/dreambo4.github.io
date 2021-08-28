---
title: Workshop記錄-Volley與API
date: 2019-07-13 12:39:12
tags:
- Android
- 行雲部落格
- 行雲者 Workshop
- Volley
- API
---

* 本文曾發佈在 [https://blog.cmrdb.cs.pu.edu.tw/?p=981](https://blog.cmrdb.cs.pu.edu.tw/?p=981)

對於Volley，我一直以來都只是會用，不曾深入了解。2019/05/18-19，我們規劃了一場Workshop，希望能讓新進的夥伴了解，API怎麼開？怎麼接？讓未來各組在專案的合作上可以更了解彼此的想法。

沒想到在事前準備教材的過程中，我也收穫了不少，雖然有點可惜，Workshop那天沒有講完。這篇文章主要記錄我學到的Volley用法，與整理Workshop當天的教材，也包括來不及講到的部分。
<!-- more -->

# 簡介
Volley是Google於2013年推出的網路連線框架，讓連線可以更簡單、快速。簡化了HTTP程式處理邏輯與提高執行效率。由於Volley快取的特性，適合頻繁、資料量小的傳輸。如果是較大流量傳輸，可以考慮HttpURLConnection、HttpClient等其他方式。

![](8azZ7hm.png)
(Life of a request. 節自 [Android開發指南](https://developer.android.com/training/volley/simple.html))

當一個Request被加到Queue之後，會先檢查Cache中有沒資料，如果有，就會直接從Cache中回傳；如果沒有，再到網路上存取。

# Volley和API可以做什麼

- 搭配網路連線的APP，能做的應用更多
- 行雲者近期的APP專案常用Volley串接API
- 透過API，可以傳資料到伺服器，或從伺服器取得資料

其實我有找到一個套件可以讓手機可以直接和資料庫連線，JDBC。
但是不知道各位有想過，為什麼我們不用APP，直接存取伺服器資料庫的內容嗎？

這個其實我還沒有確切的答案，以下是我的想法：
- 透過API我們可以統一取得的內容與格式，我們可以統一API的格式，例如JSON。不管是Android、iOS或網頁，都可以透過同一支API拿到一樣的資料。
- 另外，是安全性問題。當APK被反編譯，可能可以取的程式碼裡面，資料庫的IP、帳號、密碼等資訊。

# 實作

1. 載入套件
在`build.gradle(Module: app)`中載入volley的套件
```
compile 'com.android.volley:volley:1.1.1
```
![](x4k4a8r.png)

2. 網路權限
在`AndroidMenifest.xml`加網路權限
	```xml
	<uses-permission android:name="android.permission.INTERNET" />
	```

3. *程式碼中的用到的API都放在文章最後的附錄* 

## StringRequest(Get)

1. 宣告變數
TextView是等下要用來顯示回傳內容的
![](K8ldhLr.png)

2. Volley
![](qqFqCG4.png)

3. 顯示內容
![](KbWN5Kh.png)

## JsonObjectRequest

JSON Object 最外層的的括號是 { }
![](rwp2EGF.png)

## JsonArrayRequest

JSON Object 最外層的的括號是 [ ]
![](Z1s0ujZ.png)

## StringRequest(Post)
在大括號內按 Ctrl-O 搜尋 getParams() 可以補齊
下面Map<String,String> params的內容就是要傳給API的Key和Value
![](5IqdECc.png)

## ImageRequest
1. 先加個ImageView
![](UeTe6ah.png)

2. 宣告變數
![](wUXkrzO.png)

3. Volley
圖片可以自己找網路上的
![](DQqIxdO.png)

# 附錄
這邊有些簡單測試資料，如果沒有自己的Web Server，可以試試[JSON Generator](https://next.json-generator.com/NJd7BqW-P)。

- string.txt
```=
This is a string!!
```

- jsonArr.php
```php=
<?php 
	echo '[ "Ford", "BMW", "Fiat" ]';
?>
```

- jsonObj.php
```php=
<?php 
	echo '{ "name":"John", "age":30, "car":null }';
?>
```

- jsonPost.php
```php=
<?php 
	$id = $_POST['id'];
	$pwd = $_POST['pwd'];

	if($id != "" && $pwd != ""){
		echo json_encode(array('id' => $id, 'pwd' => $pwd));
	}else{
		echo json_encode(array('msg' => "Please enter ID and password !"));
	}
	
?>
```

- login.php
```php=
<?php 
	$id = $_POST['account'];
	$pwd = $_POST['passwd'];

	if($id == "" || $pwd == ""){
		echo json_encode(array('success' => "0", 'message' => "Please enter ID and password !"));
	}else if($pwd == "2019workshop"){
		echo json_encode(array('success' => "1", 'message' => "Login Success!", 'data' => $id));
	}else{
		echo json_encode(array('success' => "0", "message" => "Login Failed !"));
	}	
	
?>
```
