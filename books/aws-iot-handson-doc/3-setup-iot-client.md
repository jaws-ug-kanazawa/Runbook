---
title: "AWS IoT クライアントの設定"
---

# 
- AWS IoTのトップ画面へアクセスします
IoT Core
https://ap-northeast-1.console.aws.amazon.com/iot/home?region=ap-northeast-1#/home

- 画面左下の【設定】を押します

- 【エンドポイント】をコピーしておき、テキストファイルなどにペーストしておきます。IoTクライアントが通信を行う先のURIです。はじめて利用する場合、右上のボタンを操作し、【有効】と表示されるように設定してください。
```
→有効という表示はない
```
- 【安全性】→　【Policy】を選びます。

- 【ポリシーの作成】をクリックします。

- 適当な名前を付けます。ここで作成したポリシーは、AWS IoT Coreと通信を行うクライアントが持つべきセキュリティポリシー（AWS IoT Coreの複数の機能と連携できる・できない等）になります。

- 以下の表示と同じ値を入力し、【作成】を押します。このハンズオンではAWS IoTのすべての機能を使えるポリシーを作成します。（AWSのその他リソースを操作できる権限ではないことに注意してください）【iot:*】【*】

- ポリシーが作成されました。

- 【管理】→【モノ】を選んでください。モノ、はAWS IoTが管理するIoTクライアント（デバイス）になります。このハンズオンではダミークライアントとしてCloud9を使います。商用環境では大量の登録が発生するため、CLI等プログラム化しておくことをお勧めしています。

- 【モノの登録】を押します。

- 【単一のモノを作成する】を選びます。

- 適当な名前を入力します。

- その他の設定は行わず、画面下の【次へ】を押します

- 【証明書の作成】を押します
AWS IoT Coreは通信及びデバイスのセキュリティ管理、制御に電子証明書を用いるため、認証局の機能を内蔵しています。ここで発行された認証局をクライアント（Cloud9）に組み込むことによって通信が可能となります。

- すべてをDLして【有効化】のボタンを押します。

- 【ポリシーのアタッチ】を押します。ポリシーは先ほど作成したデバイスが操作可能なAWS IoTの権限が設定されたものです。AWS IoT Coreはデバイスの制御に証明書を使いますので、ポリシーを証明書に結び付けることになります。

- 先ほど作成したポリシーを選び【モノの登録】を押します。モノが作成されました。

- 作成したCloud9でターミナルの画面にいきます。

- 以下のコマンドを実行
```
sudo ln -s /usr/bin/pip-3.6 /usr/bin/pip3
```
ln: failed to create symbolic link '/usr/bin/pip3': File exists
が表示された場合、すでにPython3.6がインストール済みですので、先に作業を進めてください。＃IoT用SDKはPython3が動作に必要です。

- pip3 –V を実行し、以下の表示がされたらインストール完了です。

- Python SDKをインストールします。以下のコマンドを実行します。
```
sudo pip3 install AWSIoTPythonSDK
```

- ダミークライアントのソースコードをダウンロードします。
```
wget http://bit.ly/2QggRgx -O dummyclient.tar.gz
```

- ダウンロードしたクライアントを解凍します。
```
tar -zxvf dummyclient.tar.gz
```

- 今の解凍で新しいフォルダができていますので、【DummyDevice】【certs】を選んで開きます。

- 【File】【Upload Local Files】を開きます。

- 先ほどDLした2つの電子証明書ファイル【**-certificate.pem.crt 】【**-private.pem.key】をUploadします。
注意：Windows環境であれば、*.crtファイルは証明書を表すアイコンマークとなり、拡張子が表示されず*.pemファイルとなっています。

- ファイルがコピーされたことを確認します。

- private.pem.key のファイル名を private.pemに変更します。Cloud9のシェルで変更してもいいですし、エクスプローラーでrenameを選んでもいいです。

- ディレクトリをシェル上で移動します。移動先は【DummyDevice】です。TABを使うことができますので、たとえば cd D だけ入力してTABを押すと残りは自動で補完されます。
 
- 以下のコマンドを入力します。赤字は置き換えてください。
```
python3 deviceMain.py --device_name ご自分の作ったモノ名 --endpoint AWS IoTのendpoint_url

python3 deviceMain.py --device_name 20220505things --endpoint a26x565ji2jizr-ats.iot.ap-northeast-1.amazonaws.com
start >>>
device_name: 20220505things
endpoint: a26x565ji2jizr-ats.iot.ap-northeast-1.amazonaws.com
rootca cert: ./certs/root.pem
private key: ./certs/private.pem
certificate: ./certs/60adfabe8d-certificate.pem.crt
connect to AWS IoT >>>
Connect timed out
class shadow Error
Error main()
Traceback (most recent call last):
  File "deviceMain.py", line 48, in device_main
    iot_client.create_shadow()
  File "/home/ubuntu/environment/DummyDevice/iotCommon.py", line 136, in create_shadow
    raise e
  File "/home/ubuntu/environment/DummyDevice/iotCommon.py", line 122, in create_shadow
    self._shadow_client.connect(self.KEEPALIVE)
  File "/usr/local/lib/python3.6/dist-packages/AWSIoTPythonSDK/MQTTLib.py", line 1278, in connect
    return self._AWSIoTMQTTClient.connect(keepAliveIntervalSecond)
  File "/usr/local/lib/python3.6/dist-packages/AWSIoTPythonSDK/MQTTLib.py", line 520, in connect
    return self._mqtt_core.connect(keepAliveIntervalSecond)
  File "/usr/local/lib/python3.6/dist-packages/AWSIoTPythonSDK/core/protocol/mqtt_core.py", line 199, in connect
    raise connectTimeoutException()
AWSIoTPythonSDK.exception.AWSIoTExceptions.connectTimeoutException
```

