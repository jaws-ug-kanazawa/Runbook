---
title: "スケジュールスケーリング（１）~起動テンプレートの作成~"
---

# ユーザデータのダウンロード

[https://pages.awscloud.com/rs/112-TZM-766/images/h4b-ec2autoscaling-userdata.zip](https://pages.awscloud.com/rs/112-TZM-766/images/h4b-ec2autoscaling-userdata.zip)
よりダウンロードしたzipファイルを解凍します。

# 起動テンプレートの作成

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchTemplates:](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchTemplates:)
よりEC2起動テンプレートのコンソール画面を開き、`起動テンプレートを作成`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/1974ef60fb91e700b18cf7f2.png)

以下の内容を設定します。
起動テンプレート名　`autoscaling-handson20211013`　を入力
Amazon マシンイメージ（AMI）　`Amazon Linux 2 AMI (HVM), SSD Volume Type` を選択
インスタンスタイプ　t2.micro を選択
セキュリティグループ　h4b-ec2-sg

![](https://storage.googleapis.com/zenn-user-upload/f43c373da84a7b5587d007f5.png)

リソースタグで`タグを追加`をクリックし、以下の内容を追加します。
キー　`Name`　を入力
値　`autoscaling-handson20211013`　を入力
リソースタイプ　`インスタンス`　を選択

高度な詳細を開き、以下の内容を入力します。
CloudWatchモニタリングの詳細　有効化
ユーザデータ　先程ダウンロードしたzipファイルを解凍して得られる`h4b-ec2autoscaling-userdata.txt`をエディタなどで開いた上で、内容を貼り付け`起動テンプレートの作成`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/d91d860f66bd9555dbc97fcf.png)

# オートスケーリンググループの作成

[https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/](https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/)
よりAuto Scaling グループのコンソール画面を開き、`Auto Scaling グループの作成`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/24926e9fca1e8cff8d266fdd.png)

起動テンプレートまたは起動設定を選択する のステップで以下を入力し、`次へ`をクリックします。

Auto Scaling グループ名　`autoscaling-handson20211013`　を入力
起動テンプレート　`autoscaling-handson20211013`　を選択

![](https://storage.googleapis.com/zenn-user-upload/6a0f6f9f765541154c8fab17.png)

設定の構成　のステップでは以下を入力し、`次へ`をクリックします。

VPC　`h4b-vpc`　を選択
サブネット　`h4b-subnet1`, `h4b-subnet2`　を選択

![](https://storage.googleapis.com/zenn-user-upload/9d4d15c919b6ef1a8e88f8c5.png)

詳細オプションを設定　のステップでは以下を入力し、`次へ`をクリックします。

ロードバランシング　`既存のロードバランサーにアタッチ`　を選択
既存のロードバランサーにアタッチ　`ロードバランサーのターゲットグループ　から選択`　をクリック

![](https://storage.googleapis.com/zenn-user-upload/a7fde5fcda3f5d629e9d45cf.png)

グループサイズとスケーリングポリシーを設定する　のステップでは以下を入力し、`次へ`をクリックします。

最大キャパシティ　４

![](https://storage.googleapis.com/zenn-user-upload/93ee9054831d15fa7f7585ab.png)

通知を追加　のステップでは何も入力せず、`次へ`をクリックします。

タグを追加　のステップでは何も入力せず、`次へ`をクリックします。

確認のステップで内容を確認した上で、`Auto Scaling グループを作成`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/7271e989126af4770324111d.png)

一覧に作成したAuto Scaling グループが表示されていることを確認します。

![](https://storage.googleapis.com/zenn-user-upload/4e66d7430a2f4514819c7493.png)

# 自動スケーリングの設定

作成されたAuto Scaling グループを選択し、自動スケーリングを選択し、`Create dynamic scaling policy` をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/2c05c8be8a53097a570c1e31.png)

ターゲット値を 80 に変更し、`作成` をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/43db06f77c84a94fd4dd6f1b.png)

# CloudWathアラームの確認

自動スケーリングの設定によってアラームが設定されていることを確認します。
[https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~()](https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~())
よりCloudWatchコンソール画面を開き、`TargetTracking-autoscaling-handson20211013`から始まるアラームが２つ（スケールアウト用、スケールイン用）できていることを確認します。

![](https://storage.googleapis.com/zenn-user-upload/8b589c335294074b1e1c7bc3.png)
