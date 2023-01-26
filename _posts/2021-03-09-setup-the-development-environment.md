---
title: 開発環境のセットアップ
author: ymt117
date: 2021-03-09
last_modified_at: 2021-07-29
categories: [CanSatをはじめる前に, 準備編]
tags: [100kinsat, edusat, tutorial, arduino]
---

## 動作環境
---

|OS|Windows 10|
|:---:|:---:|
|IDE|Arduino IDE ver1.8.X|

## STEP1：Arduino IDEのインストール
---

STEP1ではArduino IDEのインストールを行います。

[公式サイト](https://www.arduino.cc/en/Main/Software)からインストールファイルをダウンロードします。

ご自身のOSに合わせたインストーラをクリックします（画像では赤枠で囲ったWindows10向けのインストーラを選択）。

![ide1](/assets/img/post/setup-the-development-environment/IDE_install_1.png){: width="50% .normal}
_公式サイトから自分のPCのOSに応じてダウンロードする_

ダウンロードするだけなら「JUST DOWNLOAD」をクリックします。

![ide2](/assets/img/post/setup-the-development-environment/IDE_install_2.png){: width="50% .normal}
_公式サイトのダウンロード画面_

Window10の場合、Microsoft Storeが開くので、「入手」をクリックします。

![ide3](/assets/img/post/setup-the-development-environment/IDE_install_3.png){: width="50% .normal}
_Microsoft Storeのダウンロード画面_

ダウンロードが終わったら「起動」をクリックします。

![ide5](/assets/img/post/setup-the-development-environment/IDE_install_5.png){: width="50% .normal}
_Mirosoft Storeからダウンロードした場合の画面_

このときアクセスの許可が求められた場合、「アクセスを許可する」をクリックします。

![ide6](/assets/img/post/setup-the-development-environment/IDE_install_6.png){: width="50% .normal}
_アクセスの許可を求められたときの画面_

Arduino IDEが起動しました！

![ide7](/assets/img/post/setup-the-development-environment/IDE_install_7.png){: width="50% .normal}
_Arduino IDEの画面_

## STEP2：ESP32開発ボードの環境セットアップ
---

STEP1でArduino IDEのインストールが完了したと思います。

STEP2では、Arduino IDEの選択ボードにESP32を追加します。

以下のリポジトリにアクセスしてください。

[https://github.com/espressif/arduino-esp32](https://github.com/espressif/arduino-esp32){:target="_blank"}

READMEに記載されているJSONファイルのパスをコピーします。

![esp3](/assets/img/post/setup-the-development-environment/arduino3.png){: width="50% .normal}
_JSONファイルのパスをコピーする_

Arduino IDEの「ファイル」>「環境設定」を開きます。

![esp4](/assets/img/post/setup-the-development-environment/arduino4.png){: width="50% .normal}
_環境設定を開く_

環境設定の画面を開いたら、「追加のボードマネージャのURL」欄に先ほどコピーしたJSONファイルのURLを貼り付けます。

![esp5](/assets/img/post/setup-the-development-environment/arduino5.png){: width="50% .normal}
_環境設定の画面_

次に「ツール」>「ボード」>「ボードマネージャ」を開きます。

![esp6](/assets/img/post/setup-the-development-environment/arduino6.png){: width="50% .normal}
_ボードマネージャを開く_

検索窓に「esp32」と入力するとesp32用のボードのパッケージが表示されます。

「インストール」をクリックしてボードのパッケージをインストールします。

![esp7](/assets/img/post/setup-the-development-environment/arduino7.png){: width="50% .normal}
_ボードのパッケージをインストールする_

インストールが完了すると、「ツール」>「ボード」にesp32のボードが追加されていることが確認できます。

![esp8](/assets/img/post/setup-the-development-environment/arduino8.png){: width="50% .normal}
_ボードが追加されていることを確認_

100kinSATの開発では「ESP32 Dev Module」のボードに設定します。

![esp9](/assets/img/post/setup-the-development-environment/arduino9.png){: width="50% .normal}
_環境設定を開く_

ボードの設定を「ESP32 Dev Module」にすると「ファイル」>「スケッチ例」にESP32 Dev Module用のスケッチ例が表示されるようになります。

![esp10](/assets/img/post/setup-the-development-environment/arduino10.png){: width="50% .normal}
_環境設定を開く_

これで開発環境のセットアップは完了です。
