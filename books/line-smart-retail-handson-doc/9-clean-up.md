---
title: "クリーンアップ"
---

# 概要
AWSの課金発生を止めるため、ハンズオンで作成したAWSのリソースを削除していきます。

# S3バケットの削除
下記のURLからS3のコンソール画面を開き、aws-sam-cli-managed-default-samclisourcebucket から始まるバケットを選択し、`空にする`ボタンを押してください。
[https://console.aws.amazon.com/s3/home?region=ap-northeast-1](https://console.aws.amazon.com/s3/home?region=ap-northeast-1)

# CloudFormation削除
下記のURLからCloudFormationのコンソール画面を開き、ハンズオンで作った３つのスタックを削除してください。
[https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=20211002&viewNested=true&hideStacks=false&stackId=](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=20211002&viewNested=true&hideStacks=false&stackId=)
![](https://storage.googleapis.com/zenn-user-upload/563a98ae270fe4fab9b7dbd0.png)

次に下記のURLからaws-sam-cli-managed-defaultのスタックも削除してください。
[https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=aws-sam&viewNested=true&hideStacks=false&stackId=](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks?filteringStatus=active&filteringText=aws-sam&viewNested=true&hideStacks=false&stackId=)

# Amplifyの削除
下記のURLからAmplifyのコンソール画面を開き、ハンズオンで作ったものを選択してください。
[https://ap-northeast-1.console.aws.amazon.com/amplify/home?region=ap-northeast-1](https://ap-northeast-1.console.aws.amazon.com/amplify/home?region=ap-northeast-1)

アクションからアプリの削除を選択してください。
![](https://storage.googleapis.com/zenn-user-upload/7a3fa8da800d5c732adaab7b.png)

deleteと入力して`Delete`ボタンを押してください。
![](https://storage.googleapis.com/zenn-user-upload/a3832d5a36f65c43e508e2cf.png)

# CodeCommitの削除
下記のURLからCodeCommitのコンソール画面を開き、ハンズオンで作ったものを選択してください。
[https://ap-northeast-1.console.aws.amazon.com/codesuite/codecommit/repositories?region=ap-northeast-1](https://ap-northeast-1.console.aws.amazon.com/codesuite/codecommit/repositories?region=ap-northeast-1)
![](https://storage.googleapis.com/zenn-user-upload/013880778ccfb95373f1aa21.png)

deleteと入力して`削除`ボタンを押してください。
![](https://storage.googleapis.com/zenn-user-upload/77d41055252e31a1a595f3a4.png)

# Cloud9削除
下記のURLからCloud9のコンソール画面を開き、ハンズオンで作ったCloud9の環境を削除してください。
[https://ap-northeast-1.console.aws.amazon.com/cloud9/home?region=ap-northeast-1#](https://ap-northeast-1.console.aws.amazon.com/cloud9/home?region=ap-northeast-1#)
![](https://storage.googleapis.com/zenn-user-upload/f6wgjh7jaeptqwq2hna2kxpyg0lr)

