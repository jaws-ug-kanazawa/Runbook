---
title: "環境作成の事前準備"
---

# ハンズオンに必要な環境の作成
- CloudFormationテンプレートのダウンロード
[https://pages.awscloud.com/rs/112-TZM-766/images/h4b_ec2autoscaling_template.zip](https://pages.awscloud.com/rs/112-TZM-766/images/h4b_ec2autoscaling_template.zip)
よりダウンロードしたzipファイルを解凍します。

マネージメントコンソールにアクセス
[https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/create/template](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/create/template)

（ここにハードコピー入る）

テンプレートソースに`テンプレートファイルのアップロード`を選択し、ファイルの選択ボタンより先ほど解凍した`h4b_ec2autoscaling_template.json`を選択し`次へ`をクリックします。
スタックの詳細を指定でスタック名に`autoscaling-handson20211013`を入力し`次へ`をクリックします。
スタックオプションの設定では何も入力せず`次へ`をクリックします。
何も入力せず`スタックの作成`をクリックします。

（ここにハードコピー入る）

ステータスが`CREATE_IN_PROGRESS`から`CREATE_COMPLETE`に変われば完了です。