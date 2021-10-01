---
title: 基板の設計ミスと修正に関して
author: ymt117
date: 2021-10-01
categories: [その他]
tags: [100kinsat, edusat, v1.0.0]
---

# はじめに

エデュサットの基板にはGPSセンサの回路に関して，設計ミスがあります．
そのため，乾電池によるバッテリー駆動ではGPSセンサが動作しません．
（一方でUSBケーブルでPCと接続しているときは動作します）

ここでは設計ミスの内容と基板の修正方法に関して説明します．

※修正が必要な基板は，基板上のシルクで「100kinSAT_ver3.4」と記載されているものが対象です．

![edusat](/assets/img/post/fix-circuit-board/edusat.jpg){: width="50% .normal}
_修正対象の基板_

# GPSセンサの回路設計ミスについて

エデュサットに搭載しているGPSセンサは5Vで駆動します．
USBケーブルでPCとESPマイコンを接続しているときは，PCから5Vが供給されているためGPSセンサは動作します．

しかしながら，乾電池から供給する際は約6V（=乾電池4本）の電圧を三端子レギュレータを介して3.3Vにして供給しています．
そのため，GPSセンサに5Vの電圧が供給されず，動作しない設計ミスがあります．

![gps](/assets/img/post/fix-circuit-board/gps.jpg){: width="50% .normal}
_回路の接続関係のイメージ図_

# 修正方法

バッテリ（乾電池）から三端子レギュレータを介さず，ESPマイコンの5V端子に接続するようにジャンパしてあげることで修正できます．

具体的には，下記画像のように三端子レギュレータの入力側とESPマイコンの5V端子を接続します．

![fix](/assets/img/post/fix-circuit-board/image0.jpg){: width="50% .normal}
_修正した基板_

この修正によって，ESPマイコンの5V端子に約6V（=乾電池4本）の電圧が供給されます．
エデュサットの基板上でESPマイコンの5V端子は，GPSセンサの5V端子と繋がっているので，GPSセンサにも6Vの電圧が供給されるのでバッテリ駆動で動作するようになります．

5V端子に6Vを供給して問題ないかという点に関して少し説明します．

ESPマイコンの5V端子は内部で「AMS1117-3.3」というレギュレータに接続されていて，このICを介してESPマイコン本体に3.3Vを供給しています．
そして，このICは最大電圧15Vまで印加可能なため，6Vの電源を接続しても問題ありません．

また，GPSセンサにも6Vの電圧が供給されますが，GPSセンサには「XC6216P332PR-G」というレギュレータが接続されていて，このICは10Vまでの入力が可能なため問題ありません．

バッテリのスイッチをONにした状態でPCとESPマイコンを接続した場合は，ESPマイコンに搭載されているショットキーバリアダイオードがPCのUSB端子側へ不正に電流が流れることを防ぎます．