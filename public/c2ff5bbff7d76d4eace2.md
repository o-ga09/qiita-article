---
title: Golangに入門して詰まったこと【備忘録】　〜これからやりたいことを添えて〜
tags:
  - Go
  - Mac
  - 備忘録
  - Se
  - ハマリポイント
private: false
updated_at: '2021-05-15T19:08:49+09:00'
id: c2ff5bbff7d76d4eace2
organization_url_name: null
---
##自己紹介
SEです。

趣味の範囲でGolangに入門したので環境構築から詰まった所を備忘録として忘れないようにしておくために投稿しました。
Qiita初投稿なので生暖かい目で見てください。
アウトプットとしてこれからどんどん投稿していきたいと思っています。

##環境
Mac OS BigSur 11.3
go 1.16
VScode
M1 Macbook Air

##早速、環境構築
公式サイトからダウンロード！！！

https://golang.org/dl/

https://code.visualstudio.com/download

公式のやり方ページを参考にインストール

https://golang.org/doc/install

ついでに、vscodeも「vscode インストール」 と検索して流れでGoの拡張機能もインストール!!!

Golangのインストールを確認する。

~~~
$go version
go version go1.16rc1 darwin/arm64
$
~~~

とプロンプトが帰って来ればOK!!!

まぁ、ここまで来ればインストールは完了だけど、一応GOROOT と GOPATHを
確認する。

GOROOT

~~~
$ls -l /usr/local/
total 0
drwxr-xr-x  19 root  wheel  608  5  9 11:45 bin
drwxr-xr-x  20 root  wheel  640  1 28 07:22 go ←goのディレクトリが存在する
drwxr-xr-x   3 root  wheel   96  5  9 11:45 lib
$
~~~

GOPATH

~~~
$ls -l /Users/xxxxx/
total 441632
drwx------@  3 xxxxx  staff         96  1 31 18:08 Applications
drwx------+ 18 xxxxx  staff        576  5  5 16:53 Desktop
drwx------+  3 xxxxx  staff         96  3 13 22:57 Documents
drwx------+ 28 xxxxx  staff        896  5  9 18:22 Downloads
drwx------@ 78 xxxxx  staff       2496  5  9 14:53 Library
drwx------   5 xxxxx  staff        160  2 12 16:48 Movies
drwx------+  5 xxxxx  staff        160  1 31 17:59 Music
drwxr-xr-x@ 13 xxxxx  staff        416  3  6 22:38 OneDrive
drwx------+  4 xxxxx  staff        128  1 31 17:13 Pictures
drwxr-xr-x+  4 xxxxx  staff        128  1 31 17:12 Public
drwxr-xr-x   4 xxxxx  staff        128  1 31 22:26 development
-rw-r--r--@  1 xxxxx  staff  138412110  1 31 20:59 flutter_macos_1.22.6-stable.zip
drwxr-xr-x   5 xxxxx  staff        160  3 14 19:12 go　　　　←goのディレクトリが存在する
drwxr-xr-x  21 xxxxx  staff        672  4 12 20:49 google-cloud-sdk
-rw-r--r--@  1 xxxxx  staff   87698261  2  8 22:32 google-cloud-sdk-324.0.0-darwin-x86_64.tar.gz
$
~~~

最後に、環境変数を確認する。

~~~
$env
GOROOT=/usr/local/go
GOPATH=/Users/xxxxx/go/
(他は省略)
$
~~~

###<font color="Red">⭐️個人的に最大のハマりポイント🌟</font>

GOPATH(/Users/xxxxx/go)以外に作業ディレクトリを作成してGolangを書きたい場合、以下を設定すること。

~~~
$go env GO111MODULE="on"
$go env
GO111MODULE="on"　←ここを"on"にすること！！！
(他は省略)
~~~

【理由】

上記がonになっていない場合及び作業ディレクトリがGOPATH以外である場合

パッケージをインポートした際にGOPATH配下もしくはGOROOT配下を探しに行くため作業ディレクトリがGOPATH配下以外だとパッケージが見つからなくてエラーになるため。

***!!!環境構築完了!!!***

##GoでHelloWorld!!!

!!!作業ディレクトリの構成は以下!!!

~~~
$tree /Users/xxxxx/Desktop/golang_20210207
|--go.mod
|--go.sum
|--main            
|--main.go
$
~~~

【手順】

1. 任意の場所にディレクトリを作成する。
2. 以下のコマンドにて、モジュールを作成

~~~
$go mod init
~~~

3.(任意)デフォルトにないパッケージを使う場合は、以下のコマンドを実行する(今回は省略)

~~~
$go get "[パッケージのURL]"
~~~

4.ソースコードを編集する

~~~go:hello.go
package main

import (
    "fmt"
)

func main() {
    fmt.Println("HelloWorld!")
}

~~~

5.コードを実行

~~~
$go build hello.go
$./hello
HelloWorld!
$
~~~

***完了***

##これからGolangで作りたいもの

- OCR で画像認識を使ってレシートから文字を読み取って家計簿集計アプリ
- LINE チャットボット　(クソアプリ版)
- LINE チャットボット 有用版 (公開しても良い版)
- REST API サーバ/クライアント
- SOAP API サーバ/クライアント

##最後に

これから趣味、仕事問わず個人的に勉強になった事を投稿していきます。
文章とか説明資料の練習も兼ねつつまったりゆるくやってきます。

これから投稿していきたい記事としては、DB、OS,ネットワーク,クラウドあたりと考えています。

主に個人用ですが、読んだ方の参考になれば幸いです。



 












