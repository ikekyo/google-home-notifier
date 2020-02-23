# LINEに送信したメッセージを、Google Homeで読み上げる
LINEからメッセージを送ると、設定したGoogleHomeからメッセージを読み上げてくれる

## LINE Developers
https://developers.line.biz/en/

## 使い方
### Install google-home-notifier
```shell
npm install google-home-notifier
```

### 設定ファイル　default.json
```json
{
  "server_port": "",

  "googlehome_ip": "",
  "googlehome_name": "リビングルーム",

  "beginning_sentence": "メッセージが届きました。",
  "speakable_userid": ""
}
```
- server_port 
webhookのeventを受け取るport。ngrok使用時に指定するport番号とする
- googlehome_ipに、GoogleHomeのIPアドレス ([確認方法](https://qiita.com/nigo1973/items/15b403b7658d6276946f))
- googlehome_nameは、GoogleHomeのDeviceName
- beginning_sentenceに、メッセージの冒頭にの文を記載
- speakable_useridは、特定Userからのメッセージのみ発話させたい場合に記載。

### ngrokを使う場合


ngrokでローカルにHTTPサーバを起動する
```
$ ngrok http 8080

ngrok by @inconshreveable
 (Ctrl+C to quit)

Session Status                online
Version                       2.2.8
Region                        United States (us)
Web Interface                 http://127.0.0.1:4040
Forwarding                    http://XXXXXXXX.ngrok.io -> localhost:8080
Forwarding                    https://XXXXXXXX.ngrok.io -> localhost:8080
```

ngrokが起動した状態で
```
$ node server_for_line.js
```

## 注意点
下記エラーがでて読み上げられない場合は、node_module/google-tts-api/lib/key.jsを書き換える必要がある
```
Error: get key failed from google
```
https://github.com/ikekyo/google-home-notifier/blob/master/google-tts-api/lib/key.js
