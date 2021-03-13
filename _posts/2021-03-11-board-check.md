---
title: 基板の動作確認
author: ymt117
date: 2021-03-11
category: [CanSatをはじめる前に]
tags: [100kinsat, edusat]
---

### Lチカ（I/Oの動作確認）

電子部品の実装を終えたら基板の動作確認をします．

Lチカのプログラムを書き込んで動作確認をしましょう．

まず[開発環境のセットアップ]({% post_url 2021-03-09-setup-the-development-environment %})でインストールしたArduino IDEを起動してください．

Arduino IDEを起動したら，以下のソースコード([blink.ino](https://gist.github.com/ymt117/2b3c5da8cf7bde8671921cffae173766))を入力してください．

```cpp
#define LED 2

void setup() {
  // LEDに接続したピンを「出力（OUTPUT）」に設定
  pinMode(LED, OUTPUT);
}

void loop() {
  // LEDを点灯
  digitalWrite(LED, HIGH);
  delay(500);
  // LEDを消灯
  digitalWrite(LED, LOW);
  delay(500);
}
```
次にプログラムが正しいかどうかチェック（コンパイル）します．

Arduino IDEのメニュー欄（画面上部）にある「矢印」マーク（検証ボタン）をクリックしてください．

![ltika1](/assets/img/post/board-check/ltika1.png){: width="50% .normal}

検証ボタンをクリックするとスケッチの保存先を聞かれると思います．

余談ですが，Arduinoではプログラムのことをスケッチと呼び，拡張子は「ino」です．

このWebページでは「スケッチ」と「プログラム」の用語は区別しません．

Arduinoのスケッチはスケッチ名と同じフォルダにスケッチが保存されている必要があります．

例）「/スケッチ名/スケッチ名.ino」

任意の保存先に適当な名前を付けて保存してください．

「コンパイルが完了しました」と表示されればOKです．

![ltika2](/assets/img/post/board-check/ltika2.png){: width="50% .normal}

コンパイルに失敗した場合は[トラブルシューティング]({% post_url 2021-03-11-trouble-shooting %})のページを参照してください．

コンパイルが完了したら，次は100kinSATにプログラムを書き込んでみましょう．

プログラムを書き込む際は，PCと100kinSATをUSBケーブルで接続してください．

PCと接続したら，Arduio IDEがESP32マイコンを正しく認識しているか確認します．

メニューの「ツール」→「シリアルポート」にCOMポートが表示され，チェックが入っていることを確認してください．

COMポートの番号はボードによって異なるので写真と異なる番号でも問題ありません．

検証ボタンの隣にある「マイコンボードに書き込む」ボタンをクリックします．

![ltika](/assets/img/post/board-check/ltika.png){: width="50% .normal}

「マイコンボードに書き込む」ボタンをクリックすると，再度コンパイルが行われたのち書き込みが行われます．

![ltikagif](/assets/img/post/board-check/ltika.gif){: width="50% .normal}

Lチカ出来ましたね！

### ソースコードの説明

#### マクロ定義

```cpp
#define LED 2
```

GPIO2ピンをLEDという名前にマクロ定義しています．

このように定義することで，プログラム中で「LED」と入力したときと「2」と入力したときのどちらも「2」を表すようになります．

```cpp
  // LEDを点灯
  digitalWrite(LED, HIGH);
```

そのため上記プログラムは`digitalWrite(2, HIGH);`と書いた場合と同じ意味を持ちます．

マクロ定義を活用することでLEDを接続しているピンをHIGHにしていることが明確になり，ピン番号をそのまま使用するよりプログラムが読みやすくなります．

また，プログラムの書き間違いを防止することにも繋がります．

#### setup関数

```cpp
void setup() {
  // LEDに接続したピンを「出力（OUTPUT）」に設定
  pinMode(LED, OUTPUT);
}
```

setup関数はESP32マイコンに電源が入ったときやリセットしたときに1度だけ実行される関数です．

setup関数ではGPIOピンの入出力を設定したりシリアル通信のボーレートを設定したりします．

`pinMode(pin, mode)`でGPIOピンの入出力を設定することができます．

ここでは「LED（2）」を「OUTPUT（出力）」に設定しています．

#### loop関数

loop関数はsetup関数で各種設定を行ったあと実行される関数です．

loop関数はsetup関数と異なり，繰り返し実行されます．

```cpp
void loop() {
  // LEDを点灯
  digitalWrite(LED, HIGH);
  delay(500);
  // LEDを消灯
  digitalWrite(LED, LOW);
  delay(500);
}
```

上記のプログラムではLEDに接続しているGPIO2を500ミリ秒間HIGHにして，その後500ミリ秒間LOWにするという動作を繰り返します．

ピンの状態をHIGHにするとLEDが点灯し，LOWにすると消灯します．

この動作を繰り返すことでLEDがチカチカ点灯するためLチカと呼ばれます．