---
title: CodeIgniter安裝Swagger
date: 2019-08-20 01:19:26
tags:
- CodeIgniter
- Swagger
- API
---

* 本文曾發佈在 [https://hackmd.io/@yrw/S1TdomtNS](https://hackmd.io/@yrw/S1TdomtNS)

> 環境: Windows、XAMPP

1. 下載CodeIgniter
<!-- more -->
2. 建資料夾`YourProject/swagger/`
3. 下載[Swagger UI](https://github.com/swagger-api/swagger-ui)，解壓縮，將`dist/`資料夾裡的檔案全搬到`YourProject/swagger/`
	![dir](dir.png)
4. 安裝
	```shell
	composer require zircote/swagger-php:2.*
	```
5. 有需要的話，安裝
	```shell
	composer require darkaonline/l5-swagger
	```
6. 建立Controller(Member)
7. 加上一些註解 swg annotation
一份專案裡至少需要一個`@SWG\Info`的註解
	```php
	/**
	 * 这里需要一个主`Swagger`定义：
	 * @SWG\Swagger(
	 *     @SWG\Info(
	 *         title="我的`Swagger`API文檔",
	 *         version="1.0.0"
	 *     )
	 * )
	 */
	```

8. 加上一些方法和註解
	```php
	/**
	 * @SWG\Post(
	 *     path="/YourProject/index.php/Member/login",
	 *     tags={"會員功能"},
	 *     summary="登入",
	 *     @SWG\Parameter(
	 *         in="query",
	 *         name="account",
	 *         type="string",
	 *         description="帳號",
	 *         required=true,
	 *     ),
	 *     @SWG\Parameter(
	 *         in="query",
	 *         name="password",
	 *         type="string",
	 *         description="密碼",
	 *         required=true,
	 *     ),
	 *     @SWG\Response(response="default", description="操作成功")
	 * )
	 *
	 */
	public   function   login()
	{
		echo '{"msg":"hello world"}';
	}
	```

9. 下指令生成API 文件檔(json格式)
路徑和檔名可以自行調整

	> php [swagger程式位置] [Controller資料夾(需要掃描的資料夾)] -o [api文件生成位置]

	```shell
	php /xampp/htdocs/YourProject/vendor/zircote/swagger-php/bin/swagger /xampp/htdocs/YourProject/application/controllers -o \xampp\htdocs\YourProject\api_doc.json
	```
	
10. 修改`YourProject/swagger/index.html`
    改成你的api文件位置
    http://127.0.0.1/YourProject/api_doc.json
    ![edit](edit.png)

11. 瀏覽 http://127.0.0.1/Swagger_CodeIgniter/swagger/
    **沒更新的話，用無痕瀏覽**
    ![show](show.png)

