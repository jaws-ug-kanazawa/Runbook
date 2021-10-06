---
title: "スケジュールスケーリング（２）~負荷をかけてスケールアウトを確認~"
---

# 負荷をかけるコマンド

[https://pages.awscloud.com/rs/112-TZM-766/images/h4b-ec2autoscaling-command.txt](https://pages.awscloud.com/rs/112-TZM-766/images/h4b-ec2autoscaling-command.txt)
よりダウンロードします。

# EC2への接続

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:search=autoscaling-handson20211013)
よりEC2マネジメントコンソール画面を開き、autoscaling-handson20211013となっているインスタンスを選択し、アクションより`接続`をクリックします。

EC2 Instance Connectのタブにて`接続`をクリックします。

コンソール画面が表示されるので、先程ダウンロードしたコマンドを入力し、画面のようになることを確認します。

# CloudWatchアラーム

[https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~()](https://ap-northeast-1.console.aws.amazon.com/cloudwatch/home?region=ap-northeast-1#alarmsV2:?~())
からTargetTracking-autoscaling-handson20211013-AlarmHigh から始まるものを選択します。

CPU使用率が80%を超えていることを確認します。
3分間経過するとアラーム状態となり、スケールアウトが開始されます。

# スケールアウトしていることの確認

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013)
にてインスタンスが1台から2台に増えていることを確認します。
ステータスチェックが2台とも 2/2 のチェックに合格しました となるまで待ちます。
