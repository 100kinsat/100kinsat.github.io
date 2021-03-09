---
title: 基板の入手方法
author: ymt117
date: 2021-03-08
categories: [Tutorial]
tags: [100kinsat, edusat]
---

### はじめに

100kinSATの基板は設計データを中国の企業（[ELECROW](https://www.elecrow.com/)）に発注することで入手できます．注文にはクレジットカードが必要となります．料金は送料込みで10枚2000円ほどかかります．

### STEP1：ガーバデータの入手

まずは基板の発注用データ（ガーバデータ）をダウンロードします．

[こちら](https://github.com/100kinsat/100kinSAT/tree/master/data/Gerver)からガーバデータ（100kinSAT_ver3.X.zip）をダウンロードしてください．

「X」の数字が大きいものが新しいバージョンです．新しいバージョンのデータをインストールしてください．

「Download」をクリックするとダウンロードできます．

ダウンロードが完了したら，一度Zipファイルを解凍して以下の8つのファイルが含まれていることを確認してください
（発注の際，データをアップロードするときはZipファイルのままアップロードします）．

 - 100kinSAT_ver3.X.GBL
 - 100kinSAT_ver3.X.GBO
 - 100kinSAT_ver3.X.GBS
 - 100kinSAT_ver3.X.GML
 - 100kinSAT_ver3.X.GTL
 - 100kinSAT_ver3.X.GTO
 - 100kinSAT_ver3.X.GTS
 - 100kinSAT_ver3.X.TXT

※「X」は任意の数

### STEP2：基板の発注

次に基板の発注を行います．

STEP2では[ELECROW](https://www.elecrow.com/)という会社の基板発注サービスを利用する方法を説明します．

#### 発注の流れ

 1. ログイン（新規の場合は会員登録）
 1. 基板データ（ガーバファイルを圧縮したZipファイル）のアップロード
 1. 発注内容（基板の情報や発送方法）の入力
 1. 発送先住所や支払いの入力
 1. 発注確認メールが届く

![elecrow2](/assets/img/post/get-the-pcb-board/elecrow_2.png){: width="40% .normal}
![elecrow1](/assets/img/post/get-the-pcb-board/elecrow_1.png){: width="40% .normal}

はじめにログインをします．会員登録をしていない場合は，左上の「Join Free」から必要な情報を入力して会員登録をしてください．ログインを完了したら，サイト上部のメニューから「Services」をクリックしてください．

![elecrow3](/assets/img/post/get-the-pcb-board/elecrow_3.png){: width="50% .normal}

サービス一覧のページに移動するので，サービス一覧から「PCB Manufacturing」の「Regular Custom PCB(On-line Ordering)」をクリックします．

![elecrow4](/assets/img/post/get-the-pcb-board/elecrow_4.png){: width="50% .normal}

「ガーバーファイルを提供」と書かれたボタンがあるので，クリックしてSTEP1でダウンロードしたZIPファイルをアップロードしてください．

ZIPファイルのアップロードが完了したら，発注する基板に関する情報を入力していきます．

|項目|入力する内容|備考|
|:---:|:---:|:---:|
|層数|二層| - |
|寸法|100×100| - |
|製造枚数|5|10でもOK(それより多い枚数は値段が上がる)|
|Different PCB Design|1| - |
|板厚|1.6| - |
|レジスト色|Blue|好みの色でOK(PurpleとMatte Blackは値段が上がる)|
|基板の表面処理|HASL| - |
|端面スルーホール|No| - |
|銅箔厚|1oz| - |
|PCBステンシル|No| - |
|生産時間|4-7 working days| - |
|国家|Japan| - |
|運送費用|OCS/ANA Express| - |

![elecrow5](/assets/img/post/get-the-pcb-board/elecrow_5.png){: width="50% .normal}
![elecrow6](/assets/img/post/get-the-pcb-board/elecrow_6.png){: width="50% .normal}
![elecrow7](/assets/img/post/get-the-pcb-board/elecrow_7.png){: width="50% .normal}

### STEP3：基板の受け取り

早ければ1週間ほどで基板が届きます．
2月頃は春節（旧正月）のため製造が遅くなりますので確認してください．