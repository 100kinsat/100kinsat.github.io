---
title: GPSセンサで取得した位置情報をGoogleマップに描画しよう
author: ymt117
date: 2021-04-12
categories: [CanSatをはじめよう, 基礎編]
tags: [100kinsat, edusat, basic, gps sensor]
---

<i class="{{ site.data.post.file }}"></i>
[この記事で使うソースコード](https://github.com/100kinsat/100kinsat_ver_3_4_code/blob/main/100kinsat_gps_lat_lng_csv){:target="_blank"}

## TeraTermのインストール

[緯度と経度を取得しよう]({% post_url 2021-04-09-get-lat-lng-value %}){:target="_blank"}でGPSセンサから取得した情報から緯度・経度の値のみを取得することができました．

ここでは，緯度・経度の情報をCSVファイルとして保存してGoogleに描画をしてみます．

CanSatは競技のあと制御ログを提出する必要があります．
制御ログには，「センサからAの値を取得した．だからBの制御をした」というような説明ができるようにログを残す必要があります．

制御ログの考え方として秋田大学 平山先生の下記投稿が参考になると思います．

<blockquote class="twitter-tweet"><p lang="ja" dir="ltr"><a href="https://twitter.com/hashtag/CanSat?src=hash&amp;ref_src=twsrc%5Etfw">#CanSat</a> の「制御履歴」には、状態量の観測値だけでなく、制御量もなければ説得力のある記録と言えません。 <a href="https://twitter.com/hashtag/%E3%81%AE%E3%81%97%E3%82%8D%E3%82%B5%E3%83%83%E3%83%88?src=hash&amp;ref_src=twsrc%5Etfw">#のしろサット</a> では周知が不十分だったようで、制御量を記録していないチームがいくつかあり、2回目の実験までにプログラム修正するよう指導しました。（制御の模式図をつけます） <a href="https://t.co/P16X12WpKn">pic.twitter.com/P16X12WpKn</a></p>&mdash; 平山🛰 (@H_Hirayama) <a href="https://twitter.com/H_Hirayama/status/898943241432702976?ref_src=twsrc%5Etfw">August 19, 2017</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

今回は，単に緯度・経度の観測値をログとして記録してGoogleマップに描画してみます．
最終的に画像のようなCanSatの移動ルートを描画したマップを取得します．

![gps-map](/assets/img/post/get-gps-value-lat-lng-csv/gps_map.png){: width="80%"}
_Googleマップに描画した様子_

緯度・経度の情報をCSVファイルとして出力するためにTeraTermを使用します．
TeraTermを使用して，Arduino IDEのシリアルコンソールと同じようにCOMポートから取得したシリアル通信の内容を表示することができます．
TeraTermは下記からダウンロードしてください．

- [https://ttssh2.osdn.jp/index.html.ja](https://ttssh2.osdn.jp/index.html.ja){:target="_blank"}

## CSVファイル形式（カンマ区切り）のログを出力するプログラム

[緯度と経度を取得しよう]({% post_url 2021-04-09-get-lat-lng-value %}){:target="_blank"}では下記のようなログをシリアルコンソールに出力していました．

```
Lat=  35.700883 Lng=  139.576153
Lat=  35.700883 Lng=  139.576153
Lat=  35.700883 Lng=  139.576153
Lat=  35.700883 Lng=  139.576153
Lat=  35.700883 Lng=  139.576153
Lat=  35.700883 Lng=  139.576153
Lat=  35.700883 Lng=  139.576153
Lat=  35.700883 Lng=  139.576153
```

このままのログでは「Lat=」のような余計な文字が入っていて，CSV形式の出力になっていないため，ソースコードを修正して「緯度の値,経度の値」を出力するようにします．
変更する箇所は，シリアルコンソールに出力している箇所です．

```cpp
Serial.print(gps.location.lat(), 6);
Serial.print(",");
Serial.println(gps.location.lng(), 6);
```

## TeraTermに出力してみる

CanSatをPCに接続してTeraTermを起動します．
「新しい接続」の画面が開くので「シリアル」にチェックを入れてCanSatのポートを選択します．

Arduino IDEのシリアルコンソールにCOMポートを接続しているとbusy状態で接続できない場合があります．
Arduino IDEのシリアルコンソールは閉じておきましょう．

![tera5](/assets/img/post/get-gps-value-lat-lng-csv/gps_teraterm_config5.png){: width="80%"}
_TeraTermの起動_

接続出来たらボーレートを設定します．
メニューの「設定」>「シリアルポート」から設定画面を開きます．
「スピード」を「115200」にしましょう．そのほかの設定はデフォルトのままで大丈夫です．

![tera1](/assets/img/post/get-gps-value-lat-lng-csv/gps_teraterm_config1.png){: width="80%"}
_ボーレートの設定(1)_

![tera2](/assets/img/post/get-gps-value-lat-lng-csv/gps_teraterm_config2.png){: width="80%"}
_ボーレートの設定(2)_

ボーレートを設定したら，TeraTermのコンソール画面にカンマ区切りの緯度・経度が出力されます．
もし何も表示されない場合は，GPSセンサが衛星を補足しているか確認してください．

![tera0](/assets/img/post/get-gps-value-lat-lng-csv/gps_teraterm.png){: width="80%"}
_緯度・経度が出力された様子_

## TeraTermの出力をCSVファイルとして保存する

次に出力された値をCSVファイルとして保存します．
メニューの「ファイル」>「ログ」を開いて，保存場所を選択します．
デフォルトでは`teraterm.log`のようなファイル名になっているので，拡張子をcsvに変更しておきます．
「保存」をクリックするとログの記録が始まります．

![tera4](/assets/img/post/get-gps-value-lat-lng-csv/gps_teraterm_config4.png){: width="80%"}
_ログの保存(1)_

![tera3](/assets/img/post/get-gps-value-lat-lng-csv/gps_teraterm_config3.png){: width="80%"}
_ログの保存(2)_

ログの保存を開始したら，CanSatとPCを持って適当に歩いてみてください．
歩いたルートの緯度・経度が時系列順でCSVファイルとしてログに記録されます．

ある程度ログが取れたら，メニューの「ファイル」>「ログを終了」で記録を終了します．
保存されたCSVファイルを開きます．
うまく保存できていたら1列目が緯度，2列目が経度でカンマで区切られたファイルとなっているはずです．

- [CSVファイルの例]({{ site.url }}/assets/img/post/get-gps-value-lat-lng-csv/teraterm.csv)

```
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
35.700877,139.576142
```

## Googleマップに描画する

最後に緯度・経度を記録したCSVファイルを使ってGoogleマップに移動経路を描画してみます．

ブラウザでGoogleマップを開き，左上のハンバーガーアイコンからメニューを開きます．

![map1](/assets/img/post/get-gps-value-lat-lng-csv/gps_map1.png){: width="80%"}
_Googleマップに描画する(1)_

「マイプレイス」をクリックします

![map2](/assets/img/post/get-gps-value-lat-lng-csv/gps_map2.png){: width="80%"}
_Googleマップに描画する(2)_

「マイマップ」>「地図を作成」をクリックします

![map3](/assets/img/post/get-gps-value-lat-lng-csv/gps_map3.png){: width="80%"}
_Googleマップに描画する(3)_

「インポート」をクリックし，CSVファイルをアップロードします

![map4](/assets/img/post/get-gps-value-lat-lng-csv/gps_map4.png){: width="80%"}
_Googleマップに描画する(4)_

CSVファイルの緯度・経度の列をそれぞれ指定します．マーカのタイトルとして使用する列はどちらでもOKです

![map5](/assets/img/post/get-gps-value-lat-lng-csv/gps_map5.png){: width="80%"}
_Googleマップに描画する(5)_

完了をクリックすると，地図が作成されます

エラーが出る場合は，緯度・経度に指定する列が逆になっていないか確認してください．
