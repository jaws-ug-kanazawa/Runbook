---
title: "IoTダミークライアント(Cloud9)の作成"
---

AWS IoT Coreと通信（MQTT及びHTTP）を行うIoTクライアントを構築します。このハンズオンでは、デバイスを用いず、AWS Cloud9にAWS IoT SDKをインストールします。

# Cloud9環境の作成
- AWS Cloud9のコンソール画面にアクセスします。（ブラウザの別タブで開くことをお勧めします）
下記のURLからCloud9のコンソール画面を開き、
https://ap-northeast-1.console.aws.amazon.com/cloud9/home?region=ap-northeast-1
![](https://storage.googleapis.com/zenn-user-upload/izcu5i5dd1s10ibjr99q1b7tb79q)
[Name] 欄に任意の名前を入力して、`Next step`を押します。
![](https://storage.googleapis.com/zenn-user-upload/e0uigt6pwmrszw9gh9jkrle48pnc)
Instance typeはt2.micro、OSはAmazon LinuxでなくUbuntuを選択してください。（あとは基本的にデフォルトのままで構いません）
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

