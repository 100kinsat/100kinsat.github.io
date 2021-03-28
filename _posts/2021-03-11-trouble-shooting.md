---
title: トラブルシューティング
author: ymt117
date: 2021-03-11
categories: [その他, トラブルシューティング]
tags: [100kinsat, edusat, other, trouble shooting]
---

# 基板に電源が入らない

電池ボックスには電池の極性に合わせた向きがあります．
プラスとマイナスが逆になっていないか確認してください．

はんだづけがしっかりできていない場合があります．
テスターを使って各端子の導通チェックをしてみてください．

# コンパイルエラーが出た

コンパイルエラーとなっている場合は，エラーメッセージに解決のヒントがあります．
まずはエラーメッセージに書いてある内容を確認してください．
エラーメッセージをWebで検索すると解決策が見つかることもあります．

よくあるミスは，プログラムのスペルミス等です．

# プログラムの書き込みができない

### マイコンとPCが接続されているか

マイコンとPCがUSBケーブルで接続されているか確認してください．接続されている場合，PCにマイコンがCOMポートとして認識されているか確認します．

また，ケーブルが断線している場合や信号線がないケーブルの場合もあります．
別のケーブルに変えてみる等してください．

マイコンのリセットボタンが押されたままになっていると書き込みできる状態になりません．
ESP32マイコンのボード上で「EN」という文字が書かれた箇所にあるタクトスイッチはリセットボタンです．
このボタンを何回か押してみると解消することがあります．

### COMポートにチェックが入っているか

Arduino IDEのメニューからCOMポートを選択しているか確認してください．

### ボードの選択は合っているか

Arduino IDEのメニューからボードが正しく選択されているか確認してください．

# COMポートが表示されない

COMポートが表示されない場合は，ESPマイコンをCOMポートとして認識するためにデバイスドライバがPCにインストールされていない可能性があります．Windowsの場合「デバイスマネージャ」を開いて確認してください．

![cp1](/assets/img/post/trouble-shooting/cp201driver1.png){: width="50% .normal}

　画像のように「ほかのデバイス」となっている場合，COMポートとして認識できていません．下記URLにアクセスしてご自身のOSに合ったデバイスドライバをダウンロードしてください．ここではWindows10の場合を例に説明します．Windows10の場合は，下の画像のような「Windows 10 Universal VCPをダウンロード」をクリックしてZIPファイルをダウンロードしてください．

[https://jp.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers](https://jp.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

![cp3](/assets/img/post/trouble-shooting/cp201driver3.png){: width="50% .normal}
　

　ダウンロードできたらZIPファイル「CP210x_Universal_Windows_Driver」を解凍（展開）します．64ビットのWindowsを使用している場合は，展開したフォルダの中にある「CP210xVCPInstaller_x64.exe」ファイル（インストーラ）を実行します．32ビットのWindowsを使用している場合は，展開したフォルダの中にある「CP210xVCPInstaller_x86.exe」ファイルを実行します．最近のPCは，ほとんどが64ビットなのでわからない場合は「CP210xVCPInstaller_x64.exe」を実行すれば良いでしょう．

![cp4](/assets/img/post/trouble-shooting/cp201driver4.png){: width="50% .normal}

　インストールが終わったら，再び100kinSATをUSBポートに挿して「デバイスマネージャ」を開いて確認してください．画像のようにCOMポートとして認識できていればOKです．（画像ではCOM5となっていますが，この「5」という数字は使っているPCによって変わることがあります）

![cp2](/assets/img/post/trouble-shooting/cp201driver2.png){: width="50% .normal}


# シリアルコンソールに文字が表示されない/文字化けする

　シリアルコンソールに文字が表示されない/文字化けするという場合は，シリアル通信のボーレートが適切に設定できていない可能性があります．ボーレートはプログラム中の `setup関数` で設定していると思います． `Serial.begin(9600);` の場合はボーレートは9600bpsです．

　プログラム中で設定しているボーレートを確認したら，シリアルコンソールのボーレートをその数値に合わせてください（画像参照）．

![bps](/assets/img/post/trouble-shooting/bps.png){: width="50% .normal}