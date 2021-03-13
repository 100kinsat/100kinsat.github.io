---
title: 複数のセンサを組み合わせる
author: ymt117
date: 2021-03-13
categories: [CanSatをはじめよう, 応用編]
tags: [100kinsat, edusat]
---

# 安全な設計思想とは

ものづくりを行う上で安全管理は非常に重要です．たとえば，CanSatを上空から放出したときに着地判定を誤ってしまうとパラシュートを上空で切り離すことになり大変危険です．

ここでは，安全な設計について説明します．

### 複数のセンサを組み合わせたシステム開発

CanSatの落下判定におけるポイントは以下の2つです．

 - 落下中にパラシュートを切り離さない
 - 着地したら確実にパラシュートを切り離す

このような着地判定をするためには複数のセンサを組み合わせたシステム開発が必要になります．100kinSATに搭載されている(1)フライトピン，(2)加速度センサ，(3)タイマーの3つを組み合わせた場合について考えていきましょう．

フライトピンは，CanSatがロケットやパラシュートから放出された際の衝撃でピンが外れることで放出を検知する仕組みになっています．フライトピンが外れたことを検知しただけではCanSatがまだ上空にいるのか，着地したのか分かりません．

![flightPin](/assets/img/post/multiple-sensors/flightPin.png){: width="50% .normal}

加速度センサはCanSatにかかる加速度を検知します．落下中のCanSatは大きく揺れている状態になるので加速度センサの値も大きく変化します．一方で，着地したCanSatは地面で静止している状態になるので加速度センサの値の変化は小さくなります．このような加速度センサの値の変化量をみることで，CanSatが落下中なのか着地しているのか判断することができます．

![acc](/assets/img/post/multiple-sensors/acceleration.png){: width="50% .normal}

しかし，着地したあとパラシュートを切り離す前のCanSatは風の影響を受けて大きく動く可能性があります．その場合，着地していたとしても加速度センサの値の変化は大きくなり，地面で静止している状態であるのかどうか判断することができません．

そこでタイマーを使います．「競技開始から一定時間経過していたら確実に地面に着地しているはず」という時間を設定しておくことで，一定時間経過したら着地と判定することができます．タイマーによる判定は最終手段ですが，このようにフライトピンや加速度センサで判断できない場合にタイマーを使うことで空中でパラシュートを切り離してしまう危険性を少なくすることができます．