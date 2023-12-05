---
title: TypescriptでCloud Loggingにログを出力する方法
tags:
  - cloudlogging
  - googlecloud
  - typescript
  - nodejs
private: false
updated_at: ""
id: null
organization_url_name: null
slide: false
ignorePublish: false
---

# はじめに

本記事は、私が、Typrscript を使用して、Cloud Logging に出力しようとした際に、
以下の点が分からず少し調べるのに時間が掛かってしまったので解決した方法を記事にしました。

- Typescript で構造化ログを出力する方法
- ログフィールドを変更する方法
- ロギングパッケージの種類

# 想定読者

- Typescript で構造化ログを出力する方法が分からない
- 「Nodejs 構造化ログ　フィールド変更」で調べてもそうじゃないって記事ばかりあった人
- ぱっと、解決方法が知りたい人

# 解決法

ロギングのインスタンスを生成する際に以下のカスタムフォーマットを設定する

1 . winston をインストール

```bash:npm
npm install winston
```

2 . loggerr インスタンスを生成

```javascript:src/middleware/logger.ts
import  winston from 'winston';


const myCustomFormat = winston.format.printf((info) => {
    // カスタムフォーマットに合わせて新しいオブジェクトを構築
    const formattedLogEntry = {
      time: new Date().toISOString(),
      severity: info.level.charAt(0).toUpperCase() + info.level.slice(1), // 先頭を大文字に変換
      "logging.googleapis.com/sourceLocation": info.sourceLocation,
      "logging.googleapis.com/labels": info.Label,
      message: info.message,
      Request: info.req
    };

    // 新しいオブジェクトを JSON 文字列に変換して返す
    return JSON.stringify(formattedLogEntry);

});
export const logger = winston.createLogger({
    format: winston.format.combine(
        myCustomFormat
    ),
    level: 'info',
    transports: [
      new winston.transports.Console(),
    ],
});
```

3 . logger を使用する

```javascript:src/lib/handler/server.ts
    this.app.listen(8080, () => {
      logger.info('starting server :8080');
    });
```

## ソースを解説

## Logger の設定について

src/middleware/logger.ts の formattedLogEntry でログフィールドを設定する。
ログフィールドの対応は以下の通り。

| 変更前    | 変更後                                | 変更                                     |
| --------- | ------------------------------------- | ---------------------------------------- |
| timestamp | time                                  | あり                                     |
| level     | severity                              | あり                                     |
| message   | message                               | なし                                     |
| -         | logging.googleapis.com/sourceLocation | cloud logging 固有のログフィールドを追加 |
| -         | logging.googleapis.com/labels         | cloud logging 固有のログフィールドを追加 |
| -         | costomLogField                        | 独自のログフィールドを追加               |

customLogField は、文字列でも、オブジェクトでも可

## Logger の使い方について

`logger.info()`の定義を見ると、` (message: string, ...meta: any[]): Logger;`となっている
ので、第二引数には、追加のメタ情報を渡すことができる。

それをカスタムフォーマットで使用するには、`info.req`のようにすれば値を取得する頃が
可能となる。

第二引数が渡されていなかった場合は、undefined となりログフィールドは出力されない。

```javascript:main.ts
const req = {
  req_id: string
  req_param: string
}

logger.info("message",req)
```

```javascript:logger.ts
const myCustomFormat = winston.format.printf((info) => {
    const formattedLogEntry = {
      Request: info.req
    };

    return JSON.stringify(formattedLogEntry);
});
```

## cloud logging での出力

![スクリーンショット 2023-12-06 7.44.56.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/1312905/bdb4ead6-ed1a-4453-dde4-bc9cbfae1e6c.png)

上記の画像のように、左側のログの重大度が severity が反映されて、「i」のアイコンになっている。
タイムスタンプの隣には、メッセージのみが出力されている。

:::note warn
`console.log()`のみだと、オブジェクト全てがタイムスタンプの隣に出力される。
また、`console.log()`1 つに対して 1 行出力されるためログも増えてしまう。
:::

# まとめ

いかがだったでしょうか？私自身、Typescript で構造化ログを出力する方法に少し手間取ってしまったので記事にしてみました。
Go だと、最近、log/slog ぱっけーが標準で追加でされ構造化ログが扱いやすくなったので。Typescript はどうだろうと
やってみましたが、割と簡単にできたが、意外と情報が少ないかな思いました。

本記事が役に立てば幸いです。

よろしければ、いいね、フォローよろしくお願いいたします。

# 参考

https://cloud.google.com/logging/docs/reference/v2/rest/v2/LogEntry#logseverity

https://cloud.google.com/logging/docs/agent/logging/configuration?hl=ja#special-fields

https://zenn.dev/aiji42/articles/b41232aea7ca34
