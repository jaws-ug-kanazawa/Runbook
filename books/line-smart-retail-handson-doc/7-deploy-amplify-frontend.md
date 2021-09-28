---
title: "Amplify構築手順(フロントエンド)"
---

## 本番（AWS）フロントエンド環境構築
- CodeCommitマネージメントコンソールにアクセス
　https://ap-northeast-1.console.aws.amazon.com/codesuite/codecommit/repositories?region=ap-northeast-1

    `リポジトリの作成`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/721bacb9d4da3ff0669d1a61.png)
    
    リポジトリ名に line-api-use-case-smart-retail と入力し、`作成`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/472069bb2ba6abb3621a5cdc.png)
    
    `コピー`ボタンの左側にあるコマンドが git clone https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/line-api-use-case-smart-retail  となっていることを確認します。
    ![](https://storage.googleapis.com/zenn-user-upload/4be91c538ba062f6038aee98.png)

- Cloud9環境で作成したリポジトリにpushする
:::message
下記のコマンドをコピペして実行しましょう！
:::
```
cd ~/environment/line-api-use-case-smart-retail/
git remote -v
git remote set-url origin https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/line-api-use-case-smart-retail
git remote -v
git push origin main
```

  以下のようになっていることを確認します。
  ![](https://storage.googleapis.com/zenn-user-upload/6e9a1e676666ee60c4c66f3d.png)

- Amplifyマネージメントコンソールにアクセス
　https://ap-northeast-1.console.aws.amazon.com/amplify/home?region=ap-northeast-1#/create
  
    Host your web appの`Get Started`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/b12192549aa9b13b50273adf.png)

    CodeCommitを選択し、`Continue`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/476404d5074323ee9cab9a6b.png)

    リポジトリの選択より line-api-use-case-smart-retail、ブランチの選択より main を選択し、`次へ`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/38ca5898e8b523c8459e59dd.png)
    
    Advanced settingsをクリックして、以下の環境変数を設定し、`次へ`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/feb029f2f3ad12787a9bb2eb.png))
    
    - LIFF_ID: LIFF アプリの LIFF IDを入力
    - BASE_URL: AWS APIGatewayのURLを入力
    - APIGATEWAY_STAGE: dev
    - AJAX_MODULE: amplify
    - SCANNER_MODULE: quagga
    - SCANDIT_LICENSE: xxxxxxxxxxxxxxxxxxxxxxxx
    ![](https://storage.googleapis.com/zenn-user-upload/bea1c5e618bff8ca45dd5e3d.png)

    設定内容を確認し、`保存してデプロイ`ボタンを押します。
    ![](https://storage.googleapis.com/zenn-user-upload/638916f5fee9f6088b1c17ee.png)

- ドメインURLの取得
　　デプロイが完了したら、mainをクリックします。
    ![](https://storage.googleapis.com/zenn-user-upload/41ab3292b25090a82c0c9175.png)
    
　　表示されるドメインのURLを控えます。
    ![](https://storage.googleapis.com/zenn-user-upload/2f8a88e68d99603ac7735f6d.png)