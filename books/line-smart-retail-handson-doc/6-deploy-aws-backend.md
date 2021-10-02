---
title: "バックエンドの構築手順"
---

# バックエンドの構築手順

## 概要

AWS SAM(AWS サーバーレスアプリケーションモデル)を使い、下記の`APP`、`batch`、`Layer`のフォルダ内のリソースをそれぞれデプロイします。

```
line-api-use-case-smart-retail/
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

- template.yaml の修正
:::details 参考）修正が必要になった場合
下記ファイル内のパラメータを修正します。
![](https://storage.googleapis.com/zenn-user-upload/9fab646cd01919a4d55a48e9.png)

```
      LayerName: 任意のレイヤー名
```
:::

- 以下のコマンドを実行してデプロイします。

:::message
下記のコマンドをコピペして実行しましょう！
:::

```shell
cd ~/environment/line-api-use-case-smart-retail/backend/Layer/
sam build --use-container
sam deploy --guided
```

```
    Stack Name [sam-app]: line-api-use-case-smart-retail-layer-20211002
    AWS Region [ap-northeast-1]: ap-northeast-1
    Parameter Environment [dev]: dev
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
    Confirm changes before deploy [Y/N]: Y
    #SAM needs permission to be able to create roles to connect to the resources in your template
    Allow SAM CLI IAM role creation [Y/n]: Y
    Save arguments to configuration file [Y/n]: Y

    SAM configuration file [samconfig.toml]: 入力せずEnter 
    SAM configuration environment [default]: 入力せずEnter
    
    (しばらく待ちます)

    Deploy this changeset? [y/N]: y
```

本ハンズオンではLayerのデプロイは１回だけを想定してますが、２回以上デプロイを実施した場合は以降の手順で `LayerVersion` の値を修正する必要があります。

## batchフォルダのリソースをデプロイ(アクセストークン定期更新・取得バッチ)

- template.yaml の修正
:::details 参考）修正が必要になった場合
下記ファイル内のパラメータを修正します。
![](https://storage.googleapis.com/zenn-user-upload/5978d27c15557c8d1365c328.png)

```
    dev:
      LINEChannelAccessTokenDBName: LINEChannelAccessTokenTBL
      EventBridgeName: AmplifyEventBridge
      LayerVersion: Layer 1
      LoggerLevel: DEBUG
```
:::

- 以下のコマンドを実行してデプロイします。

:::message
下記のコマンドをコピペして実行しましょう！
:::

```shell
cd ~/environment/line-api-use-case-smart-retail/backend/batch
sam build --use-container
sam deploy --guided
```

```
    Stack Name [sam-app]: line-api-use-case-smart-retail-batch-20211002
    AWS Region [ap-northeast-1]: ap-northeast-1
    Parameter Environment [dev]: dev
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
    Confirm changes before deploy [Y/N]: Y
    #SAM needs permission to be able to create roles to connect to the resources in your template
    Allow SAM CLI IAM role creation [Y/n]: Y
    Save arguments to configuration file [Y/n]: Y
        
    SAM configuration file [samconfig.toml]: 入力せずEnter 
    SAM configuration environment [default]: 入力せずEnter
    
    (しばらく待ちます)

    Deploy this changeset? [y/N]: y
