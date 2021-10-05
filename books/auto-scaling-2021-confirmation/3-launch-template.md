---
title: "スケジュールスケーリング（１）~起動テンプレートの作成~"
---

# ユーザデータのダウンロード

https://pages.awscloud.com/rs/112-TZM-766/images/h4b-ec2autoscaling-userdata.zip
よりダウンロードしたzipファイルを解凍します。

# 起動テンプレートの作成

https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchTemplates:
よりEC2起動テンプレートのコンソール画面を開き、`起動テンプレートを作成`をクリックします。

以下の内容を設定します。
起動テンプレート名　`autoscaling-handson20211013`　を入力
Amazon マシンイメージ（AMI）　`Amazon Linux 2 AMI (HVM), SSD Volume Type` を選択
インスタンスタイプ　t2.micro を選択
セキュリティグループ　h4b-ec2-sg

リソースタグで`タグを追加`をクリックし、以下の内容を追加します。
キー　`Name`　を入力
値　`autoscaling-handson20211013`　を入力
リソースタイプ　`インスタンス`　を選択

高度な詳細を開き、以下の内容を入力します。
CloudWatchモニタリングの詳細　有効化
ユーザデータ　先程ダウンロードしたzipファイルを解凍して得られる`h4b-ec2autoscaling-userdata.txt`をエディタなどで開いた上で、内容を貼り付け`起動テンプレートの作成`をクリックします。

# オートスケーリンググループの作成

https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/
よりAuto Scaling グループのコンソール画面を開き、`Auto Scaling グループの作成`をクリックします。

起動テンプレートまたは起動設定を選択する のステップで以下を入力し、`次へ`をクリックします。

Auto Scaling グループ名　`autoscaling-handson20211013`　を入力
起動テンプレート　`autoscaling-handson20211013`　を選択

設定の構成　のステップでは以下を入力し、`次へ`をクリックします。

VPC　`h4b-vpc`　を選択
サブネット　`h4b-subnet1`, `h4b-subnet2`　を選択

詳細オプションを設定　のステップでは以下を入力し、`次へ`をクリックします。

ロードバランシング　`既存のロードバランサーにアタッチ`　を選択
既存のロードバランサーにアタッチ　`ロードバランサーのターゲットグループ　から選択`　をクリック

グループサイズとスケーリングポリシーを設定する　のステップでは以下を入力し、`次へ`をクリックします。

最大キャパシティ　４

通知を追加　のステップでは何も入力せず、`次へ`をクリックします。

タグを追加　のステップでは何も入力せず、`次へ`をクリックします。

確認のステップで内容を確認した上で、`Auto Scaling グループを作成`をクリックします。

一覧に作成したAuto Scaling グループが表示されていることを確認します。