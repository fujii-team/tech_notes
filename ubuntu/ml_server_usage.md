# ML server
光工学研究室の機械学習用計算サーバです。
長所は
+ GPUを用いた超並列化計算が可能です。
+ Home ディレクトリをNFSサーバで共有しています。
Jupyter-notebook をブラウザから使うと、
ローカルでの作業とほぼ同等の操作感を実現できます。

短所もあって
+ Home ディレクトリがネットワーク経由のNFSファイルシステムなので、
ストレージへのアクセスが低速です。
基本的には、メモリに載る程度のデータを用いて長時間計算することを想定しています。


# 構成・IPアドレス
ML serverは、データ共有用のNFSサーバと、計算用のGPUサーバからなります。
GPUサーバは随時増やす予定です。

## NFS サーバ ： 10.249.254.52
現状、QnapのNAS（TS-219P）をNFSサーバとして使っています。

## GPUサーバ
### ML-server1: 10.249.254.54
GTX1070を2台積んでいます。

### ML-server2 ： 10.249.254.55
GTX1070を1台積んでいます。

# NFSサーバの使い方
## home ディレクトリの共有
ML server の homeディレクトリを、各自のPCと共有しておくと便利です。
まず、nfsファイルシステムをUbuntuで使えるようにします。
```
sudo apt-get install nfs-common
```

その後、以下のコマンドでML serverのディレクトリを共有できます。
```
sudo mkdir /mnt/ML_home/[username]
sudo mount -t nfs 10.249.254.52:/ML_home/[username] /mnt/ML_home/[username]
```
ここで、`10.249.254.52:/ML_home/[username]` はNFSサーバ内のアドレスで、
`/mnt/ML_home/[username]` は、ローカルマシンのアドレスです。

上記コマンドが成功すると、ローカルマシンの`/mnt/ML_home/[username]`にアクセスすることで、
ML serverのホームディレクトリの内容を閲覧・変更できます。

なお、上記のマウントコマンドはPCの再起動によりリセットされます。
永続的にマウントさせるためには、
`/etc/fstab` の最終行に以下を追加します。
```
# nfs home directory
10.249.254.52:/ML_home/[username] /mnt/ML_home/[username] nfs rw,sync 0 0
```

### リンクの追加
`/mnt/ML_home/[username]` というパスが長すぎて不便な場合は、
リンクを作成しておくと便利です。
例えば
```
ln -s /mnt/ML_home/[username] ~/ml_home
```
とすると、ホームディレクトリ直下の`ml_home`からアクセスすることが可能になります。


# ML server の使い方
## ログイン
基本的には ssh でログインしてください。
ユーザーアカウント・パスワードを伝えますので
```
ssh [username]@10.249.254.54
```
などでアクセスしてください。
パスワードはログイン後に
```
passwd
```
で変更できます。

サーバの状況がどうなっているかわからなくなったら、
ディスプレイ・マウス・キーボードを接続することでGUI環境からでも触れます。


## Anaconda Jupyter の設定
ローカルマシンにインストールしたように、ML serverにもAnacondaをインストールします。
[Anacondaのダウンロードサイト](https://www.continuum.io/downloads)から
Anacondaの最新版のリンクをコピーし、ML server上で
```
cd ~/Downloads
wget https://repo.continuum.io/archive/Anaconda3-4.3.1-Linux-x86_64.sh
chmod +x Anaconda3-4.3.1-Linux-x86_64.sh
./Anaconda3-4.3.1-Linux-x86_64.sh
```
を実行します。
一度ログアウトすることで、Anacondaが使えるようになります。


## Jupyter-notebook server のセットアップ
[参考](http://qiita.com/joemphilips/items/de5d12723b9b88b5b090)

ML server上で
一度 ipython を起動し、
```
from notebook.auth import passwd
passwd()
```
を入力します。パスワードを聞かれるので入力すると、
sha鍵が表示されます。それをコピーしてください。

`~/.jupyter/jupyter_notebook_config.py` ファイルを作成し
```
mkdir ~/.jupyter
nano ~/.jupyter/jupyter_notebook_config.py
```
以下を入力します。
```
c = get_config()

# 全てのIPから接続を許可
c.NotebookApp.ip = '*'
c.NotebookApp.password = u'sha1:bcd259ccf...<先ほどの鍵をコピペ>'
#ブラウザは立ち上げない
c.NotebookApp.open_browser = False

# 特定のポートに指定(デフォルトは8888)
c.NotebookApp.port = 2****
```
最後のポートは各自に割り当てるものです。
ユーザーアカウント作成時に伝えますので、それを入力してください。

最後に、`jupyter-notebook &`でJupyterを起動し、
ローカルマシンのブラウザなどから
```
http://10.249.254.54:/2****
```
でログインできます。
あとはローカルのJupyter-notebookと使い方は同様です。

なお、命令の末尾につける`&` はバックグラウンドで起動することを意味します。
フォアグラウンドに持ってくるためには
```
fg %1
```
（1はジョブ番号）を実行します。

# 応用的な使い方
## 自宅・出先から ML server を利用する
[kuins の ssh ポート転送](http://www.iimc.kyoto-u.ac.jp/ja/services/kuins/vpn/use/sshportforward.html) を用いることで、
自宅などから ML server 上のJupyterを操作することができます。

なお、上記の Jupyter server の設定を各自のPC行っておくことで、
同様に各自のPCも操作できます。

```
ssh -L 2****:10.249.254.54:2**** [ECS-ID/SPS-ID]@forward.kuins.kyoto-u.ac.jp
```
を実行して kuins にログインした後、
ローカルのブラウザを用いて
`localhost:2****` にアクセスするとML server 上のJupyter serverに接続できます。