```

- テーブルにチャネル ID とチャネルシークレットを登録する
  - DynamoDBのコンソール画面にアクセス
下記のURLからDynamoDBのコンソール画面を開き、先ほど作成したテーブルを開き、`項目の作成`ボタンを押します。
https://ap-northeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-northeast-1#item-explorer?initialTagKey=&maximize=true&table=LINEChannelAccessTokenTBL
![](https://storage.googleapis.com/zenn-user-upload/8830331679787eb0211da779.png)
  - 項目の作成画面でデータを登録
  項目の作成画面でMessaging APIのチャネル(※LINE Loginのチャネルではありません)の`チャネルID`と`チャネルシークレットキー`を登録します。（`チャネルID`と`チャネルシークレットキー`は[LINE Developers コンソール](https://developers.line.biz/console/)のチャネル基本設定にて確認できます。）
    - channelId: チャネル ID (文字列)
    - channelSecret: チャネルシークレット(文字列)
![](https://storage.googleapis.com/zenn-user-upload/24637064fecc9704decbe640.png)
      
- チャネルアクセストークン更新の Lambda 関数を実行する
  - AWS マネジメントコンソールにログインし、Lambda のコンソールを開く
下記のURLからLambdaのコンソールにアクセスし、テストイベントの設定画面を表示します。
https://ap-northeast-1.console.aws.amazon.com/lambda/home?region=ap-northeast-1#/functions/SmartRegister-PutAccessToken-dev?tab=testing
  - テストイベントの設定に必要な情報を入力し右上の`テスト`ボタンを押下してLambdaを実行します。
    - テンプレート: `hello-world`を選択
    - 名前: test
    - 一番下のテキストボックス : `{}`
![](https://storage.googleapis.com/zenn-user-upload/7fd9aafada73df4520895d3d.png)

- 【確認】DynamoDBのテーブルに必要な情報が入ったかを確認
下記のURLからDynamoDBのコンソール画面を開き、`channelAccessToken`,`limitDate`の項目が追加されていることを確認します。
https://ap-northeast-1.console.aws.amazon.com/dynamodbv2/home?region=ap-northeast-1#item-explorer?initialTagKey=&table=LINEChannelAccessTokenTBL
![](https://storage.googleapis.com/zenn-user-upload/f7d894a603843abb11fefe20.png)

## APPフォルダのリソースをデプロイ

以下の手順で、アプリ本体をデプロイしてください。

- template.yaml の修正  
下記ファイル内のパラメータを修正します。
![](https://storage.googleapis.com/zenn-user-upload/f726c8eed24044a5b1fdbc76.png)

    - LineOAChannelId: Messaging API チャネルのチャネル IDを入力
    - LIFFChannelId: LINEログイン チャネルのチャネル IDを入力
    - LiffUrl: LIFF URLを入力(https://liff.line.me/xxxxxxxxx-xxxxxxxxx)
    - PayPayApiKey: PayPayサンドボックス利用設定でメモしたAPIキーを入力
    - PayPayApiSecret: PayPayサンドボックス利用設定でメモしたシークレットキーを入力
    - PayPayApiMerchantId: PayPayサンドボックス利用設定でメモしたMERCHANT ID(加盟店ID)を入力
    - PayPayIsProd: Falseを指定してください。
    - RegisterOrderInfoDBName: RegisterOrderInfoTBL（注文情報を登録するテーブル）
    - RegisterItemInfoDBName: RegisterItemInfoTBL（商品情報を登録するテーブル）
    - RegisterCouponInfoDBName: RegisterCouponInfoTBL（クーポン情報を登録するテーブル）
    - LINEChannelAccessTokenDBName: LINEChannelAccessTokenTBL（デプロイした「短期チャネルアクセストークンを管理するテーブル」のテーブル名）
    - ConfirmUrlPass: /completed.html（LINEPay決済完了後に遷移するパス）
    - DetailsPass: /history.html（注文履歴画面のパス）
    - PaymentImageUrl: https://media.istockphoto.com/vectors/cash-register-with-a-paper-check-flat-isolated-vector-id1018485968
    - LayerVersion: 1 (Layerのバージョンを指定。今回は基本的に1でOK)
```
      LineOAChannelId: LineOAChannelId
      LIFFChannelId: LIFFChannelId
      LiffUrl: https://liff.line.me/xxxxxxxxx-xxxxxxxxx
      PayPayApiKey: PayPayApiKey
      PayPayApiSecret: PayPayApiSecret
      PayPayApiMerchantId: PayPayApiMerchantId
      PayPayIsProd: False
      RegisterOrderInfoDBName: RegisterOrderInfoTBL
      RegisterItemInfoDBName: RegisterItemInfoTBL
      RegisterCouponInfoDBName: RegisterCouponInfoTBL
      LINEChannelAccessTokenDBName: LINEChannelAccessTokenTBL
      ConfirmUrlPass: /completed.html
      DetailsPass: /history.html
      PaymentImageUrl: "https://media.istockphoto.com/vectors/cash-register-with-a-paper-check-flat-isolated-vector-id1018485968"
      LayerVersion: 1
