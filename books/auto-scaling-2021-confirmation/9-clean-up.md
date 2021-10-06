---
title: "クリーンアップ"
---

# 概要
AWSの課金発生を止めるため、ハンズオンで作成したAWSのリソースを削除していきます。

# オートスケーリンググループの削除

[https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/details?id=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/details?id=autoscaling-handson20211013)

autoscaling-handson20211013を選択し、`削除`をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/974ddb5820d3611f698b63a7.png)

![](https://storage.googleapis.com/zenn-user-upload/9f1c9fe4056630f392a25a57.png)

# 起動テンプレートの削除

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchTemplates:search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchTemplates:search=autoscaling-handson20211013)

起動テンプレート名がautoscaling-handson20211013となっているものを選択し、アクションより`テンプレートを削除`をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/08a155a8134cebff17cd8d66.png)

![](https://storage.googleapis.com/zenn-user-upload/11d73b30c124a71d5b2dc518.png)

# CloudFormation削除
下記のURLからCloudFormationのコンソール画面を開き、ハンズオンで作ったスタックを削除します。
[https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=autoscaling-handson20211013&viewNested=true&hideStacks=false&stackId=](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=autoscaling-handson20211013&viewNested=true&hideStacks=false&stackId=)

![](https://storage.googleapis.com/zenn-user-upload/c4ec69a37e3f379560f8b0a7.png)

![](https://storage.googleapis.com/zenn-user-upload/e01a3ce8594fee58e603bb01.png)
