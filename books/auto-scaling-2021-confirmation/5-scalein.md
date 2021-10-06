---
title: "スケジュールスケーリング（３）~負荷をとめてスケールインを確認~"
---

# 負荷を止める

先程の手順で表示済みのコンソールを開き、Crtl+Cでコマンドを止めます

![](https://storage.googleapis.com/zenn-user-upload/38a340584a5ff7c93a682c7c.png)

# CloudWatchアラーム

[https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~()](https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~())
からTargetTracking-autoscaling-handson20211013-AlarmLow から始まるものを選択します。

CPU使用率が50%を下回ってことを確認します。

![](https://storage.googleapis.com/zenn-user-upload/778fd7c08d784e0b1bdaf2bb.png)

15分間経過するとアラーム状態となり、スケールインが開始されます。

![](https://storage.googleapis.com/zenn-user-upload/48bc86517180c358c4997a6d.png)

# スケールインしていることの確認

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013)
にてインスタンスが1台に減っているを確認します。

# アクティビティ履歴を確認する

[https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/details/autoscaling-handson20211013?view=activity](https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/details/autoscaling-handson20211013?view=activity)
よりどのようにインスタンス数が変化しているかを確認することができます。

![](https://storage.googleapis.com/zenn-user-upload/d1177597f591a1f54efc4805.png)

:::message
スケールインすることでセッション情報が失われてログイン画面に戻ってしまう障害が発生したり、ログが消失することになるため、セッション管理やログ管理のようにセッション情報やログをインスタンス内に保持するのではなく、DynamoDB、ElasticCache、CloudWatch Logsなどを活用して、外出しする設計が必要となります。
:::