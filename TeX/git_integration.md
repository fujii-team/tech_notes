# Git との組み合わせ

**laTeX 環境の構築** については[こちら](get_started.md)を参考のこと。

## gitを用いてバージョン管理する。
TeXはいろいろな中間ファイルを吐き出すので、それを無視する`.gitignore`ファイルを作成する。  
[このファイル](gitignore)の名前を`.gitignore`に変更し、リポジトリの最上階層に保存する。  
その他、git管理したくないファイルがあれば、同様に`.gitignore`ファイルに記述しておくとよい。

# git-latexdiff
laTexには`latexdiff`という差分を表示する仕組みがある。
それを簡単に使うためのスクリプト[`git-latexdiff`](git-latexdiff)を用意した。

## 環境構築
### latexdiffのインストール
latex ファイルの差分を抽出するlatexdiffを用いる。
PCにインストールされていない場合は、それをインストールしておく。  
> sudo apt-get install latexdiff

### git-latexdiffの準備
この`git-latexdiff`を[laTeX 環境の構築](get_started.md)で用意した`latexmkrc`と
同じパスに置く。

## 差分の表示
以下のようにすると、ディレクトリ内にdiff.pdfが作成される。
このdiff.pdfファイルには、修正前のものが小さな赤字で、修正後のものがボールドの青字で示されており、
変更点がわかりやすくなっている。


### 現在のファイルと直前のコミットとの差分を表示する。
ターミナルから`./git-latexdiff`を実行する。  
> Permission denied  

と表示される場合は、`chmod +x git-latexdiff` などとして、ファイルの実行を許可する。


### 指定したブランチと現在のファイルの差分を表示する。
ターミナルから`./git-latexdiff ブランチ名`を実行する。  
例えば、master ブランチ内のファイルとの差分を表示したければ、
`./git-latexdiff master`
を実行する。  

### 指定したコミットと現在のファイルの差分を表示する。
ターミナルから`./git-latexdiff {SHA-id}`を実行する。   
なお、SHA-id はコミットに紐付けられた id で各種ツールから確認できる。  
例えば、0198fe0f というSHA-idを持つコミットとの差分を表示したければ  
`./git-latexdiff 0198fe0f`  
を実行する。  

### 指定した２つのブランチ間の差分を表示する。
ターミナルから`./git-latexdiff 新ブランチ名 旧ブランチ名`を実行する。  
同様に、ディレクトリ内にdiff.pdfが作成される。

なお前項と同様に、ブランチ名の代わりに 特定のコミットのSHA-idを指定してもよい。  
その場合は、指定した2つのコミット間での差分を表示することになる。
