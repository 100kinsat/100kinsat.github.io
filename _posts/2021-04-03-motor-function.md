---
title: モータの制御プログラムを関数化しよう
author: ymt117
date: 2021-04-03
categories: [CanSatをはじめる前に, 基礎編]
tags: [100kinsat, edusat, basic, motor]
---

- [この記事で使うソースコード](https://github.com/100kinsat/100kinsat_ver_3_4_code/tree/main/100kinsat_motor_function{:target="_blank"}

ここでは[モータを制御しよう]({% post_url 2021-03-14-control-motor %}){:target="_blank"}で書いたプログラムを関数化します．
関数化することでよく使うプログラムを何度も書かずに使いまわすことができます．
また，ソースコードの削減や可読性の向上が期待できます．

## 関数を作成する

Arduinoのプログラムは`setup`関数と`loop`関数が必要です．
それ以外に関数を追加したい場合は下記のように`function1()`や`function2()`を追加します．

```cpp
void setup() {
  // ここに最初に1回だけ実行する処理を書く
}

void loop() {
  // ここに繰り返す処理を書く
}

void function1() {
  // ここに関数化するソースコードを書く
}

void function2() {
  // ここに関数化するソースコードを書く
}
```

モータの正転制御のプログラムは下記のように関数化できます．
`ccw()`という関数にしました．
ccwはCounterClockWiseを意味します．
これで`loop`関数から`ccw(80)`のように呼び出すとモータの正転制御ができます．
このとき関数に80という引数（ひきすう）を渡しています．
引数は関数が受け取る値で，今回は`int`型の`pwm`という変数を関数に定義しています．
引数のpwmは0~255の値を渡すようにします．

```cpp
/** 正転（反時計回り） */
void ccw(int pwm) {
  digitalWrite(motorA[0], LOW);
  digitalWrite(motorA[1], HIGH);
  ledcWrite(CHANNEL_A, pwm);
  
  digitalWrite(motorB[0], LOW);
  digitalWrite(motorB[1], HIGH);
  ledcWrite(CHANNEL_B, pwm);
}
```

同様に，逆転と停止の制御をそれぞれ`cw()`，`stop()`という関数にします．
関数にすることで`loop`関数は以下のようになります．

```cpp
void loop() {
  ccw(80);
  delay(1000);

  stop();
  delay(1000);

  cw(80);
  delay(1000);

  stop();
  delay(1000);
}
```

関数化する前の`loop`関数と比較してソースコードを短く，わかりやすく書けるようになりました．
特に停止の処理は，これまで同じ内容を2回書いていましたが，関数にすることで単に`stop()`と書くだけでよくなりました．
