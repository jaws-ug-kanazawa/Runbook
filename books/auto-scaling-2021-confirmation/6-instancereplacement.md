---
title: "異常なインスタンスの置き換え"
---

# インスタンスを停止する

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013)
よりEC2マネジメントコンソール画面を開き、autoscaling-handson20211013となっているインスタンスを選択し、インスタンスの状態より`インスタンスを停止`をクリックします。

# 新しくインスタンスが起動することを確認する

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013)
にてインスタンスが追加されていることを確認します。
ステータスチェックが2台とも 2/2 のチェックに合格しました となるまで待ちます。

セッション管理やログ管理のようにセッション情報やログをインスタンス内に保持するのではなく、DynamoDB、ElasticCache、CloudWatch Logsなどを活用して、外出しする設計が必要。