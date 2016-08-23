# ScanSnap S1300i by Fujitsu を Ubuntu 16.04　で使う。

## Reference
http://www.openfusion.net/linux/scansnap_1300i


## 準備
`sane`と`gscan2pdf`をインストールしておく。

`sudo apt-get install sane gscan2pdf`


## Scannerの検出
USBケーブルでUbuntuに接続し、スキャナの電源を入れる。
> `sudo sane-find-scanner`

を実行し、S1300iが検出されていることを確認する。以下のように表示されればOKである。
> found USB scanner (vendor=0x04c5 [FUJITSU], product=0x128d [ScanSnap S1300i]) at libusb:002:012

## Firmwareのダウンロード
Windows用ファームウェアに同梱されている`nal`ファイルをダウンロードする。

`C:/Windows`らへんにあるようだが、現在では以下に同様のものがアップロードされている。

+ 300_0C00.nal ( http://www.openfusion.net/public/files/300_0C00.nal )
+ 1100_0A00.nal ( http://www.openfusion.net/public/files/1100_0A00.nal )
+ 1300_0C26.nal ( http://www.openfusion.net/public/files/1300_0C26.nal )
+ 1300i_0D12.nal ( http://www.openfusion.net/public/files/1300i_0D12.nal )

これらのファイルを、`/usr/share/sane/epjitsu/`内にコピーする。
> `sudo mkdir /usr/share/sane/epjitsu`

> `cp *.nal /usr/share/sane/epjitsu/`

## sane.d設定ファイル
`/etc/sane.d/epjitsu` が以下の内容が含まれていることを確認する。
> `# Fujitsu S1300i`

> `firmware /usr/share/sane/epjitsu/1300i_0D12.nal`

> `usb 0x04c5 0x128d`

ここで`usb`の行は、
> `sudo sane-find-scanner`

で確認した内容と一致する必要がある。

## ドライバの確認
（念の為）スキャナの電源を入れなおして、
> `sudo scanimage -L`

を実行し、スキャナが起動することを確認する。
> `$ sudo scanimage -L`

> `device 'epjitsu:libusb:001:014' is a FUJITSU ScanSnap S1300i scanner`


## gscan2pdfの起動
http://www.openfusion.net/linux/scansnap_1300i

と異なり、私の環境では単純に`gscan2pdf`を起動するだけでスキャンを実施できた。
