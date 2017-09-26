# cuDNN5 から cuDNN6 へのアップデート
## cuDNN5 のアンインストール
以下のコードで、cuDNN5をアンインストールする
```
cd /usr/local/cuda-8.0/lib64/
sudo rm libcudnn.so  libcudnn.so.5  libcudnn.so.5.1.10  libcudnn_static.a
cd /usr/local/cuda-8.0/include/
sudo rm cudnn.h
sudo ldconfig
```
## cuDNN6のインストール
[nvidiaホームベージ](https://developer.nvidia.com/rdp/cudnn-download)から3つのdebパッケージをダウンロード
- cuDNN v6.0 Runtime Library for Ubuntu16.04 (Deb)
- cuDNN v6.0 Developer Library for Ubuntu16.04 (Deb)
- cuDNN v6.0 Code Samples and User Guide for Ubuntu16.04 (Deb)
ダウンロードしたフォルダで以下のコマンドを実行してインストールする。
```
# Install Runtime library
sudo dpkg -i libcudnn6_6.0*+cuda8.0_amd64.deb
# Install developer library
sudo dpkg -i libcudnn6-dev_6.0*+cuda8.0_amd64.deb
# Install code samples and user guide
sudo dpkg -i libcudnn6-doc_6.0*+cuda8.0_amd64.deb
```
