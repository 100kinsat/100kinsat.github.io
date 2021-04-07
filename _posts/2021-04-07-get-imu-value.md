---
title: 9軸センサの値を取得しよう
author: ymt117
date: 2021-04-06
categories: [CanSatをはじめる前に, 基礎編]
tags: [100kinsat, edusat, basic, imu]
---

## ライブラリのインストール

100kinSATには9軸センサが搭載されています．
加速度，ジャイロ，地磁気に関して，それぞれX・Y・Z軸の3方向測定できるので3×3で9軸センサとなっています．

100kinSATのマイコン（ESP32）と9軸センサはI2C（アイスクエアドシー，アイツーシー）という通信規格でデータのやり取りを行います．
I2C通信についてはここでは詳しく説明しません．
9軸センサを簡単に扱えるライブラリがあるため，今回はそちらをインストールして使います．

[https://github.com/bolderflight/MPU9250](https://github.com/bolderflight/MPU9250)のGitHubリポジトリからライブラリをインストールしましょう．
下記画像に示すように「Code」→「Download ZIP」とクリックしてZIPファイルをダウンロードします．

![mpu1](/assets/img/post/get-imu-value/mpu9250.jpg){: width="80%"}
_ライブラリのダウンロード_

そして，Arduino IDEのライブラリにインポートします．
インポートはArduino IDEのメニューから「スケッチ」→「ライブラリをインクルード」→「.ZIP形式のライブラリをインストール」で先ほどダウンロードしたZIPファイルを選択します．
これでライブラリのインストールは完了です．

![mpu2](/assets/img/post/get-imu-value/mpu9250_2.png){: width="80%"}
_ライブラリのインストール_

## サンプルプログラムの実行

ライブラリをインストールしたので，サンプルプログラムを実行してみましょう．
サンプルプログラムは，Arduino IDEのメニューから「ファイル」→「スケッチ例」→「Bolder Flight Systems MPU9250」→「Basic_I2C」をクリックして開きます．

![mpu3](/assets/img/post/get-imu-value/mpu9250_3.png){: width="80%"}
_サンプルプログラムを開く_

サンプルプログラムが開けたら，パソコンと100kinSATをケーブルで接続していることを確認して，Arduino IDEのメニューから「ツール」でボードを「ESP32 Dev Module」に設定して，シリアルポートを選択します．
「マイコンボードに書き込む」のボタンを押してサンプルプログラムを100kinSATに書き込みます．
書き込みが成功したら，シリアルモニタを開いて動作を確認しましょう．
画像のように各センサの値が表示されれば成功です．
もし何も表示されなかったり文字化けしていたりする場合は，ボーレートが115200になっているか確認してみてください（画像の赤枠で囲ったところ）．

![mpu4](/assets/img/post/get-imu-value/mpu9250_4.png){: width="80%"}
_ボーレートの設定_

シリアルモニタには9軸センサから取得した値がそれぞれ表示されています．
しかし，これではただ数字が表示されているだけでよくわかりません．
Arduino IDEにはシリアルモニタ以外にシリアルプロッタという機能があります．
シリアルプロッタを使用すると，センサから取得した値をグラフとしてみることができます．

シリアルモニタを閉じてから，Arduino IDEのメニューの「ツール」→「シリアルプロッタ」をクリックしてみてください．
シリアルプロッタが開き，画像のようにセンサの値がグラフとして描画されるはずです．
100kinSATを上下に振ってみたり，左右に揺らしてみたりしてセンサの値が変化することをグラフで確認してみてください．

![mpu5](/assets/img/post/get-imu-value/mpu9250_5.png){: width="80%"}
_シリアルプロッタを開く_
![mpu6](/assets/img/post/get-imu-value/mpu9250_6.png){: width="80%"}
_シリアルプロッタの画面_

## ソースコードの説明

最初の行でMPU9250のライブラリをincludeして，次の行でインスタンスを初期化しています．
インスタンスの初期化の際，コンストラクタに引数を渡しています．
渡している引数は，第一引数が`Wire`ライブラリのインスタンス，第二引数がMPU9250のI2Cアドレスです．

```cpp
#include "MPU9250.h"

// an MPU9250 object with the MPU-9250 sensor on I2C bus 0 with address 0x68
MPU9250 IMU(Wire,0x68);
```

`setup`関数では，シリアル通信の初期化と9軸センサとの通信の開始（I2C通信の開始）をしています．

`IMU.begin()`が9軸センサとの通信の開始です．
`begin()`メソッドは9軸センサの初期設定を行い，通信の準備が完了すると返り値として`1`を返します．
初期設定に失敗すると負の値が返って来ます．
int型の変数`status`に返り値が代入されるので，if文による判定で初期設定に失敗したらエラーのメッセージがシリアルモニタに表示されます．
初期設定に成功したら`loop`関数に遷移します．

```cpp
void setup() {
  // serial to display data
  Serial.begin(115200);
  while(!Serial) {}

  // start communication with IMU 
  status = IMU.begin();
  if (status < 0) {
    Serial.println("IMU initialization unsuccessful");
    Serial.println("Check IMU wiring or try cycling power");
    Serial.print("Status: ");
    Serial.println(status);
    while(1) {}
  }
}
```

`loop`関数では，9軸センサから値を取得してシリアルモニタに出力する処理を行っています．

`IMU.readSensor()`でセンサの値を読み取っています．
読み取った値のうち加速度センサのX軸の値は`getAccelX_mss()`メソッドで取得できます．
Y軸，Z軸は`getAccelY_mss()`，`getAccelZ_mss()`メソッドで取得できます．
同様に，ジャイロセンサや地磁気センサの各値も取得するメソッドも用意されています．

`Serial.print("\t");`の「\t」はタブ文字を出力しています．
各センサの値の間にタブを出力することで，シリアルモニタに表示したときに見やすくしています．

```cpp
void loop() {
  // read the sensor
  IMU.readSensor();
  // display the data
  Serial.print(IMU.getAccelX_mss(),6);
  Serial.print("\t");
  Serial.print(IMU.getAccelY_mss(),6);
  Serial.print("\t");
  Serial.print(IMU.getAccelZ_mss(),6);
  Serial.print("\t");
  Serial.print(IMU.getGyroX_rads(),6);
  Serial.print("\t");
  Serial.print(IMU.getGyroY_rads(),6);
  Serial.print("\t");
  Serial.print(IMU.getGyroZ_rads(),6);
  Serial.print("\t");
  Serial.print(IMU.getMagX_uT(),6);
  Serial.print("\t");
  Serial.print(IMU.getMagY_uT(),6);
  Serial.print("\t");
  Serial.print(IMU.getMagZ_uT(),6);
  Serial.print("\t");
  Serial.println(IMU.getTemperature_C(),6);
  delay(100);
}
```
