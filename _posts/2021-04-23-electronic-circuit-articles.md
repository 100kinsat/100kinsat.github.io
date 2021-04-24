---
title: 電子回路
author: jjsprings
date: 2021-04-23
categories: [基礎編]
tags: [100kinsat, edusat, tutorial, pcb, 電子回路]
---

## 回路図
---
下画像が100kinsatの回路図全体になります

サイト上で画像が見にくい場合はPDFをDLして参照してください→
[回路図PDF]({{ site.url }}//assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4.pdf)

![回路図1](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4.jpg){: width="40% .normal}



---
##　回路の概要



#### マイコン
cansatの頭脳であり、ここにプログラムが書き込まれ、制御信号などが各素子に出力される。

![回路図_マイコン](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_microcomputer.jpg){: width="40% .normal}

---

#### 電源
スイッチ、レギュレータ、コンデンサ、LEDで構成されている。
電源のON/OFF、電池電圧から適切な電圧への変換、電源ON時のLED点灯などの機能がある
![回路図_電源](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_power.jpg){: width="40% .normal}

---

#### スピーカー
スピーカーである。
![回路図_スピーカー](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_buzzer.jpg){: width="40% .normal}

---

#### スイッチ
動作テストなどに使えるスイッチ
![回路図_SW](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_SW.jpg){: width="40% .normal}

---

#### LED
マイコンから制御して光らせるLED、プログラムで光るパターンを変えるなどできるので、テストにも使える。
![回路図_LED](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_LED.jpg){: width="40% .normal}

---

#### モータードライバ
モーターを動かすためのIC、マイコンからの制御信号に従ってモーターに電流を流す
![回路図_モータードライバ](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_moter_driver.jpg){: width="40% .normal}

---

#### GPS
GPSセンサとつながる端子
![回路図_GPS](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_GPS.jpg){: width="40% .normal}

---

#### 9軸センサ
ジャイロセンサ、加速度センサ、地磁気センサがそれぞれXYZ軸あるので3+3+3軸で9軸センサと呼ばれている。
![回路図_9軸](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_sensor.jpg){: width="40% .normal}

---

#### SDカードスロット
GPS座標や9軸センサのセンサ値や制御ログを保存するためのマイクロSDを指すためのスロットとつながっている。
![回路図_SD](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_SD.jpg){: width="40% .normal}

---

#### 電源
単4電池4本を直列にして電源として利用している。
![回路図_電源](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_power.jpg){: width="40% .normal}

---

#### 電熱線回路
パラシュートを切り離すための電熱線回路
![回路図_電熱線](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_heat.jpg){: width="40% .normal}

---

#### モーターへのコネクタ
モーターと接続するコネクタ
![回路図_モーターコネクタ](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_moter_con.jpg){: width="40% .normal}

---

#### コネクタ・フラグ
上基板と下基板をつなぐコネクタ、配線のフラグ
![回路図_コネクタ](/assets/img/post/electronic-circuit-articles/100kinSAT_ver3.4_con.jpg){: width="40% .normal}

---



