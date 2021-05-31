---
title: 緯度と経度を取得しよう
author: ymt117
date: 2021-04-09
last_modified_at: 2021-05-31
categories: [CanSatをはじめよう, 基礎編]
tags: [100kinsat, edusat, basic, gps sensor]
---

<i class="{{ site.data.post.file }}"></i>
[この記事で使うソースコード](https://github.com/100kinsat/100kinsat_ver_3_4_code/tree/main/100kinsat_gps_lat_lng){:target="_blank"}

## ライブラリのインストール
---

[GPSセンサの値を取得しよう]({% post_url 2021-03-28-get-gps-value %}){:target="_blank"}でGPSセンサが受信する値を取得しました．

受信した値は，緯度経度等の情報を含む文字の羅列でした．
CanSatの制御プログラムを書いていく上では，ここから必要な情報を取り出す必要があります．

CanSatの誘導においてGPSセンサから取得した値のうち，緯度と経度の情報を使う場合が多いです．
ここでは，ライブラリを使ってGPSセンサが受信した値から，緯度と経度を取得していきます．

最初に[https://github.com/mikalhart/TinyGPSPlus](https://github.com/mikalhart/TinyGPSPlus){:target="_blank"}のGitHubリポジトリからライブラリをインストールしましょう．
リポジトリからZIPファイルをダウンロードして，Arduino IDEにインポートします．
インストールの詳しい方法は[9軸センサの値を取得しよう]({% post_url 2021-04-07-get-imu-value %}){:target="_blank"}で詳しく説明しています．

## 緯度・経度を取得するプログラムを作成する
---

ライブラリのインストールが完了したら，緯度・経度を取得するプログラムを作成していきます．
まずはライブラリをincludeします．
`TinyGPSPlus gps`はTinyGPSPlusのインスタンスを生成しています．
`gps.location.lat()`のようにメソッドにアクセスして緯度を取得できます．

GPSセンサとマイコンの通信にハードウェアシリアルを使用するのは[GPSセンサの値を取得しよう]({% post_url 2021-03-28-get-gps-value %}){:target="_blank"}と同じです．

```cpp
#include <TinyGPS++.h>

static const uint32_t GPSBaud = 9600;
TinyGPSPlus gps;
HardwareSerial ss(2);
```

`setup`関数ではソフトウェアシリアルとハードウェアシリアルのボーレートを設定しています．
今回はGPSセンサとの通信に用いるハードウェアシリアルのボーレートを`GPSBaud`という変数に定義してみました．
`static const`を宣言しているので，`GPSBaud`は定数になります．
よく使う変数は定数としてこのように定義することもできます．

```cpp
void setup() {
  Serial.begin(115200);
  ss.begin(GPSBaud);

  Serial.println("GPS start!");
}
```

`loop`関数を見ていきましょう．
`ss.read()`でGPSセンサから読み取った値をchar型の変数`c`に代入して，`gps.encode()`の引数として渡しています．

GPSセンサから取得できる値はNMEAフォーマットの情報となっています．
1行が`$GPGGA,061251.000,3542.0553,N,...`のように先頭が「$」で始まり，「改行文字（\r\n）」で終わります．
各行は「,」で区切られています．
`gps.encode()`メソッドはNMEAフォーマットの文字列をパースする役割をしています．

GPSセンサから更新された位置情報を取得すると`gps.location.isUpdated()`から`true`が返ってきて，`gps.location.lat()`で緯度の値を，`gps.location.lng()`で経度の値をそれぞれ取得できます．

```cpp
void loop() {
  while(ss.available() > 0){
    char c = ss.read();
    gps.encode(c);
    if(gps.location.isUpdated()){
      Serial.print("Lat=\t");   Serial.print(gps.location.lat(), 6);
      Serial.print(" Lng=\t");   Serial.println(gps.location.lng(), 6);
    }
  }
}
```

緯度経度が取得できると，シリアルコンソールに緯度経度の値が出力されます．

![gps-lat-lng](/assets/img/post/get-gps-value-lat-lng/gps_lat_lng.png){: width="80%"}
_GPSセンサから緯度・経度の情報を取得した様子_
