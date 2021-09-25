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
下記のURLからDynamoDBのコンソール画面を開き、先ほど作成したテーブルを開き、項目の作成ボタンを押します。
https://ap-northeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-northeast-1#item-explorer?initialTagKey=&maximize=true&table=RegisterCouponInfoTBL
画像差し替え
![](https://storage.googleapis.com/zenn-user-upload/5xtnded86oxfy70aahw4ilgcoh8r)

- 項目の作成画面でデータを登録
下記のURLにアクセスしjsonのデータを全てコピーし、項目の作成画面の左上のセレクトボックスを`Text`にした後、先ほどコピーしたjsonデータをペーストしてください。
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiCouponInfo/smart_register_coupon_1.json
画像差し替え
![](https://storage.googleapis.com/zenn-user-upload/6zk3nlfdp559odgo5mbgj0jwejgk)

- データ登録の確認
データが正常に登録されたか、データレコードができていることを確認してください。
画像差し替え
![](https://storage.googleapis.com/zenn-user-upload/aod7nnsaredu1n1ujaygr90moaax)

# 商品データの登録
- DynamoDBのコンソール画面にアクセス
下記のURLからDynamoDBのコンソール画面を開き、先ほど作成したテーブルを開き、項目の作成ボタンを押します。
https://ap-northeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-northeast-1#item-explorer?initialTagKey=&table=RegisterItemInfoTBL
画像差し替え
![](https://storage.googleapis.com/zenn-user-upload/5xtnded86oxfy70aahw4ilgcoh8r)

- 項目の作成画面でデータを登録
下記のURLにアクセスしjsonのデータを全てコピーし、項目の作成画面の左上のセレクトボックスを`Text`にした後、先ほどコピーしたjsonデータをペーストしてください。
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_1.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_2.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_3.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_4.json
https://github.com/tacck/line-api-use-case-smart-retail/blob/main/backend/APP/dynamodb_data/SmaRegiItemInfo/smart_register_item_5.json
画像差し替え
![](https://storage.googleapis.com/zenn-user-upload/6zk3nlfdp559odgo5mbgj0jwejgk)

- データ登録の確認
データが正常に登録されたか、データレコードができていることを確認してください。
画像差し替え
![](https://storage.googleapis.com/zenn-user-upload/aod7nnsaredu1n1ujaygr90moaax)

# 動作確認しましょう！

全ての準備は整いました！
LIFEのURLをLINEアプリで起動して、動作確認してみてください！

https://youtu.be/ZBKGvAQKlIY