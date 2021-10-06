---
title: "環境作成の事前準備"
---

# ハンズオンに必要な環境の作成
- CloudFormationテンプレートのダウンロード
[https://pages.awscloud.com/rs/112-TZM-766/images/h4b_ec2autoscaling_template.zip](https://pages.awscloud.com/rs/112-TZM-766/images/h4b_ec2autoscaling_template.zip)
よりダウンロードしたzipファイルを解凍します。

マネージメントコンソールにアクセス
[https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/create/template](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/create/template)

テンプレートソースに`テンプレートファイルのアップロード`を選択し、ファイルの選択ボタンより先ほど解凍した`h4b_ec2autoscaling_template.json`を選択し`次へ`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/cdbd956f71ce54141776a4de.png)

スタックの詳細を指定でスタック名に`autoscaling-handson20211013`を入力し`次へ`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/73d2690bda944cf28a8b7093.png)

スタックオプションの設定では何も入力せず`次へ`をクリックします。
何も入力せず`スタックの作成`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/0e1d774ffa1881e894bf8efa.png)

ステータスが`CREATE_IN_PROGRESS`から`CREATE_COMPLETE`に変われば完了です。

![](https://storage.googleapis.com/zenn-user-upload/85cd9c05db3de142d65617be.png)
![](https://storage.googleapis.com/zenn-user-upload/9c403f58eca5ae1f78b91865.png)
