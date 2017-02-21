# Ubuntuでのキーアサイン
[参考](http://symfoware.blog68.fc2.com/blog-entry-1873.html)

Ubuntu 16.04 でキーアサインをカスタマイズするために
**窓使いの憂鬱** というソフトウェアを愛用しています。

主な設定項目は
+ 「変換」「無変換」キーを利用したカーソル移動
+ 「Caps Lock」を「Ctrl」に変更
などです。

ホームポジションから手を移動させずにキーボード操作を全て行うことを目指しました。

## インストール方法

大まかな手順は

1. 必要なライブラリをインストール
2. ソースをダウンロードして展開・インストール
3. 設定ファイルの登録
4. スタートアップに登録

です。

### 必要なライブラリをインストール
```
$ sudo apt-get install libudev-dev
$ sudo apt-get install libusb-1.0-0-dev
$ sudo apt-get install libboost-dev
$ sudo apt-get install libboost-iostreams-dev
```

### ソースをダウンロードして展開
元は `http://www42.tok2.com/home/negidakude/downdata/mayu-0.12.1.tar.gz`
にあったようですが、現在なくなっています。
現在は
[こちら](https://github.com/kenhys/mayu)からダウンロードできます。

```
git https://github.com/kenhys/mayu clone
cd mayu.github
$ sudo ./configure --with-boost-libdir=/usr/lib/x86_64-linux-gnu/
$ sudo make
$ sudo make install
```

### 設定ファイルの作成
私が使っている設定ファイルは[こちら](config_files/.mayu)にあります。  
主な設定は

+ カーソル移動
  + 変換 + i : ↑
  + 変換 + j : ←
  + 変換 + k : ↓
  + 変換 + l : →
  + 無変換 + i : Page up
  + 無変換 + j : Home
  + 無変換 + k : Page down
  + 無変換 + l : End

+ 決定・削除
  + CapsLock : Ctrl
  + Ctrl + Space : Back space
  + 変換 + Space : Enter


### Ubuntuのスタートアップに登録
[参考](http://symfoware.blog68.fc2.com/blog-entry-1938.html)
