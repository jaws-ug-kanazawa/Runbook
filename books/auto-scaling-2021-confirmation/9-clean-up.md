---
title: "クリーンアップ"
---

# 概要
AWSの課金発生を止めるため、ハンズオンで作成したAWSのリソースを削除していきます。

# オートスケーリンググループの削除

[https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/details?id=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2autoscaling/home?region=ap-northeast-1#/details?id=autoscaling-handson20211013)

autoscaling-handson20211013を選択し、`削除`をクリックします。

# 起動テンプレートの削除

[https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchTemplates:search=autoscaling-handson20211013](https://ap-northeast-1.console.aws.amazon.com/ec2/v2/home?region=ap-northeast-1#LaunchTemplates:search=autoscaling-handson20211013)

起動テンプレート名がautoscaling-handson20211013となっているものを選択し、アクションより`テンプレートを削除`をクリックします。

# CloudFormation削除
下記のURLからCloudFormationのコンソール画面を開き、ハンズオンで作ったスタックを削除します。
[https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=autoscaling-handson20211013&viewNested=true&hideStacks=false&stackId=](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=autoscaling-handson20211013&viewNested=true&hideStacks=false&stackId=)