---
title: "スケジュールスケーリング（２）~負荷をかけてスケールアウトを確認~"
---

# 負荷をかけるコマンド

[https://pages.awscloud.com/rs/112-TZM-766/images/h4b-ec2autoscaling-command.txt](https://pages.awscloud.com/rs/112-TZM-766/images/h4b-ec2autoscaling-command.txt)
よりダウンロードします。

# EC2への接続

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:search=autoscaling-handson20211013)
よりEC2マネジメントコンソール画面を開き、autoscaling-handson20211013となっているインスタンスを選択し、アクションより`接続`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/7ff3e1a487c022d10ececd60.png)

EC2 Instance Connectのタブにて`接続`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/4d7673feda3c2bbd5f10bfb4.png)

コンソール画面が表示されるので、先程ダウンロードしたコマンドを入力し、画面のようになることを確認します。

![](https://storage.googleapis.com/zenn-user-upload/9fef00838ea69a21947dc838.png)

# CloudWatchアラーム

[https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~()](https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~())
からTargetTracking-autoscaling-handson20211013-AlarmHigh から始まるものを選択します。

CPU使用率が80%を超えていることを確認します。

![](https://storage.googleapis.com/zenn-user-upload/13cd559955dd2fdbf5d521c0.png)

3分間経過するとアラーム状態となり、スケールアウトが開始されます。

![](https://storage.googleapis.com/zenn-user-upload/abed566298a8d52cd923a337.png)

# スケールアウトしていることの確認

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013)
にてインスタンスが1台から2台に増えていることを確認します。

![](https://storage.googleapis.com/zenn-user-upload/e5394fdbc556bf732261600e.png)

ステータスチェックが2台とも 2/2 のチェックに合格しました となるまで待ちます。
