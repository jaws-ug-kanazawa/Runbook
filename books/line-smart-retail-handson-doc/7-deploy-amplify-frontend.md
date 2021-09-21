---
title: "Amplify構築手順(フロントエンド)"
---

## 本番（AWS）フロントエンド環境構築
- .env ファイルの設定

    `line-api-use-case-table-order/front/.env` ファイルの`xxxxxxxxx`の部分を変更してください。
    - LIFF_ID: LIFF アプリの LIFF IDを入力
    - BASE_URL: AWS APIGatewayのURLを入力

    ▼ .env ファイル
    ```` 
    # LIFF ID
    LIFF_ID=xxxxxxxxx-xxxxxxxxx

    # AXIOS BASE URL
    BASE_URL=https://xxxxxxxxx.execute-api.ap-northeast-1.amazonaws.com

    # API Gateway Stage
    APIGATEWAY_STAGE=dev

    # Ajax Module (axios or amplify)
    AJAX_MODULE=amplify
    ````

- node_modules インストール

    下記のコマンドを実行し、Node.js の依存パッケージ(node_modules)をインストールしてください。
    :::message
    下記のコマンドをコピペして実行しましょう！
    :::
    ```
    cd ~/environment/line-api-use-case-table-order/front
    npm install
    ``` 

- 静的ビルド

    下記のコマンドを実行し、S3 に配置する静的モジュール生成してください。
    :::message
    下記のコマンドをコピペして実行しましょう！
    :::
    ```
    cd ~/environment/line-api-use-case-table-order/front
    npm run build
    ```
    ビルドが完了したら front/dist フォルダが生成されています。 

- S3 にフロントエンドのモジュールを配置

    下記のコマンドを実行し、dist フォルダの中身をS3に配置してください。
    :::message
    下記のコマンドをコピペして実行しましょう！
    :::
    ```
    cd ~/environment/line-api-use-case-table-order/front
    aws s3 cp ./dist s3://lineawspaypay20210510＜バックエンドで指定したバケット名＞ --recursive
    ```