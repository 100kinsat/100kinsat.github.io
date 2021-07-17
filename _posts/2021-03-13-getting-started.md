---
title: 最初に読むページ
author: ymt117
date: 2021-03-13
categories: [CanSatをはじめる前に, はじめに]
tags: [100kinsat, edusat, tutorial, contents]
pin: true
---

<style>
.post-content h2::before {
  font-family: "Font Awesome 5 Free";
  font-weight: 900;
  color: #a9a9a9;
  content: '\f135\0020\0020'; /* https://fontawesome.com/icons/rocket?style=solid */
}
</style>

このWebページは[@_ymt_117](https://twitter.com/_ymt_117){:target="_blank"}が開発した**初心者向けCanSat 100kinSAT（ひゃっきんさっと）**のサポートページです．
「100円ショップで手に入るような安価な部品でつくれるCanSat」をコンセプトに100kinSATと名付けました．
100kinSATやCanSat競技については「[100kinSATとは]({% link _tabs/about.md %}){:target="_blank"}」を読んでください．

100kinSATは部品の購入や開発環境のセットアップなど初学者がつまづきやすいポイントを解決し，ステップバイステップでCanSat開発が行えるように工夫しています．
まずは準備編で部品を揃え，100kinSATを組み立てて開発環境を整えます．
次に基礎編で，モータの制御や各種センサの値の取得方法を学習します．
応用編では目的地への誘導アルゴリズムやログの取り方など，実際の競技で必要な技術を学びます．
また，CanSatの実験を安全に行う方法を学びます．

「CanSat競技に興味はあるけれど，何から始めたら良いかわからない」といった方に100kinSATを使って，学んでもらいたいです．

# 100kinSATとは
---

- [100kinSATとは]({% link _tabs/about.md %}){:target="_blank"}

# 準備編
---

- [基板の入手方法]({% post_url 2021-03-08-get-the-pcb-board %}){:target="_blank"}
- [部品の入手方法]({% post_url 2021-03-09-get-the-electronic-components %}){:target="_blank"}
- [開発環境のセットアップ]({% post_url 2021-03-09-setup-the-development-environment %}){:target="_blank"}
- [基板のはんだ付け]({% post_url 2021-03-09-pcb-soldering %}){:target="_blank"}
- 基板の動作確認

# 基礎編
---

## 構造

- [100kinSATの構成（システム設計）について]({% post_url 2021-05-02-cansat-system-diagram %}){:target="_blank"}

## 電子回路
- [回路図の概要]({% post_url 2021-04-23-electronic-circuit-articles %}){:target="_blank"}

## LED・スイッチ・スピーカー

- [LEDを制御しよう]({% post_url 2021-03-11-board-check %}){:target="_blank"}
- [スイッチの動作確認をしよう]({% post_url 2021-06-07-button %}){:target="_blank"}
- スピーカーを鳴らしてみよう

## モーター

- [モータを制御しよう]({% post_url 2021-03-14-control-motor %}){:target="_blank"}
- [モータの制御プログラムを関数化しよう]({% post_url 2021-04-03-motor-function %}){:target="_blank"}
- [モータの制御プログラムをライブラリ化しよう]({% post_url 2021-04-06-motor-library %}){:target="_blank"}

## GPSセンサ

- [GPSセンサの値を取得しよう]({% post_url 2021-03-28-get-gps-value %}){:target="_blank"}
- [緯度と経度を取得しよう]({% post_url 2021-04-09-get-lat-lng-value %}){:target="_blank"}
- [GPSセンサで取得した位置情報をGoogleマップに描画しよう]({% post_url 2021-04-12-get-lat-lng-value-csv %}){:target="_blank"}

## 9軸センサ

- [9軸センサの値を取得しよう]({% post_url 2021-04-07-get-imu-value %}){:target="_blank"}

## SDカード

- ファイルの読み書きをしよう
- センサの値を記録しよう

## パラシュート

- [パラシュートの作り方]({% post_url 2021-03-13-make-parachute %}){:target="_blank"}

## 電熱線

- 電熱線でパラシュートを切り離そう

## 無線

- WiFiを使って通信しよう
- BLEを使って通信しよう

# 応用編
---

## 9軸センサ

- 地磁気センサで方位を求めよう
- ジャイロセンサでCanSatの進路を補正しよう
- 加速度センサで落下推定をしよう
- [複数のセンサを組み合わせて落下推定しよう]({% post_url 2021-03-13-multiple-sensors %}){:target="_blank"}

## SDカード

- 参照しやすい制御ログを保存しよう
- 制御の状態遷移を記録して，起動時に読み込もう
