---
title: モータを制御しよう
author: ymt117
date: 2021-03-14
categories: [CanSatをはじめよう, 基礎編]
tags: [100kinsat, edusat, basic, motor]
---

<i class="{{ site.data.post.file }}"></i>
[この記事で使うソースコード](https://github.com/100kinsat/100kinsat_ver_3_4_code/tree/main/100kinsat_motor){:target="_blank"}

## モータドライバ

モータを動かすためには大きな電流を必要とします．モータドライバICを使うことで簡単にモータを制御することができます．写真に写っているICが100kinSATのモータドライバIC（[TB6612FNG](http://akizukidenshi.com/catalog/g/gI-11317/){:target="_blank"}）です．

![tb6612fng](/assets/img/post/control-motor/tb6612fng.jpg){: width="80%"}
_モータドライバIC_

TB6612FNGは1つのICで2つのモータを制御することができます．

## モータの制御

マイコンのGPIOピン3つ（IN1，IN2，PWM）で1つのモータを制御します．IN1とIN2のHIGHとLOWの組み合わせでモータの正転と逆転，ストップ，ブレーキを操作できます．PWMは0～255までの値を指定し，モータの回転速度の強弱を制御することができます．Arduino UNOでは`analogWrite()`関数を使用することができますが，ESP32ではLEDC機能を利用することで`analogWrite()`と同様の機能を使うことができます．各ピンの入力によるモータの出力の関係は表のとおりです．

![table](/assets/img/post/control-motor/motor_table.png){: width="80%"}
_モータへの入力と出力の関係_

では，モータを動かしてみましょう．

モータ用のプログラムは[motor1.ino](https://gist.github.com/ymt117/1b4b46b52df050628812f843fe81b65b){:target="_blank"}を使います．

## ソースコードの説明

### モータ制御ピンの設定

```cpp
const int motorA[3] = {4, 13, 25};  // AIN1, AIN2, PWMA
const int motorB[3] = {14, 27, 26}; // BIN1, BIN2, PWMB
```

ここではモータの制御に使用するGPIOピンを配列に格納しています．

```cpp
void setup() {
  for(int i = 0; i < 3; i++){
    pinMode(motorA[i], OUTPUT);
    pinMode(motorB[i], OUTPUT);
  }

  // 省略
}
```

次に`setup`関数内でモータ制御に使用するピンを「出力」に設定します．

配列を利用することで「for文」により一括で設定を行うことができます．

### LEDCの設定

次にLEDCの設定について説明します．

```cpp
const int CHANNEL_A = 0;
const int CHANNEL_B = 1;

const int LEDC_TIMER_BIT = 8;
const int LEDC_BASE_FREQ = 490;
```

最初にチャンネルや周波数，分解能をグローバル変数に定義しています．

今回はモータを2つ動かすため，`CHANNEL_A`と`CHANNEL_B`の2つのチャンネルを使用します．

分解能を8ビットに指定したので，PWMは0~255（2^8）の範囲で指定できます．

```cpp
void setup() {
  // 省略

  ledcSetup(CHANNEL_A, LEDC_BASE_FREQ, LEDC_TIMER_BIT);
  ledcSetup(CHANNEL_B, LEDC_BASE_FREQ, LEDC_TIMER_BIT);

  ledcAttachPin(motorA[2], CHANNEL_A);
  ledcAttachPin(motorB[2], CHANNEL_B);
}
```

`setup`関数内ではLEDC機能を設定します．

設定には`ledcSetup`関数を使用します．

```cpp
ledcSetup(channel, freq, resolution)
```

引数にチャンネル，周波数，分解能を指定します．

次に`ledcAttachPin`関数を使用してPWM信号を出力するピンとチャンネルを結びつけます．

### loop関数

最後に`loop`関数内でモータを動かしているプログラムの説明を行います．

```cpp
  // 前進
  // 左モータ（CCW，反時計回り）
  digitalWrite(motorA[1], LOW);
  digitalWrite(motorA[0], HIGH);
  ledcWrite(CHANNEL_A, 80);

  // 右モータ（CW，時計回り）
  digitalWrite(motorB[1], LOW);
  digitalWrite(motorB[0], HIGH);
  ledcWrite(CHANNEL_B, 80);
```

`digitalWrite`関数でピンの出力を「LOW」または「HIGH」にしています．この組み合わせにより，モータの正回転，逆回転を制御することができます．
CCWはCounterClockWiseを意味します．

PWMの出力には`ledcWrite`関数を使用します．第1引数に出力するピンのチャンネルを指定し，第2引数にPWM値を指定しています．第2引数には0~255の値を指定することができます．

　PWM値を変化させることでモータの回転速度が変化するので，いろいろな値を入力して動作を確認してください．