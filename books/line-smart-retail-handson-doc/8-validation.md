---
title: "動作確認"
---

# LIFFのエンドポイントを変更

LINEログインのチャネル設定画面でLIFFのエンドポイントURLに、バックエンドの構築手順でメモしたドメインURLの値を設定して「更新」ボタンを押してください。

![](https://storage.googleapis.com/zenn-user-upload/4xntpxietdrhyrsm4boio81g7zyq)

![](https://storage.googleapis.com/zenn-user-upload/82fc51c37438a41023d86027.png)

# LIFF公開する

「非公開」ボタンを押します。
![](https://storage.googleapis.com/zenn-user-upload/mhgpfl6m6a6bd2gliq0pwfgio8kc =500x)

「公開」ボタンを押します。
![](https://storage.googleapis.com/zenn-user-upload/4ith4uysdvcsmv24zq13gb0i523a =500x)

# クーポンデータの登録
- DynamoDBのコンソール画面にアクセス
下記のURLで表示されるDynamoDBのコンソール画面でRegisterCouponInfoTBLテーブルを開き、`項目の作成`ボタンを押します。
https://ap-northeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-northeast-1#item-explorer?initialTagKey=&maximize=true&table=RegisterCouponInfoTBL
![](https://storage.googleapis.com/zenn-user-upload/595f42031e964fb754a424c6.png)

- 項目の作成画面でデータを登録
項目の作成画面の左上のDynamoDB JSONの表示がオフになっていて、右上のボタンが`JSON`になっていることを確認の上、下記のURLにあるjsonのデータをコピー＆ペーストしてください。
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiCouponInfo/smart_register_coupon_1.json
![](https://storage.googleapis.com/zenn-user-upload/155c28baaca0fab831334ade.png)

- データ登録の確認
データが正常に登録されたか、データレコードができていることを確認してください。
![](https://storage.googleapis.com/zenn-user-upload/970f80e1519b821f4fcfa4bd.png)

# 商品データの登録
- DynamoDBのコンソール画面にアクセス
下記のURLで表示されるDynamoDBのコンソール画面で、RegisterItemInfoTBLテーブルを開き、`項目の作成`ボタンを押します。
https://ap-northeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-northeast-1#item-explorer?initialTagKey=&table=RegisterItemInfoTBL

- 項目の作成画面でデータを登録
項目の作成画面の左上のDynamoDB JSONの表示がオフになっていて、右上のボタンが`JSON`になっていることを確認の上、下記のURLにあるjsonのデータをコピー＆ペーストしてください。
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_1.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_2.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_3.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_4.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_5.json
![](https://storage.googleapis.com/zenn-user-upload/5923bde8e7c6b434909caa63.png)

- データ登録の確認
データが正常に登録されたか、データレコードができていることを確認してください。
![](https://storage.googleapis.com/zenn-user-upload/8f7e1f249e43232aba1a36ef.png)

# 動作確認しましょう！

全ての準備は整いました！
LIFEのURLをLINEアプリで起動して、動作確認してみてください！

https://youtu.be/ZBKGvAQKlIY