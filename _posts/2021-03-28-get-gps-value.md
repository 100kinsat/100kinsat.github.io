---
title: GPSセンサの値を取得しよう
author: ymt117
date: 2021-03-28
categories: [CanSatをはじめる前に, 基礎編]
tags: [100kinsat, edusat, basic, gps]
---

<i class="{{ site.data.post.file }}"></i>
[この記事で使うソースコード](https://github.com/100kinsat/100kinsat_ver_3_4_code/tree/main/100kinsat_gps_raw_data){:target="_blank"}

### GPSセンサについて

100kinSATは秋月電子で購入できるGPSセンサを搭載しています．GPSセンサを使うと衛星から様々な情報を所得することができます．CanSat競技では，センサから緯度・経度の情報を所得することで自分の位置を把握してゴールに向かう制御を行う方法が一般的です．
しかし，今回用いるGPSセンサはある程度開けた場所でも5~10mの誤差があるため，ゴールまでの距離0mを達成するためにはカメラを用いる等ほかのセンサを組み合わせた工夫が必要になります．

![gps-sensor](http://akizukidenshi.com/img/goods/C/K-09991.jpg){: width="80%"}
_GPSセンサ_

### GPSセンサとマイコンの接続

GPSセンサとマイコンはUARTで通信を行います．接続は以下の表のようになっています．

|ESPマイコン|GPSセンサ|
|:---:|:---:|
|P16(RX)|TXD|
|P17(TX)|RXD|

表のように，UARTの接続はマイコンのTXピンをセンサのRXピンと，マイコンのRXピンをセンサのTXピンと接続します．
TXピンから信号を送り，RXピンで受信します．
100kinSATの回路図上ではTXピンとRXピンのいずれも接続していますが，GPSセンサから値を取得するだけであれば，GPSセンサのRXピンに接続する必要はありません．

### ソースコード

以下に示すのは，単にGPSセンサから所得した値を表示するだけのプログラムです．
実際に誘導を行うためには，取得した値から緯度・経度の情報を抽出する必要があります．

```cpp
HardwareSerial gps(2);

void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  Serial.println("start");
  gps.begin(9600);
}

void loop() {
  // put your main code here, to run repeatedly:
  if(gps.available()){
    Serial.write(gps.read());
  }
}
```

シリアルコンソールに文字が表示されない/文字化けするという場合は，ボーレートがプログラムで設定した値と同じであるか，COMポートが正しく選択されているかなど確認してみてください．

### ソースコードの説明

```cpp
HardwareSerial gps(2);
```

GPSセンサの値を取得するためにESP32マイコンのハードウェアシリアル通信を用いています．
ESP32にはUART通信が行えるハードウェアシリアルピンが3つ用意されています（UART0, UART1, UART2）．
上記のプログラムではUART2を選択しています．

```cpp
gps.begin(9600);
```

ハードウェアシリアルのボーレートを`9600[bps]`に設定しています．
このボーレートはGPSセンサの初期設定に合わせた値です．
基本的には初期設定のままで問題ありません．
GPSセンサの設定を変更したい場合は，[秋月電子の販売ページ](https://akizukidenshi.com/catalog/g/gK-09991/){:target="_blank"}にある取扱説明書PDFファイルを参考にしてください．

```cpp
if(gps.available()){
  Serial.write(gps.read());
}
```

`gps.available()`でGPSセンサから文字列（シリアルデータ）を取得しています．そして`gps.read()`で受信した文字列を読み込み，`Serial.write()`でシリアルコンソールに出力します．

シリアルコンソールで取得した文字列が確認できます．

![gps-value]()

### GPSセンサから取得した値に緯度・経度が表示されないとき

GPSセンサが衛星を補足するまでは数分~十数分程度かかります．
GPSセンサが衛星を補足すると，GPSセンサ基板の赤色のLEDが点滅します．
LEDが点滅せず単に点灯しているだけの場合は，衛星が補足できていない可能性があります．見晴らしの良い公園などで実験してみてください．

![complemental-gps](/assets/img/post/get-gps-value/complemental_gps.gif){: width="80%"}
_GPSセンサが衛星を補足した様子_

### その他

ESPマイコンとGPSセンサについて（ESPマイコンのUART，ハードウェアシリアルについて）は[ココ](https://github.com/ymt117/esp32-dev/wiki/GPS){:target="_blank"}にも少しまとめています．