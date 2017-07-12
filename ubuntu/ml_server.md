# ML cluster の設定

# NFS server
ip: 10.249.254.52

# ML server
## NFS client のインストール

Home directory を共有するため、NFS client をインストールする。

```bash
sudo apt-get install nfs-common
```

## homeディレクトリを共有する。
以下の元ディレクトリ
+ 10.249.254.52:/ML_home
を `fstab` で `home` に上書き。

> `sudo nano /etc/fstab`  
> Add the following line in /etc/fstab  
> 10.249.254.52:/ML_home /home nfs rw,sync 0 0  

# Install Nvidia Cuda toolkit
([参考](http://qiita.com/tetchi821/items/614ea4ceb4c193e14c6c#cuda%E5%AF%BE%E5%BF%9C%E3%81%AEgpu%E3%81%8C%E3%83%8F%E3%83%BC%E3%83%89%E3%82%A6%E3%82%A7%E3%82%A2%E8%AA%8D%E8%AD%98%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8B%E7%A2%BA%E8%AA%8D))

まず[Nvidiaのサイト](https://developer.nvidia.com/cuda-toolkit) から Cuda toolkit をダウンロードする。

Package Manager Installation を利用する。

<img src=cuda_download.png width=480pt>

> Linux -> x86-64 -> Ubuntu -> 16.04 -> deb(network)

ページ下部のインストラクションに従って
> `sudo dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb`  
> `sudo apt-get update`  
> `sudo apt-get install cuda`  

を実行する。

# CUDNN のインストール
libcudnn を /usr/cuda-8.0 ...  にコピーする


# SSH server のインストール
```
sudo apt-get install ssh-server
sudo ufr allow 22
```

# .bashrc の変更
各自の `.bashrc` ファイルにCuda, Cudnn へのパスを自動で追加するため
/etc/skel/.bashrc の末尾に

```
## CUDA and cuDNN paths
export PATH=/usr/local/cuda-8.0/bin:${PATH}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:${LD_LIBRARY_PATH}
```
を追加する。

ユーザ追加時に`.bashrc`に上記が自動的に追加されるよう、
`/etc/skel/.bashrc` ファイル末尾に上記を記述しておく。

# ユーザの追加
ホームディレクトリは共通だた、ユーザはそれぞれのサーバごとに追加する必要がある。  
追加する際、既存のサーバでの `uid`、ユーザ名が一致するように注意する。

# Monitoring tool munin のインストール
```
sudo apt-get install munin-node
```
