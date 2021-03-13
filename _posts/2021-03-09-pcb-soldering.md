---
title: 基板のはんだ付け
author: ymt117
date: 2021-03-09
categories: [CanSatをはじめる前に, 準備編]
tags: [100kinsat, edusat]
---

<style>
r { color: Red }
</style>

### 準備するもの

![handa1](/assets/img/post/pcb-soldering/handa1.jpg){: width="50% .normal}
![handa2](/assets/img/post/pcb-soldering/handa2.jpg){: width="50% .normal}

　はんだ付けに必要な道具と電子部品を準備します．ここでは，はんだ付けに必要な道具について説明します．必要な電子部品については[部品の入手方法]({% post_url 2021-03-09-get-the-electronic-components %})のページを参考にしてください．

　はんだ付けに必要な道具(上記写真左側)を以下に示します．

 - はんだごて
 - こて台
 - はんだ
 - ニッパー
 - ラジオペンチ
 - はんだ吸い取り器
 - ピンセット
 - マスキングテープ

 はんだごては[温度調整できるもの](https://www.amazon.co.jp/dp/B006MQD7M4/ref=twister_B076PDQJYS?_encoding=UTF8&psc=1)がおすすめです．また，こて先を標準のものではなく，[熱容量の大きいこて先](https://www.amazon.co.jp/gp/product/B00744EHRW/ref=oh_aui_search_asin_title?ie=UTF8&psc=1)に交換するとはんだ付けが楽になります．

 はんだは電子工作用と書かれたものであれば問題ないです．太さは0.3～0.8㎜くらいのものが適当です．ニッパーとラジオペンチ，ピンセットはホームセンターで購入できます．

[はんだ吸い取り器](https://www.amazon.co.jp/gp/product/B0016V5KHU/ref=oh_aui_search_asin_title?ie=UTF8&psc=1)ははんだ付けに失敗したときに使います．マスキングテープは電子部品を仮固定する用途で使います．

### 部品リスト

部品リストは[こちらのエクセルファイル]({{ site.url }}/assets/img/post/pcb-soldering/100kinSAT_ver3.4_BOM.xlsx)を参考にしてください．リファレンスの列に記載されている「SP1」などの番号が基板上に印刷されている番号と対応します．

![bom1](/assets/img/post/pcb-soldering/bom1.png){: width="50% .normal}
![bom2](/assets/img/post/pcb-soldering/bom2.jpg){: width="50% .normal}

### はんだ付けの順番

　はんだ付けを行う際は，背の低い部品からはんだ付けを行うと基板がガタつくことが少なくはんだ付けしやすくなります．具体的には，背の低い抵抗やダイオードなどからはんだ付けしていき，最後にレギュレータやスピーカなどをはんだ付けするようにします．

![handa3](/assets/img/post/pcb-soldering/handa3.jpg){: width="50% .normal}


　また，注意点として**ESP32マイコンボードは裏面のモータドライバと抵抗をはんだ付けしてから実装してください．**
先にESPマイコンを実装してしまうと，モータドライバと抵抗のはんだ付け面が隠れてしまい実装できなくなります．

### 抵抗のはんだ付け

### 注意が必要な部品と回路のミスについて

　極性(プラスとマイナスの向き)がある電子部品は注意が必要です．基板に印字されている記号と照らし合わせて正しい向きになるようにはんだ付けしてください．以下は100kinSATにおいて極性がある部品の一覧です．

 - ダイオード
 - LED
 - 極性のあるコンデンサ
 - 乾電池ホルダー

　また，トランジスタや3端子レギュレータ等の向きを間違えていないか注意してください．「U1」(リレー)はとくに向きがありません．

　基本的に部品はシルク(基板上の白い線で描かれた図形)がある面に部品がくるようにはんだ付けしてください．しかし，「P8」(ピンソケット)だけはミスでシルクが実装面と反対の面にあるため，<r>「P8」に関してはシルクと反対の面になるように実装してください．</r>