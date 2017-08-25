# NFS サーバ ： 10.249.254.52
光工学研究室で用いるLHDデータは、NFSサーバの`/ML_home/public` に蓄えられています。ここにあるデータをローカルマシンでロードするために、NFSサーバのhomeディレクトリを各自のPCと共有します。

# NFS サーバのマウント方法
まず、nfsファイルシステムをUbuntuで使えるようにします。
```
sudo apt-get install nfs-common
```

その後、以下のコマンドでML serverのディレクトリを共有できます。
```
sudo mkdir /mnt/ML_home/public
sudo mount -t nfs 10.249.254.52:/ML_home/public /mnt/ML_home/public
```
ここで、`10.249.254.52:/ML_home/public` はNFSサーバ内のアドレスで、
`/mnt/ML_home/public` は、ローカルマシンのアドレスです。

上記コマンドが成功すると、ローカルマシンの`/mnt/ML_home/public`にアクセスすることで、
ML serverのホームディレクトリの内容を閲覧・変更できます。

なお、上記のマウントコマンドはPCの再起動によりリセットされます。
永続的にマウントさせるために、`/etc/fstab` を編集します。
このファイルはrootによる制限がかかっているため、
以下のコマンドにより、root権限でテキストエディタgeditを開きます。
```
sudo gedit /etc/fstab
```
開いたファイルの最終行に以下を追加し、保存します。
```
# nfs home directory
10.249.254.52:/ML_home/public /mnt/ML_home/public nfs rw,sync 0 0
```
