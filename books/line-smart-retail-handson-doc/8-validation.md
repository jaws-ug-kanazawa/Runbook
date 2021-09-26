---
title: "動作確認"
---

# LIFFのエンドポイントを変更

LINEログインのチャネル設定画面でLIFFのエンドポイントURLに、バックエンドの構築手順でメモしたドメインURLの値を設定して「更新」ボタンを押してください。

![](https://storage.googleapis.com/zenn-user-upload/1ead927c9020a339648dd322.png)

![](https://storage.googleapis.com/zenn-user-upload/82fc51c37438a41023d86027.png)

# LIFF公開する

「非公開」ボタンを押します。
![](https://storage.googleapis.com/zenn-user-upload/fd9ad5b36e64fef8e7f618b9.png =500x)

「公開」ボタンを押します。
![](https://storage.googleapis.com/zenn-user-upload/4ith4uysdvcsmv24zq13gb0i523a =500x)

# リッチメニューの作成
- リッチメニュー設定
Messaging API のチャネル基本設定画面でLINE Official Account Managerに移動します。
![](https://storage.googleapis.com/zenn-user-upload/9kg3ra1mdhtiic9fti3zt2xxl6xd)
ホーム→トーク管理→リッチメニュー→作成の順にクリックしましょう。
![](https://storage.googleapis.com/zenn-user-upload/ibwgawlq1fyc7b701c6429d8vlzm)

- 表示設定
下記のように設定しましょう。
![](https://storage.googleapis.com/zenn-user-upload/0505ede6d46b2b4a69885db2.png)

- テンプレート
次に、「テンプレートを選択」を押します。小の一番下を選択して、「選択」ボタンを押しましょう。
![](https://storage.googleapis.com/zenn-user-upload/ln4cuzjkvw9u4pyr8vo03p6e8tbx)

- 画像作成
次に、「画像を作成」を押します。リッチメニューの画像を作成できるので、お好みの背景色を選んでください。
![](https://storage.googleapis.com/zenn-user-upload/e656pkyqwvg9z3pg5mcu3ynecp8d)

「テキストを追加」を押して「スマートリテール」と入力します。中央揃えをして整えましょう。
![](https://storage.googleapis.com/zenn-user-upload/8f51423752927af38d554013.png)

できたら「適用」ボタンを2回押しましょう。（「ファイルに保存」ボタンを押すと画像としてダウンロードできます。）
![](https://storage.googleapis.com/zenn-user-upload/2c5bd0132541bd20c7278be6.png =500x)

- アクション設定
次にアクションを設定します。タイプを「リンク」にして、3. LINE ログインチャネルの作成でメモした「LIFF URL」を入力し、保存しましょう。
![](https://storage.googleapis.com/zenn-user-upload/a94289f10b338de948080fbf.png)


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
アプリで起動して、以下のバーコードを読み込んで動作確認してみてください！

- 書籍
![barcode_book](https://github.com/line/line-api-use-case-smart-retail/raw/main/docs/images/jp/barcode_isbn_book.png)

- りんご
![barcode_apple](https://github.com/line/line-api-use-case-smart-retail/raw/main/docs/images/jp/barcode_jan_apple.png)
- とまと

![barcode_tomato](https://github.com/line/line-api-use-case-smart-retail/raw/main/docs/images/jp/barcode_jan_tomato.png)

- すいか
![barcode_watermelon](https://github.com/line/line-api-use-case-smart-retail/raw/main/docs/images/jp/barcode_jan_watermelon.png)

https://youtu.be/ZBKGvAQKlIY