```

- 以下のコマンドを実行してデプロイします。

:::message
下記のコマンドをコピペして実行しましょう！
:::

```shell
cd ~/environment/line-api-use-case-smart-retail/backend/APP
sam build --use-container
sam deploy --guided
```

```
    Stack Name [line-smart-retail-app] : line-api-use-case-smart-retail-app-20211002
    AWS Region　[ap-northeast-1]: ap-northeast-1
    Parameter Environment　[dev]: dev
    #Shows you resources changes to be deployed and require a 'Y' to initiate deploy
    Confirm changes before deploy [Y/n]: Y
    #SAM needs permission to be able to create roles to connect to the resources in your template
    Allow SAM CLI IAM role creation[Y/n]: Y
    ××××× may not have authorization defined, Is this okay? [y/N]: y (6個全てyと入力)  
    Save arguments to configuration file [Y/n]: Y

    SAM configuration file [samconfig.toml]: 入力せずEnter 
    SAM configuration environment [default]: 入力せずEnter
    
    (しばらく待ちます)

    Deploy this changeset? [y/N]: y
```

- API Gateway endpoint URLのメモ  
デプロイ成功時にOutPutにて表示されるAPI Gateway endpoint URL(API Gateway endpoint URL for xxx の３つのURLはいずれも https://vxxxxxl.execute-api.ap-northeast-1.amazonaws.com/ となっていますのでどれを利用しても構いません)のメモを取ってください。


```
CloudFormation outputs from deployed stack
-----------------------------------------------------------------------------------------
Outputs                                                                                                                                                                                                                                                     
-----------------------------------------------------------------------------------------
Key                 LineOAChannelId                                                                                                                                                                                                                         
Description         MessagingAPILineChannelId                                                                                                                                                                                                              
Value               1xxxxxxxx8

Key                 GetOrderInfoApi                                                                                                                                                                                                                         
Description         API Gateway endpoint URL for GetOrderInfo function                                                                                                                                                                                      
Value               https://vxxxxxl.execute-api.ap-northeast-1.amazonaws.com/dev/get_order_info/                                                                                                                                                         

Key                 GetItemInfoFunction                                                                                                                                                                                                                     
Description         GetItemInfo Lambda Function ARN                                                                                                                                                                                                         
Value               arn:aws:lambda:ap-northeast-1:7xxxxxxx5:function:SmartRegister-GetItemInfo-dev                                                                                                                                                       

Key                 GetOrderInfoFunction                                                                                                                                                                                                                    
Description         GetOrderInfo Lambda Function ARN                                                                                                                                                                                                        
Value               arn:aws:lambda:ap-northeast-1:7xxxxxxxx5:function:SmartRegister-GetOrderInfo-dev                                                                                                                                                      

Key                 PutCartDataFunction                                                                                                                                                                                                                     
Description         PutCartData Lambda Function ARN                                                                                                                                                                                                         
Value               arn:aws:lambda:ap-northeast-1:7xxxxxxxx5:function:SmartRegister-PutCartData-dev                                                                                                                                                       

Key                 PutCartDataApi                                                                                                                                                                                                                          
Description         API Gateway endpoint URL for PutCartData function                                                                                                                                                                                       
Value               https://vxxxxxl.execute-api.ap-northeast-1.amazonaws.com/dev/put_cart_data/                                                                                                                                                          

Key                 GetItemInfoApi                                                                                                                                                                                                                          
Description         API Gateway endpoint URL for GetItemInfo function                                                                                                                                                                                       
Value               https://vxxxxxxl.execute-api.ap-northeast-1.amazonaws.com/dev/get_item_info/                                                                                                                                                          

Key                 LIFFChannelId                                                                                                                                                                                                                           
Description         LIFF ChannelId                                                                                                                                                                                                                          
Value               1xxxxxxxx6
                                                                               
-----------------------------------------------------------------------------------------

Successfully created/updated stack - line-api-use-case-smart-retail-app-20211002 in ap-northeast-1
```