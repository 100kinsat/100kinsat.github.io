---
title: モータの制御プログラムをライブラリ化しよう
author: ymt117
date: 2021-04-06
categories: [CanSatをはじめる前に, 基礎編]
tags: [100kinsat, edusat, basic, motor]
---

<i class="{{ site.data.post.file }}"></i>
[この記事で使うソースコード](https://github.com/100kinsat/100kinsat_ver_3_4_code/tree/main/100kinsat_motor_library){:target="_blank"}

ここでは[モータの制御プログラムを関数化しよう]({% post_url 2021-04-03-motor-function %}){:target="_blank"}で書いたプログラムをファイル分割してライブラリ化します．
モータの制御プログラムはAのファイル，センサのプログラムはBのファイルというように分割して作成することで，役割ごとにプログラムを分けることができます．
分割したプログラムはライブラリとして読み込むことで使用できます．
ライブラリ化しておくと，様々なプログラムで再利用することが可能となり，大規模なプログラムや似た処理のプログラムを作るときに楽ができます．

## ヘッダファイルとcppファイルの作成

まずはArudino IDE上部メニューの「ファイル」から「新規ファイル」をクリックして新しいスケッチ（inoファイル）を作成します．
`100kinsat_motor_library.ino`というファイル名にしました．
次にヘッダファイルとcppファイルを追加します．
ファイルの追加はIDEの右上部にある三角アイコンの「新規タブ」からできます．
ファイル名に`motor.hpp`と`motor.cpp`を入力して作成します．

![new_file](/assets/img/post/motor-library/new_file.png){: width="80%"}
_新規ファイルの作成_

## ヘッダファイルのプログラムを実装する

まずはヘッダファイルのプログラムを書いていきます．
ヘッダファイルの上部と下部に`#ifndef`と`#endif`を書くことでインクルードガードしています．
`#ifndef __MOTOR_H__`と書くことで，「もし`__MOTOR_H__`が定義されていなかったら，`#endif`までのプログラムを実行する」というような意味になります．
これはヘッダファイルがプログラム中で二重に読み込まれることを防ぐ処置です．
先に述べたように，分割したプログラムは他のプログラムでライブラリとして読み込みます．
ファイルを分割する理由は，人間がプログラムするうえで扱いやすくするためで，分割したプログラムは最終的に一つのプログラムとしてコンパイルされます．
そのとき，複数箇所で同じライブラリを読み込んでいると二重に読み込んでしまい，コンパイルエラーとなってしまいます．
インクルードガードを書いておくことで，既にライブラリが読み込まれていた場合，二重に読み込まないようにしてくれます．

```cpp
#ifndef __MOTOR_H__ // インクルードガード
#define __MOTOR_H__

#include "Arduino.h"

class Motor {
  // ここにクラスの中身を書く
};

#endif // __MOTOR_H__
```

ヘッダファイルの中身には，`Motor`クラスを定義しています．
`Motor`クラスはコンストラクタ（クラスの初期化をする処理）と`forward()`，`back()`，`stop()`メソッド持っています．
c言語において，クラスに定義した関数のことをメソッドと呼びます．

`forward()`，`back()`，`stop()`メソッドにはcppファイルでそれぞれ前進，後退，停止の処理を実装していきます．
これらのメソッドは`public`で定義しています．
`public`にすることでこのライブラリを読み込んだプログラム上で，これらのメソッドを呼び出すことができます．

`private`にはモータに接続しているマイコンのピンなどの変数を定義しています．
`private`にすることで，ライブラリを読み込んだプログラム上からは参照できなくすることができます．

```cpp
class Motor {
  public:
    Motor();

    void forward(int pwm); // 前進
    void back(int pwm); // 後退
    void stop(); // 停止

  private:
    const int motorA[3] = {4, 13, 25}; // AIN1, AIN2, PWMA
    const int motorB[3] = {14, 27, 26}; // BIN1, BIN2, PWMB

    const int CHANNEL_A = 0;
    const int CHANNEL_B = 1;

    const int LEDC_TIMER_BIT = 8;
    const int LEDC_BASE_FREQ = 490;
};
```

## cppファイルのプログラムを実装する

次に，cppファイルを実装していきます．
最初の行は，上で作成したヘッダファイルを読み込んでいます．

```cpp
#include "motor.hpp"
```

そして，ヘッダファイルの`Motor`クラスに定義した各メソッドを定義していきます．
`Motor::Motor()`は`Motor`クラスのコンストラクタになります．

```cpp
Motor::Motor() {
  for (int i = 0; i < 3; i++) {
    pinMode(motorA[i], OUTPUT);
    pinMode(motorB[i], OUTPUT);
  }

  ledcSetup(CHANNEL_A, LEDC_BASE_FREQ, LEDC_TIMER_BIT);
  ledcSetup(CHANNEL_B, LEDC_BASE_FREQ, LEDC_TIMER_BIT);

  ledcAttachPin(motorA[2], CHANNEL_A);
  ledcAttachPin(motorB[2], CHANNEL_B);
}
```

以下は前進制御のメソッドです．
`Motor::forward()`と書くことで，`forward`メソッドは`Motor`クラスに紐づいたメソッドとなります．
`back`や`stop`メソッドも同様です．

```cpp
/**
 * 前進
 */
void Motor::forward(int pwm) {
  // 左モータ（CCW，反時計回り）
  digitalWrite(motorA[1], LOW);
  digitalWrite(motorA[0], HIGH);
  ledcWrite(CHANNEL_A, pwm);

  // 右モータ（CW，時計回り）
  digitalWrite(motorB[1], LOW);
  digitalWrite(motorB[0], HIGH);
  ledcWrite(CHANNEL_B, pwm);
}
```

これで，モータ制御のヘッダファイルとcppファイルが作成できました．

## メインのプログラムから分割したファイルを読み込んで使う

最後に，メインのプログラムからモータ制御のヘッダファイルとcppファイルをライブラリとして読み込みます．
`100kinsat_motor_library.ino`の最初の行で作成したライブラリをincludeしています．
そして，`Motor`クラスの`motor`という変数を定義して，コンストラクタを呼び出しています．
これで，`motor.forward()`のように「.（ドット）」でメソッドを繋いで，メソッドを使うことができます．

[モータの制御プログラムを関数化しよう]({% post_url 2021-04-03-motor-function %}){:target="_blank"}では，一つのファイルにすべてのプログラムを記述していましたが，ファイル分割することで役割ごとにファイルを分けることができました．
そして，メインのプログラムとなる`100kinsat_motor_library.ino`はすっきりと書くことができています．

```cpp
#include "motor.hpp"

Motor motor = Motor();

void setup() {
}

void loop() {
  motor.forward(100);
  delay(1000);

  motor.stop();
  delay(1000);

  motor.back(100);
  delay(1000);

  motor.stop();
  delay(1000);
}
```

ここまででモータ制御のプログラムを`loop`関数に書く方法，関数化する方法，ファイル分割する方法の3つのやり方で書いてきました．
CanSatの制御プログラムはモータ制御だけでなく，各センサを読み込んだり，取得したデータを記録したりとさまざまなプログラムを書く必要があります．
そうすると，プログラムは大規模なものとなり，一つのファイルに書くだけでは，大変見通しの悪いソースコードとなってしまいます．
見通しの悪いソースコードはバグが発生しやすく，バク修正等のメンテナンスも煩雑になりがちです．
機能ごとに適切にファイル分割したプログラムを作成していきましょう．
