---
title: ファイルの読み書きをしよう
author: ymt117
date: 2021-05-20
categories: [CanSatをはじめよう, 基礎編]
tags: [100kinsat, edusat, basic, SDカード]
---

今回はmicroSDカード（以下SDカードと表記）にテキストファイルを読み書きしてみます．
SDカードにテキストファイルの読み書きができるとCanSatが取得したセンサの値や制御履歴をログとして残すことができます．

![sd-slot](/assets/img/post/sd-card-sample/sd-slot.jpg){: width="80%"}
_SDカードスロット_

## スケッチ例を読み込む

まずはSDカードのサンプルスケッチを開きます．
Arduino IDEメニューの「ファイル」>「スケッチ例」>「SD（esp32）」>「SD_Test」にSDカードのサンプルスケッチがあります．

メニューにサンプルスケッチがない場合は，下記リポジトリにライブラリがあるのでここからダウンロードしてきます．

- [SDカード用ライブラリ](https://github.com/espressif/arduino-esp32/tree/master/libraries/SD){:target="_blank"}

![sd-sample-sketch](/assets/img/post/sd-card-sample/sd-sample.png){: width="80%"}
_SDカード読み書きのサンプルスケッチを開く_

サンプルスケッチをCanSatに書き込みます．
microSDカードスロットにSDカードを挿入して実行するとコンソールには以下のように読み書きのログが表示されます．

![sd-sample-sketch-console](/assets/img/post/sd-card-sample/sd-sample-console.png){: width="80%"}
_SDカードに読み書きしたときのコンソールログ_

実行後，SDカードの中身をPCで確認してみると，`foo.txt`ファイルに「Hello World!」の文字列が書かれています．

SDカードの種類によってはファイルの読み書きができないものもあります．
うまく動作しないときはSDカードを変更してみてください.

秋月電子で販売している[KIOXIAのmicroSDカード 16GB](https://akizukidenshi.com/catalog/g/gS-15845/){:target="_blank"}は読み書きできることを確認済みです．

## スケッチ例に用意されている関数

上記サンプルスケッチには以下の関数があり，`setup()`関数内でそれぞれの関数を呼び出しています．
CanSat競技では，ファイルへの新規書き込みと追記書き込み，ファイルの読み込みを使うことが多いでしょう．

|関数名|概要|
|:---|:---|
|listDir|ディレクトリ一覧表示|
|createDir|ディレクトリ作成|
|removeDir|ディレクトリ削除|
|readFile|ファイル読み込み|
|writeFile|ファイル書き込み（新規作成）|
|appendFile|ファイル書き込み（追記）|
|renameFile|ファイル名変更|
|deleteFile|ファイル削除|
|testFileIO|ファイル読み書き速度の測定|


