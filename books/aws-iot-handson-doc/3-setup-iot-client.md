---
title: "AWS IoT クライアントの設定"
---

# AWS IoT のセットアップ

AWS IoTのトップ画面へアクセスします
https://ap-northeast-1.console.aws.amazon.com/iot/home?region=ap-northeast-1#/home

画面左下の`設定`を押します
![](https://storage.googleapis.com/zenn-user-upload/207174375184-20220611.png)

`エンドポイント`をコピーしておき、テキストファイルなどにペーストしておきます。IoTクライアントが通信を行う先のURIです。
![](https://storage.googleapis.com/zenn-user-upload/a054f2a943f4-20220611.png)

`管理`→`セキュリティ`→`ポリシー`を選び、`ポリシーの作成`をクリックします。
![](https://storage.googleapis.com/zenn-user-upload/4f36cd42b888-20220611.png)

適当な名前を付け、JSONを選びます。ここで作成したポリシーは、AWS IoT Coreと通信を行うクライアントが持つべきセキュリティポリシー（AWS IoT Coreの複数の機能と連携できる・できない等）になります。
![](https://storage.googleapis.com/zenn-user-upload/c8bd67a84368-20220611.png)

以下の通りポリシードキュメントを入力し、`作成`を押します。このハンズオンではAWS IoTのすべての機能を使えるポリシーを作成します。（AWSのその他リソースを操作できる権限ではないことに注意してください）

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "iot:*",
      "Resource": "*"
    }
  ]
}
```

![](https://storage.googleapis.com/zenn-user-upload/3fb51aebc254-20220611.png)
ポリシーが作成されました。

`管理`→`すべてのディバイス`→`モノ`を選んでください。モノ、はAWS IoTが管理するIoTクライアント（デバイス）になります。このハンズオンではダミークライアントとしてCloud9を使います。商用環境では大量の登録が発生するため、CLI等プログラム化しておくことをお勧めしています。
![](https://storage.googleapis.com/zenn-user-upload/79f84ce5dbd8-20220611.png)

`単一のモノを作成する`を選び`次へ`ボタンを押してください。
![](https://storage.googleapis.com/zenn-user-upload/d6977af02cde-20220611.png)

適当な名前を入力し、その他の設定は行わず、画面下の`次へ`を押します
![](https://storage.googleapis.com/zenn-user-upload/eb89cfd88e78-20220611.png)

`新しい証明書を自動生成（推奨）`を選択し、画面下の`次へ`を押します
AWS IoT Coreは通信及びデバイスのセキュリティ管理、制御に電子証明書を用いるため、認証局の機能を内蔵しています。ここで発行された認証局をクライアント（Cloud9）に組み込むことによって通信が可能となります。
![](https://storage.googleapis.com/zenn-user-upload/5b3c2fa9f7fc-20220611.png)

`ポリシーのアタッチ`を押します。ポリシーは先ほど作成したデバイスが操作可能なAWS IoTの権限が設定されたものです。AWS IoT Coreはデバイスの制御に証明書を使いますので、ポリシーを証明書に結び付けることになります。
![](https://storage.googleapis.com/zenn-user-upload/b18acc8074d2-20220611.png)

ディバイス証明書、キーファイルをダウンロードして`完了`のボタンを押します。
![](https://storage.googleapis.com/zenn-user-upload/5e1da3e10096-20220611.png)

# IoT クライアントのセットアップ

作成したCloud9でターミナルの画面にいきます。

以下のコマンドを実行します。
```
sudo ln -s /usr/bin/pip-3.6 /usr/bin/pip3
```
`ln: failed to create symbolic link '/usr/bin/pip3': File exists`
が表示された場合、すでにPython3.6がインストール済みですので、先に作業を進めてください。(IoT用SDKはPython3が動作に必要です)

以下のコマンドを実行します。
```
pip3 -V
```
`pip 9.0.1 from /usr/lib/python3/dist-packages (python 3.6)`の表示がされたらインストール完了です

Python SDKをインストールします。以下のコマンドを実行します。
```
sudo pip3 install AWSIoTPythonSDK
```

ダミークライアントのソースコードをダウンロードします。
```
wget http://bit.ly/2QggRgx -O dummyclient.tar.gz
```

ダウンロードしたクライアントを解凍します。
```
tar -zxvf dummyclient.tar.gz
```

今の解凍で新しいフォルダができていますので、`DummyDevice`→`certs`を選んで開きます。
![](https://storage.googleapis.com/zenn-user-upload/764fcf080570-20220611.png)

`File`→`Upload Local Files`を開きます。
![](https://storage.googleapis.com/zenn-user-upload/5ec4ba80b1d1-20220611.png)

先ほどDLした2つの電子証明書ファイル`**-certificate.pem.crt `、`**-private.pem.key`をUploadし、ファイルがコピーされたことを確認します。
注意：Windows環境であれば、*.crtファイルは証明書を表すアイコンマークとなり、拡張子が表示されず*.pemファイルとなっています。
![](https://storage.googleapis.com/zenn-user-upload/dca08d33cce9-20220611.png)

- `**-private.pem.key` のファイル名を private.pemに変更します。Cloud9のシェルで変更してもいいですし、エクスプローラーでrenameを選んでもいいです。

- ディレクトリをシェル上で移動します。移動先は`DummyDevice`です。TABを使うことができますので、たとえば cd D だけ入力してTABを押すと残りは自動で補完されます。

```
cd DummyDevice/
```
 
- 以下のコマンドを入力します。{ご自分の作ったモノ名}{AWS IoTのendpoint_url}は置き換えてください。
```
python3 deviceMain.py --device_name {ご自分の作ったモノ名} --endpoint {AWS IoTのendpoint_url}
```

- 疎通が完了すると以下のような画面が表示されます。
```
$ python3 deviceMain.py --device_name 20220619things --endpoint a26x565ji2jizr-ats.iot.us-east-1.amazonaws.com
start >>>
device_name: 20220619things
endpoint: a26x565ji2jizr-ats.iot.us-east-1.amazonaws.com
rootca cert: ./certs/root.pem
private key: ./certs/private.pem
certificate: ./certs/80e93965a885b5cddd590581484a6629f588ed7119904e4f203a41bf6f9e25c3-certificate.pem.crt
connect to AWS IoT >>>
topic: data/20220619things
send back state payload:{"state": {"reported": {"wait_time": 5}}}
```

AWS IoT の管理画面で `テスト`→`MQTT テストクライアント` を選びます。

`トピックのフィルター`の欄に data/{モノの名前}を入力し`サブスクライブ`ボタンを押します。{モノの名前}は皆さんが作成した名前です。

ダミークライアントの設定が5秒間隔でのステータス同期となっているので、5秒ごとにデータが1個づつ増えていきます。
 
# デバイスシャドウによるデバイスの操作

AWS IoTにはデバイスシャドウという機能があります。クライアントデバイスが送ってきたステータスを、管理者側が書き換えることでクライアントデバイスの挙動を変更させることができます。上記でテストした5秒おきに送られてくるデータを10秒おきに送られてくるように変更します。

データ間隔が5秒おきになっていることを確認します。
 
`管理`→`すべてのディバイス`→`モノ`を選び、作成したモノを選択します。
 
`Device Shadow`タブを選択し、`Classic Shadow` を選択します。
 ![](https://storage.googleapis.com/zenn-user-upload/ee39b3384ec5-20220611.png)

データが5秒間隔で上がってくることが定義されています。これを10秒に書き換えるため`編集`を押します。
![](https://storage.googleapis.com/zenn-user-upload/e7ef8431a5b2-20220611.png)

こちらの値が空欄の場合、Cloud9上のDummy Clientを一度停止して、再度起動し5秒待ってください。

以下のように置換し`保存`を押します。
 
```
{
  "state": {
    "desired": {
      "wait_time": 10
    },
    "reported": {
      "wait_time": 5
    }
  }
}
```
![](https://storage.googleapis.com/zenn-user-upload/29913b1d336c-20220611.png)

Cloud9の画面に戻ると、指示を受信した旨が表示されています。
![](https://storage.googleapis.com/zenn-user-upload/effdd17a8f93-20220611.png)

AWS IoT Coreのテスト画面で、同期間隔が10秒になっていることを確認します。
![](https://storage.googleapis.com/zenn-user-upload/4fd37ccd2596-20220611.png)

# S3バケットの作成

https://s3.console.aws.amazon.com/ にアクセスし、`バケットを作成`を押します。
![](https://storage.googleapis.com/zenn-user-upload/19e2b0098d86-20220611.png)

適当なバケット名を入力します。
![](https://storage.googleapis.com/zenn-user-upload/8d8b0e229dba-20220611.png)

すべてデフォルトのまま`バケットの作成`を押します。
![](https://storage.googleapis.com/zenn-user-upload/03f3232ba140-20220611.png)

# ルールエンジンの作成

AWS IoT Coreにはルールエンジンという機能が存在しています。クライアントデバイスから上がってきたデータの中身をもとに、SQLを実行し、データの中身によりその後のAWS上の挙動を変更させます。このハンズオンでは、データが[s3]という文字列であった場合のみ、s3にデータを保存する手順を行います。

`管理`→`メッセージのルーティング`→`ルール` を選択し、`ルールの作成`を押します。
![](https://storage.googleapis.com/zenn-user-upload/188818b8e1fb-20220611.png)

適当な名前を入力し、`次へ`を押します。
![](https://storage.googleapis.com/zenn-user-upload/d7477f851d92-20220611.png)

以下のSQLを入力して、`次へ`を押します。
```
select name from 'data/{モノの名前}' where name = 's3'
```
![](https://storage.googleapis.com/zenn-user-upload/4a3eea8b9024-20220611.png)

ルールアクションより`S3バケット`を選択し`S3を参照`をクリックします。
 ![](https://storage.googleapis.com/zenn-user-upload/8a76f7a52182-20220611.png)

作成したバケットを選択します。
 ![](https://storage.googleapis.com/zenn-user-upload/ccb21bc78c65-20220611.png)

キーに「test」と入力し、`新しいロールの作成`を押します。
![](https://storage.googleapis.com/zenn-user-upload/f0ee9c5cd516-20220611.png)

適当な名前を付けて`作成`を押します。
![](https://storage.googleapis.com/zenn-user-upload/475b1c7097fd-20220611.png)

`次へ`ボタンを押します。
 ![](https://storage.googleapis.com/zenn-user-upload/035a8460749f-20220611.png)
 
`作成`を押します。
 ![](https://storage.googleapis.com/zenn-user-upload/eb56231a07d9-20220611.png)

ルールが作成されています。これで「s3」というデータを含んだ通信が来た際に、S3上にファイルが作成されるようになります。
 
テキストファイルを開いて以下のコマンドを入力します。（AWS IoTのデータはJSON形式です。）（シェルでの作業に慣れている方は、Cloud9上でそのままファイルを作成しても問題ありません。）
```
{ "name": "s3" }
```
入力後、ファイル名を`payload.json`で保存します。
![](https://storage.googleapis.com/zenn-user-upload/2f5e3cfed73d-20220611.png)

保存したファイルをCloud9上の`DummyDevice` フォルダにアップロードします。
 
シェルで ctr + cを押して、先ほどの通信を止めます。
以下のコマンドを入力します。
```
curl -D - --tlsv1.2 -X POST --cert ./certs/{証明書ファイル名} --key ./certs/private.pem --cacert ./certs/root.pem https://{エンドポイント}:8443/topics/data/{モノの名前}?qos=0 -d @payload.json
```
動作すると以下の表示になります。
```
HTTP/1.1 200 OK
content-type: application/json
content-length: 65
date: Sat, 11 Jun 2022 12:37:12 GMT
x-amzn-RequestId: 602536fa-5868-07ee-d9bd-78f66063db45
connection: keep-alive

{"message":"OK","traceId":"602536fa-5868-07ee-d9bd-78f66063db45"}
```

テスト画面で受信したデータの確認が可能です。[s3]と表示されていれば成功です。この画面を閉じてしまっており、新しく設定する場合、メッエージが表示されていないはずなので、もう一度curlのコマンドを実行してください。
![](https://storage.googleapis.com/zenn-user-upload/0f6f68fd007e-20220611.png)

作成したs3バケットを見てみましょう。データが保存されています。
![](https://storage.googleapis.com/zenn-user-upload/8a7e18b4300a-20220611.png)

データを送るたびに最終更新日時が上書きされています。この手順ではデータが単一ファイルを上書きしていきますが、Timestampをベースとして都度都度ファイル名を変更させることができます。また、payload.jsonの中身を書き換えて、s3が含まれていない通信は、s3のファイル更新日が上書きされないことを確認しましょう。
