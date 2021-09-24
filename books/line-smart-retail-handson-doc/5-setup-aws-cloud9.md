---
title: "AWSの開発環境作成・準備（Cloud9）"
---

# 概要
本日のハンズオンではCloud9の環境を、開発作業の場所として使用します。 Cloud9は、コードの記述・実行・デバッグが行えるクラウドベースの統合開発環境（IDE）です。 

# Cloud9
- Cloud9のコンソール画面にアクセス
下記のURLからCloud9のコンソール画面を開き、
https://ap-northeast-1.console.aws.amazon.com/cloud9/home?region=ap-northeast-1
![](https://storage.googleapis.com/zenn-user-upload/izcu5i5dd1s10ibjr99q1b7tb79q)
[Name] 欄に任意の名前を入力してください。
![](https://storage.googleapis.com/zenn-user-upload/e0uigt6pwmrszw9gh9jkrle48pnc)
Instance typeはt3.smallを選択してください。（あとは基本的にデフォルトのままで構いません）
![](https://storage.googleapis.com/zenn-user-upload/q58c5pnl0ccdv3yv0kn8jdng50n3)
VPCは特別な理由が無ければdefaultのものを選択して、`Next step`ボタンを押してください。
![](https://storage.googleapis.com/zenn-user-upload/6cv3qvohhfu9i7zqqzn73mcg5pz5)
:::message alert
defaultのVPCが無い場合は下記の方法でdefaultのVPCを作成してください。
:::
:::details defaultのVPC作成方法
![](https://storage.googleapis.com/zenn-user-upload/85uj5lrqrhip1py18u302a3au71o)
![](https://storage.googleapis.com/zenn-user-upload/kxfm5zg9xamo23esgnomgojz8bct)
:::
最後に`Create environment`ボタンを押してください。しばらくするとCloud9の画面が表示されます。
![](https://storage.googleapis.com/zenn-user-upload/yknfd95ibciruzjffklblcm315lg)

# ハンズオン用のコードの取得

Cloud9のターミナル領域で下記のgit cloneコマンドを実行しハンズオン用のコードを取得してください。
```shell
cd ~/environment
git clone https://github.com/tacck/line-api-use-case-smart-retail.git
```
![](https://storage.googleapis.com/zenn-user-upload/cfa5e1c9e75df155bde412d8.png)

# ディスク容量の拡張

Cloud9の初期EBSサイズは10GiBです。SAMを利用する際に10GBを超える容量のサイズが必要となるため、以下の方法にてEBSボリュームサイズを20GBに変更してください。
:::message
下記のコマンドをコピペして実行しましょう！
:::
```
cd ~/environment/line-api-use-case-smart-retail/tools/
chmod +x resize.sh
./resize.sh 20
```

df -Hのコマンドを実行し、/dev/xvda1が20GiB(22GB)になっていることを確認してください。
:::message
下記のコマンドをコピペして実行しましょう！
:::
```
df -H
```
```
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        1.1G     0  1.1G   0% /dev
tmpfs           1.1G     0  1.1G   0% /dev/shm
tmpfs           1.1G  463k  1.1G   1% /run
tmpfs           1.1G     0  1.1G   0% /sys/fs/cgroup
/dev/nvme0n1p1   22G  8.9G   13G  42% /
tmpfs           205M     0  205M   0% /run/user/1000
```

----
参考）
- https://docs.aws.amazon.com/cloud9/latest/user-guide/move-environment.html