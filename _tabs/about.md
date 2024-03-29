---
title: 100kinSATとは
icon: fas fa-info
order: 4
---

<style>
r { color: Red }
b { color: Blue}
</style>

## はじめに
---

CanSat（カンサット）は「<b>Can</b>（缶）」と「<b>Sat</b>ellite（サテライト、衛星）」を組み合わせた造語で、CanSatと呼ばれる小型模擬人工衛星による惑星探査を模した競技です。

CanSatの製作を通して、実際の宇宙開発で行われているような衛星モデルの開発を学ぶことができます。
100kinSATは、衛星モデルの開発を学ぶCanSat競技の初心者向け開発キットです。種子島ロケットコンテストなど国内のCanSatコンペのレギュレーションを満たした設計となっています。

「100円ショップで手に入るような安価な部品でつくれるCanSat」をコンセプトに100kinSATと名付けています。

![cansat](/assets/img/about/cansat_v3.4.jpg){: width="50% .normal}
_100kinSAT ver3.4[^caution]_

## 競技ルール（カムバックコンペ）
---

CanSatは主にローバ方式（走行してゴールへ向かう方式）とフライバック方式（飛行してゴールへ向かう方式）の2つの方式があります。 ここではローバ方式について説明します。

CanSatはロケットや気球、ドローンに搭載されて上空に打ち上げて投下されます。 例として種子島ロケットコンテストでは、主に気球で50mほどの高さから投下します。 投下されたCanSatはパラシュート等の減速機構を用いて軟着陸します。 その後、パラシュートを切り離して、センサ（GPSや加速度センサ、カメラ）の値をもとに自律走行であらかじめ決められた目標地点に走行します。

目標地点との到達距離や到達時間を競います。 競技中、CanSatは自律制御で動作します。 そのため、ダウンリンク（CanSatから地上局（パソコン等）へ情報を送ること）はできますが、アップリンク（地上局からCanSatへ情報を送ること）はできません。

![sequential](/assets/img/about/sequential.png){: width="50% .normal}
_競技のシーケンス図_

## 100kinSATで学べること
---

- 衛星モデルの開発フロー
- 宇宙開発の面白さや難しさ
- 電子回路やセンサの扱い
- ロボット制御プログラミング
- ...

## 主なCanSatコンペティション
---

- 種子島ロケットコンテスト
- 能代宇宙イベント
- 缶サット甲子園

## 100kinSATの利用について
---

- 100kinSATを利用する際は、クレジット表記（100kinSAT）をしていただけるとありがたいです。
- ぜひ個人利用や授業等に活用してください（利用するときにメール等で連絡していただけると嬉しいです）。
- 100kinSATに関して、改変や営利目的での二次利用は自由に行っていただいて構いません。
- 100kinSATに関するリポジトリに記載している内容において、利用者が行う一切の行為について、開発者はいかなる責任も負いません。
- 100kinSATの制御に使用している外部ライブラリ等に関しては配布元のライセンスに従ってください。

## 連絡先
---

質問等あれば、twitter（@_ymt_117）もしくはgmail（yamamto117`<at>`gmail.com）に連絡ください。（「`<at>`」は「@」に書き換えてください）

## 注意点
---

[^caution]: 100kinSAT ver3.4は電熱線に使用しているIOピン（P15）がデフォルトでHIGHになってしまいます。そのため、ニクロム線をターミナルブロックに接続したまま電熱線以外の実験を行う場合は、意図せずにニクロム線が熱くなってしまい大変危険です。<r>プログラムの方で電熱線のIOピンをLOW（setup関数内でdigitalWrite(15, LOW);）にしてください。</r>