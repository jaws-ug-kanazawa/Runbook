---
title: "LINE ログインチャネルの作成"
---

# チャネル作成
- チャネルの作成
https://developers.line.biz/ja/services/line-login/ にアクセス。
「今すぐはじめよう」のボタンを押して進めていきましょう。
![](https://storage.googleapis.com/zenn-user-upload/kk09ycv3181bxkla6mi8vozaysvd)

- チャネルの種類
LINEログインになっているか確認します。
![](https://storage.googleapis.com/zenn-user-upload/tu6u2hc6g83thpcqgrdkw3se4ph7 =500x)

- プロバイダ
Messaging API チャネルで使用したプロバイダーを選択しましょう。
![](https://storage.googleapis.com/zenn-user-upload/ygq2jt08ywonwjy8ki5ap8rirtc7 =500x)

- 地域、チャネルアイコン
地域は「日本」、チャネルアイコンを登録しましょう。（今回は必須ではありません）
![](https://storage.googleapis.com/zenn-user-upload/bsd3zk5de6uwrjuygwzooxzwa9mb =600x)

- チャネル名、チャネル説明
下記を入力しましょう。
チャネル名：「スマートリテール」
チャネル説明：「スマートリテール」
![](https://storage.googleapis.com/zenn-user-upload/5fb5a35fdf70816827d91159.png)

- アプリタイプ
アプリタイプは「ウェブアプリ」にチェックをつけましょう。
![](https://storage.googleapis.com/zenn-user-upload/xi654rczexr7dabdutg5uj5ljrjw)

- メールアドレス、プライバシーポリシーURL、サービス利用規約URL
メールアドレスを確認しましょう。
プライバシーポリシーURLとサービス利用規約URLは入力しないで大丈夫です。
![](https://storage.googleapis.com/zenn-user-upload/99cgwnkz1s27xti6jtakdg87ijdr)

- 作成
下記 開発者契約に同意し、チェックをして「作成」ボタンを押しましょう。
![](https://storage.googleapis.com/zenn-user-upload/o6zjh4ihmtazma4lm2xxs0qvclix)

# チャネル基本設定

- リンクされたボット（ページの下の方にあります）
さきほど作成したMessagingAPIのチャネルを選択し、更新を行います。
![](https://storage.googleapis.com/zenn-user-upload/408a53fbc738b75b62fbe287.png)
![](https://storage.googleapis.com/zenn-user-upload/41c96c33b780321a0cf262f8.png)

# LIFFの作成
- 作成
「LIFF」タブに移動して「追加」ボタンを押しましょう。
![](https://storage.googleapis.com/zenn-user-upload/lafgohpi6jrva9gfltyej6073a5u)

- LIFFアプリ名、サイズ
LIFFアプリ名は「スマートリテール」、サイズは「Full」を選択しましょう。
![](https://storage.googleapis.com/zenn-user-upload/dbad2384834df29e0feb1b07.png)


- エンドポイントURL
エンドポイントURLは仮で「https://example.com 」と入力します。URLが決まったら変更します。
![](https://storage.googleapis.com/zenn-user-upload/1cwbw25kf8chkf7rx56zt72ura10)

- Scope
Scopeは「profile」、「openid」にチェックをつけましょう。
![](https://storage.googleapis.com/zenn-user-upload/ojmcafkfz0yc9njc15b60c2eh7wn)

- ボットリンク機能
ボットリンク機能は「On」にチェックをつけて、「追加」ボタンを押しましょう。
![](https://storage.googleapis.com/zenn-user-upload/3qin3g2dilsn0k3e3io8j27kai9p)

- LIFF ID と LIFF URL
LIFF ID と LIFF URL をメモしましょう。
![](https://storage.googleapis.com/zenn-user-upload/xept4q6oi29q68tba0v05yteek86)

