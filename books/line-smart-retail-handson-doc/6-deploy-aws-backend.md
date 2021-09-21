---
title: "バックエンドの構築手順"
---

# バックエンドの構築手順

## 概要

AWS SAM(AWS サーバーレスアプリケーションモデル)を使い、下記の`APP`、`batch`、`Layer`のフォルダ内のリソースをそれぞれデプロイします。

```
line-api-use-case-table-order/
  ├ backend/
  │  ├ APP/
  │     ├ ...
  │  ├ batch/
  │     ├ ...
  │  └ Layer/
  │     ├ ...
  ...
```

- APP:メインの処理
- batch:LINEアクセストークン定期更新・取得バッチ(短期アクセストークン有効期限 30日)
- Layer:共通処理を内包、Lambda Layerとしてデプロイする

## Layerフォルダのリソースをデプロイ(共通処理)

- template.yaml の修正（今回のハンズオンでは修正せずデフォルトの値でも大丈夫です。）
:::details 参考）修正が必要になった場合
下記ファイル内のパラメータを修正します。
https://github.com/jaws-ug-kanazawa/line-api-use-case-table-order/blob/master/backend/Layer/template.yaml#L24

```
      LayerName: 任意のレイヤー名
```
:::

- 以下のコマンドを実行してデプロイします。

:::message
下記のコマンドをコピペして実行しましょう！
:::

```shell
cd ~/environment/line-api-use-case-table-order/backend/Layer
sam build --use-container
sam deploy --guided
```

```
    Stack Name [sam-app]: line-aws-paypay-layer-20210510
    AWS Region [ap-northeast-1]: ap-northeast-1
    Parameter Environment [dev]: dev
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
    Confirm changes before deploy [y/N]: y
    #SAM needs permission to be able to create roles to connect to the resources in your template
    Allow SAM CLI IAM role creation [Y/n]: Y
    Save arguments to configuration file [Y/n]: Y

    SAM configuration file [samconfig.toml]: 入力せずEnter 
    SAM configuration environment [default]: 入力せずEnter
    
    Deploy this changeset? [y/N]: y
```

本ハンズオンではLayerのデプロイは１回だけを想定してますが、２回以上デプロイを実施した場合は以降の手順で `LayerVersion` の値を修正する必要があります。

## batchフォルダのリソースをデプロイ(アクセストークン定期更新・取得バッチ)

- template.yaml の修正（今回のハンズオンでは修正せずデフォルトの値でも大丈夫です。）
:::details 参考）修正が必要になった場合
下記ファイル内のパラメータを修正します。
https://github.com/jaws-ug-kanazawa/line-api-use-case-table-order/blob/master/backend/batch/template.yaml#L23

```
      LINEChannelAccessTokenDBName: LINEChannelAccessTokenDBTableOrderDev
      EventBridgeName: EventBridgeNameTableOrderDev
      LayerVersion: Layer 1
      LoggerLevel: DEBUG
```
:::

- 以下のコマンドを実行してデプロイします。

:::message
下記のコマンドをコピペして実行しましょう！
:::

```shell
cd ~/environment/line-api-use-case-table-order/backend/batch
sam build --use-container
sam deploy --guided
```

```
    Stack Name [sam-app]: line-aws-paypay-batch-20210510
    AWS Region [ap-northeast-1]: ap-northeast-1
    Parameter Environment [dev]: dev
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
    Confirm changes before deploy [y/N]: y
    #SAM needs permission to be able to create roles to connect to the resources in your template
    Allow SAM CLI IAM role creation [Y/n]: Y
    Save arguments to configuration file [Y/n]: Y
        
    SAM configuration file [samconfig.toml]: 入力せずEnter 
    SAM configuration environment [default]: 入力せずEnter
    
    Deploy this changeset? [y/N]: y
```

- テーブルにチャネル ID とチャネルシークレットを登録する
  - DynamoDBのコンソール画面にアクセス
