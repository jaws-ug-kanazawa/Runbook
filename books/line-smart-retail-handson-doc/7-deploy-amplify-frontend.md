---
title: "Amplify構築手順(フロントエンド)"
---

## 本番（AWS）フロントエンド環境構築
- Amplifyマネージメントコンソールにアクセス
　https://ap-northeast-1.console.aws.amazon.com/amplify/home?region=ap-northeast-1#/create
  
    Host your web appの`Get Started`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/b12192549aa9b13b50273adf.png)

    GitHubを選択し、`Continue`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/ae67bddc8a149978793997a6.png)

    リポジトリの選択より line-api-use-case-smart-retail、ブランチの選択より main を選択し、`次へ`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/0d8b610db06820dfca34afb1.png)
    
    Advanced settingsをクリックして、以下の環境変数を設定し、`次へ`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/482ab5da8fe9bebc0e15f4cc.png)
    
    - LIFF_ID: LIFF アプリの LIFF IDを入力
    - BASE_URL: AWS APIGatewayのURLを入力
    - APIGATEWAY_STAGE: dev
    - AJAX_MODULE: amplify
    - SCANNER_MODULE: quagga
    - SCANDIT_LICENSE: xxxxxxxxxxxxxxxxxxxxxxxx
    ![](https://storage.googleapis.com/zenn-user-upload/bea1c5e618bff8ca45dd5e3d.png)

    設定内容を確認し、`保存してデプロイ`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/414332c89c07ab06c3552e17.png)

- ドメインURLの取得
　　デプロイが完了したら、mainをクリックします。
    ![](https://storage.googleapis.com/zenn-user-upload/41ab3292b25090a82c0c9175.png)
    
　　表示されるドメインのURLを控えます。
    ![](https://storage.googleapis.com/zenn-user-upload/2f8a88e68d99603ac7735f6d.png)