- 疎通が完了すると以下のような画面が表示されます。

- AWS IoT の管理画面でテストを選びます。

- 【トピックのサブスクリプション】の欄に data/{モノの名前}を入力し【サブスクライブ】ボタンを押します。{モノの名前}は皆さんが作成した名前です。

- ダミークライアントの設定が5秒間隔でのステータス同期となっているので、5秒ごとにデータが1個づつ増えていきます。
 
# デバイスシャドウによるデバイスの操作

AWS IoTにはデバイスシャドウという機能があります。クライアントデバイスが送ってきたステータスを、管理者側が書き換えることでクライアントデバイスの挙動を変更させることができます。上記でテストした5秒おきに送られてくるデータを10秒おきに送られてくるように変更します。
- データ間隔が5秒おきになっていることを確認します。
 
- 【管理】【モノ】を選びます。
 
- 【シャドウ】を選択します。
 
- データが5秒間隔で上がってくることが定義されています。これを10秒に書き換えるため【編集】を押します。
 
こちらの値が空欄の場合、Cloud9上のDummy Clientを一度停止して、再度起動し5秒待ってください。

- 以下のように置換し【保存】を押します。
 
- Cloud9の画面に戻ると、指示を受信した旨が表示されています。
 
- AWS IoT Coreのテスト画面で、同期間隔が10秒になっていることを確認します。
 

# ルールエンジン
AWS IoT Coreにはルールエンジンという機能が存在しています。クライアントデバイスから上がってきたデータの中身をもとに、SQLを実行し、データの中身によりその後のAWS上の挙動を変更させます。このハンズオンでは、データが[s3]という文字列であった場合のみ、s3にデータを保存する手順を行います。

- 【ACT】を押します。
 
- 【ルールの作成】を押します。
 
- 適当な名前を入力します。
 
- 以下のSQLを入力します。
```
select name from 'data/{モノの名前}' where name = 's3'
```

- 【アクションの追加】を押します。

- 複数のAWSリソースとの連携が用意されています。S3を選びます。
 
- 【アクションの設定】を押します。
 
- 【新しいリソースを作成する】を押します。
 
- 【バケットを作成する】を押します。
 
- 適当なバケット名を入力し、すべてデフォルトのまま【次へ】を3回押し【バケットの作成】を押します。
- IoTの画面に戻り、ぐるぐるしたマークをおすと、先ほど作成したバケットが表示されますので、選択します。
 
- キーに「test」と入力します。
 
- 【ロールの作成】を押します。
 
- 適当な名前を付けて【ロールの作成】を押します。
 
- 【アクションの追加】ボタンを押します。
 
S3への書き込み設定が完了しました。
 
- 【ルールの作成】を押します。
 
ルールが作成されています。これで「s3」というデータを含んだ通信が来た際に、S3上にファイルが作成されるようになります。
 
- テキストファイルを開いて以下のコマンドを入力します。（AWS IoTのデータはJSON形式です。）（シェルでの作業に慣れている方は、Cloud9上でそのままファイルを作成しても問題ありません。）
```
{ "name": "s3" }
```
入力後、ファイル名を【payload.json】で保存します。

- 保存したファイルをCloud9上の【DummyDevice】 フォルダにアップロードします。
 
- シェルで ctr + cを押して、先ほどの通信を止めます。
- 以下のコマンドを入力します。
```
curl -D -   --tlsv1.2   -X POST   --cert ./certs/{証明書ファイル名}   --key ./certs/private.pem   --cacert ./certs/root.pem   https://{エンドポイント}:8443/topics/data/{モノの名前}?qos=0   -d @payload.json
```
動作すると以下の表示になります。
 
- テスト画面で受信したデータの確認が可能です。[s3]と表示されていれば成功です。この画面を閉じてしまっており、新しく設定する場合、メッエージが表示されていないはずなので、もう一度curlのコマンドを実行してください。
 
- 作成したs3バケットを見てみましょう。データが保存されています。
 
データを送るたびに最終更新日時が上書きされています。この手順ではデータが単一ファイルを上書きしていきますが、Timestampをベースとして都度都度ファイル名を変更させることができます。また、payload.jsonの中身を書き換えて、s3が含まれていない通信は、s3のファイル更新日が上書きされないことを確認しましょう。
