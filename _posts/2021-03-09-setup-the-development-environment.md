---
title: 開発環境のセットアップ
author: ymt117
date: 2021-03-09
categories: [CanSatをはじめる前に, 準備編]
tags: [100kinsat, edusat, tutorial, arduino]
---

### 動作環境

|OS|Windows 10|
|:---:|:---:|
|IDE|Arduino IDE ver1.8.X|

### STEP1：Arduino IDEのインストール

STEP1ではArduino IDEのインストールを行います．

[公式サイト](https://www.arduino.cc/en/Main/Software)からインストールファイルをダウンロードします．

![ide1](/assets/img/post/setup-the-development-environment/IDE_install_1.png){: width="50% .normal}

ご自身のOSに合わせたインストーラをクリックします（画像では赤枠で囲ったWindows10向けのインストーラを選択）．

![ide2](/assets/img/post/setup-the-development-environment/IDE_install_2.png){: width="50% .normal}

ダウンロードするだけなら「JUST DOWNLOAD」をクリックします．

![ide3](/assets/img/post/setup-the-development-environment/IDE_install_3.png){: width="50% .normal}

Window10の場合，Microsoft Storeが開くので，「入手」をクリックします．

![ide5](/assets/img/post/setup-the-development-environment/IDE_install_5.png){: width="50% .normal}

ダウンロードが終わったら「起動」をクリックします．

![ide6](/assets/img/post/setup-the-development-environment/IDE_install_6.png){: width="50% .normal}

このときアクセスの許可が求められた場合，「アクセスを許可する」をクリックします．

![ide7](/assets/img/post/setup-the-development-environment/IDE_install_7.png){: width="50% .normal}

Arduino IDEが起動しました！


### STEP2：ESP32開発ボードの環境セットアップ

STEP1でArduino IDEのインストールが完了したと思います．

STEP2では，Arduino IDEの選択ボードにESP32を追加します．

ボードの追加用データはESP32の製造を行っている[Espressif Systems](https://www.espressif.com/)の[GitHubページ](https://github.com/espressif/arduino-esp32)からダウンロードしてきます．

![esp2](/assets/img/post/setup-the-development-environment/esp32_setup_2.png){: width="50% .normal}

まずは追加用のデータをダウンロードします．

「Clone or Download」をクリックして「Download Zip」をクリックするとZipファイルがダウンロードできます．

![esp4](/assets/img/post/setup-the-development-environment/esp32_setup_4.png){: width="50% .normal}

Zipファイルがダウンロードできたフォルダを開いて，Zipファイルを展開してください．

ファイルを展開すると中に複数のファイルがあることを確認できます．

次にダウンロードしたファイルを移動するフォルダを用意します．

Microsoft StoreからArduino IDEをインストールした場合，ドキュメントフォルダに「Arduino」というフォルダがあると思います．

そこに自身で「\hardware\espressif\esp32」とフォルダを作成してください．

ファイルの中身（cores, docs, librariesなど）をコピーして，「C:\Users\ユーザ名\Documents\Arduino\hardware\espressif\esp32\」以下に貼り付けます．

![esp7](/assets/img/post/setup-the-development-environment/esp32_setup_7.png){: width="50% .normal}

上の図のようにファイルを移動できたら，「tools」フォルダをダブルクリックして「tools」フォルダに移動します．

移動したら，「tools」フォルダにある「get.exe」をダブルクリックして実行してください．

![esp9](/assets/img/post/setup-the-development-environment/esp32_setup_9.png){: width="50% .normal}

![uninstall1](/assets/img/post/setup-the-development-environment/IDE_uninstall_1.png){: width="30% .normal}

「Arduino IDE」のところで**右クリック**をすると「アンインストール」の項目が出てきます．

![uninstall2](/assets/img/post/setup-the-development-environment/IDE_uninstall_2.png){: width="30% .normal}

「アンインストール」をクリックして完了です．