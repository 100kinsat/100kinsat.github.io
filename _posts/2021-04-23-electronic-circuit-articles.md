---
title: 回路図の概要
author: jjsprings
date: 2021-04-23
categories: [基礎編]
tags: [100kinsat, edusat, tutorial, pcb, 電子回路]
---

## 回路図
---
下画像が100kinsatの回路図全体になります

サイト上で画像が見にくい場合はPDFをDLして参照してください→
[回路図PDF]({{ site.url }}/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4.pdf)

![回路図1](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4.jpg){: width="40% .normal}



---
## 回路の概要



#### マイコン
cansatの頭脳です、ここにプログラムを書き込むことで制御信号などを各素子に出力したり、センサーからの値を処理したりします。

![回路図_マイコン](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_microcomputer.jpg){: width="40% .normal}

---

#### 電源
スイッチ、レギュレータ、コンデンサ、LEDで構成されています。
電源のON/OFF、電池電圧から適切な電圧への降圧、電源ON時のLED点灯などの機能があります。
![回路図_電源](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_power.jpg){: width="40% .normal}

---

#### スピーカー
スピーカーです。
起動音を鳴らしたり、プログラム状況で特定の音を出すことででバックに利用します。
![回路図_スピーカー](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_buzzer.jpg){: width="40% .normal}

---

#### スイッチ
動作テストなどに使えるスイッチです。
プッシュスイッチはプログラム遷移など外部入力に使うことを想定しています。
フライトピンは放出検知等での利用を想定しています。

![回路図_SW](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_SW.jpg){: width="40% .normal}

---

#### LED
マイコンから制御して光らせるLEDです。
マイコンからLEDを光らせることは電子工作の世界では「Lチカ」と呼ばれ、プログラミングの「Hello, world!」に対応する一番初めの登竜門です。

LEDの光るスピードやパターンをプログラムから変えることができるので、デバッグにも使うことができます。
![回路図_LED](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_LED.jpg){: width="40% .normal}

---

#### モータードライバ
モーターを動かすためのICです。
モーターは大電流を必要とするためこのようなICが必要となります。
マイコンからの制御信号に従ってモーターに電流を流します。
![回路図_モータードライバ](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_moter_driver.jpg){: width="40% .normal}

---

#### GPS
GPSセンサとつながる端子です。
GPSセンサーから自分の緯度経度などを知ることで制御を行います。
![回路図_GPS](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_GPS.jpg){: width="40% .normal}

---

#### 9軸センサ
ジャイロセンサ、加速度センサ、地磁気センサがそれぞれXYZの3軸あるので3+3+3軸で9軸センサと呼ばれています。
GPSセンサーだけでは、自分が向いている方向が分からないため、地磁気センサで方位を求める等の方法で自分が向いている方向を知ることができます。
その他にもセンサー値から様々な制御を考えることができます。

![回路図_9軸](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_sensor.jpg){: width="40% .normal}

---

#### SDカードスロット
GPSから求めた座標や9軸センサの値、制御ログを保存するためにマイクロSDを使用します。

![回路図_SD](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_SD.jpg){: width="40% .normal}

---

#### 電源
単4電池4本を直列にして電源として利用しています。
![回路図_電源](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_bat.jpg){: width="40% .normal}

---

#### 電熱線回路
パラシュートを切り離しに利用することを想定した電熱線回路です。
電熱線の熱でテグス等の熱に弱い素材を焼き切りパラシュートと機体の切り離しを行います。

![回路図_電熱線](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_heat.jpg){: width="40% .normal}

---

#### モーターへのコネクタ
モーターと接続するコネクタです。
![回路図_モーターコネクタ](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_moter_con.jpg){: width="40% .normal}

---

#### コネクタ・フラグ
上基板と下基板をつなぐコネクタです。
配線のフラグは回路図を成立させるうえで必要となるフラグです。
![回路図_コネクタ](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_con.jpg){: width="40% .normal}

---