下記のURLからDynamoDBのコンソール画面を開き、先ほど作成したテーブルを開き、`項目の作成`ボタンを押します。
https://ap-northeast-1.console.aws.amazon.com/dynamodb/home?region=ap-northeast-1#tables:selected=LINEChannelAccessTokenDBTableOrderDev;tab=items
![](https://storage.googleapis.com/zenn-user-upload/kw2k8nmxpd5gceb493ww8x7hgb1g)
  - 項目の作成画面でデータを登録
  項目の作成画面でMessaging APIのチャネルの`チャネルID`と`チャネルシークレットキー`を登録します。（`チャネルID`と`チャネルシークレットキー`は[LINE Developers コンソール](https://developers.line.biz/console/)のチャネル基本設定にて確認できます。）
    - channelId: チャネル ID (文字列)
    - channelSecret: チャネルシークレット(文字列)
![](https://storage.googleapis.com/zenn-user-upload/ue8y75t0geax37ta0k5rjg1flx8n)
![](https://storage.googleapis.com/zenn-user-upload/06suku5nij1vjehxdvssfuen3tdx)
      
- チャネルアクセストークン更新の Lambda 関数を実行する
  - AWS マネジメントコンソールにログインし、Lambda のコンソールを開く
下記のURLからLambdaのコンソールにアクセスし、テストイベントの設定画面を表示します。
https://ap-northeast-1.console.aws.amazon.com/lambda/home?region=ap-northeast-1#/functions/TableOrder-PutAccessToken-dev?tab=testing
  - テストイベントの設定に必要な情報を入力し右上の`テスト`ボタンを押下してLambdaを実行します。
    - テンプレート: `hello-world`を選択
    - 名前: test
    - 一番下のテキストボックス : `{}`
![](https://storage.googleapis.com/zenn-user-upload/2uf5toitic64ldxs54rq6j7gqdlc)

- 【確認】DynamoDBのテーブルに必要な情報が入ったかを確認
下記のURLからDynamoDBのコンソール画面を開き、`channelAccessToken`,`limitDate`の項目が追加されていることを確認します。
https://ap-northeast-1.console.aws.amazon.com/dynamodb/home?region=ap-northeast-1#tables:selected=LINEChannelAccessTokenDBTableOrderDev;tab=items
![](https://storage.googleapis.com/zenn-user-upload/2oeg8n311z7u0pea6ijt4czenkm2)

## APPフォルダのリソースをデプロイ

以下の手順で、アプリ本体をデプロイしてください。

- template.yaml の修正  
下記ファイル内のパラメータを修正します。
https://github.com/jaws-ug-kanazawa/line-api-use-case-table-order/blob/master/backend/APP/template.yaml#L24
    - LineChannelId: Messaging API チャネルのチャネル IDを入力
    - LIFFChannelId: LINEログイン チャネルのチャネル IDを入力
    - LiffUrl: LIFF URLを入力(https://liff.line.me/xxxxxxxxx-xxxxxxxxx)
    - PayPayApiKey: PayPayサンドボックス利用設定でメモしたAPIキーを入力
    - PayPayApiSecret: PayPayサンドボックス利用設定でメモしたシークレットキーを入力
    - PayPayApiMerchantId: PayPayサンドボックス利用設定でメモしたMERCHANT IDを入力
    - PayPayIsProd: Falseを指定
    - FrontS3BucketName: lineawspaypay20210510＜任意の値で全て英数字小文字(例：メールアドレスの@より上の部分など)＞
    - LayerVersion: 1 (Layerのバージョンを指定。今回は基本的に1でOK)
```
      LineChannelId: LineChannelId
      LIFFChannelId: LIFFChannelId
      LiffUrl: https://liff.line.me/xxxxxxxxx-xxxxxxxxx
      PayPayApiKey: PayPayApiKey
      PayPayApiSecret: PayPayApiSecret
      PayPayApiMerchantId: PayPayApiMerchantId
      PayPayIsProd: False
      FrontS3BucketName: S3 Name for FrontEnd
      LayerVersion: 1
```

- 以下のコマンドを実行してデプロイします。

:::message
下記のコマンドをコピペして実行しましょう！
:::

```shell
cd ~/environment/line-api-use-case-table-order/backend/APP
sam build --use-container
sam deploy --guided
```

```
    Stack Name : line-aws-paypay-app-20210510
    AWS Region : ap-northeast-1
    Parameter Environment: dev
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy Confirm changes before deploy [Y/n]: Y
    #SAM needs permission to be able to create roles to connect to the resources in your template Allow SAM CLI IAM role creation[Y/n]: Y
    ××××× may not have authorization defined, Is this okay? [y/N]: y (約10個全てyと入力)  
    Save arguments to configuration file [Y/n]: Y

    SAM configuration file [samconfig.toml]: 入力せずEnter 
    SAM configuration environment [default]: 入力せずEnter
    
    Deploy this changeset? [y/N]: y
```

- API Gateway endpoint URLとCloudFrontDomainNameのメモ  
デプロイ成功時にOutPutにて表示されるAPI Gateway endpoint URLとCloudFrontDomainNameのメモを取ってください。