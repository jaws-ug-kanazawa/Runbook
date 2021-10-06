---
title: "異常なインスタンスの置き換え"
---

# インスタンスを停止する

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013)
よりEC2マネジメントコンソール画面を開き、autoscaling-handson20211013となっているインスタンスを選択し、インスタンスの状態より`インスタンスを停止`をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/c34a105ad64abac778df98b9.png)
![](https://storage.googleapis.com/zenn-user-upload/cfea30d9797b84a50bc5648a.png)
![](https://storage.googleapis.com/zenn-user-upload/11228375bd9a7e10533035f3.png)

# 新しくインスタンスが起動することを確認する

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#Instances:instanceState=running;search=autoscaling-handson20211013)
にてインスタンスが追加されていることを確認します。

![](https://storage.googleapis.com/zenn-user-upload/78be8a27f5122d02673057a0.png)
ステータスチェックが2台とも 2/2 のチェックに合格しました となるまで待ちます。
