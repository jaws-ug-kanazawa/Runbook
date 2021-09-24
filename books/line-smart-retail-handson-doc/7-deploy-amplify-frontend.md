---
title: "Amplify構築手順(フロントエンド)"
---

## 本番（AWS）フロントエンド環境構築
- Amplifyマネージメントコンソールにアクセス
　https://ap-northeast-1.console.aws.amazon.com/amplify/home?region=ap-northeast-1#/create

    GitHubを選択し、`Continue`ボタンを押します。
    リポジトリの選択より line-api-use-case-smart-retail、ブランチの選択より main を選択し、`次へ`ボタンを押します。
    Advanced settingsをクリックして、以下の環境変数を設定し、`次へ`ボタンを押します。

    - LIFF_ID: LIFF アプリの LIFF IDを入力
    - BASE_URL: AWS APIGatewayのURLを入力
    - APIGATEWAY_STAGE: dev
    - AJAX_MODULE: amplify
    - SCANNER_MODULE: quagga
    - SCANDIT_LICENSE: xxxxxxxxxxxxxxxxxxxxxxxx

    設定内容を確認し、`保存してデプロイ`ボタンを押します。

- ドメインURLの取得
　　デプロイが完了したら、mainをクリックします。
　　表示されるドメインのURLを控えます。