# SmartGitのダウンロード

プログラムコードのバージョン管理・共有は **(Git)[https://ja.wikipedia.org/wiki/Git]**
で行なうほうがよい。

少し難しいシステムなので、

http://koseki.hatenablog.com/entry/2014/04/22/inside-git-1

http://www.find-job.net/startup/7-git-slides

など、仕組みや使い方を調べておくこと。

まず、gitをインストールする。
```bash
sudo apt-get install git
```

**git** は基本的にコマンドラインで実行するソフトウェアだが、直感的でないので、
GUIアプリケーションであるSmartGitを導入する。


http://www.syntevo.com/smartgit/download

からSmartGitをダウンロードする。

<img src=SmartGit_download.png width=480pt>


## 解凍
Smartgitは特にインストールを必要としないソフトウェアなので、
実行ファイル等を格納するフォルダを作成しておく。
ここでは、ホームディレクトリ直下の`tools`ディレクトリに格納することにする。

```bash
mkdir ~/tools
```

ダウンロードしたファイルを`tools`ディレクトリに移動させ
```bash
mv ~/Download/smartgit-linux-7_1_2.tar.gz
```

Linux で圧縮ファイルを解答するには、以下を実行する。
```bash
tar -xvf ~/tools/smartgit-linux-7_1_2.tar.gz
```

<img src=SmartGit_unzip.png width=480pt>

## 実行の確認
Smartgitが無事実行できるかどうか確認する。
```bash
~/tools/smartgit/bin/smartgit.sh
```

```
Error: No java environment found (JRE 1.8 or higher required).
```
と言われる場合は、
PCにJava実行環境が入っていないことによってsmartgitが起動できないことを示している。
その場合は
```bash
sudo apt-get install default-jre
```
によってJava実行環境をインストールする。

実行できることが確認できれば、smartgit をスタートメニューに登録しておく。
```bash
~/tools/smartgit/bin/add-menuitem.sh
```
