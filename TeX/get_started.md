# TeX 環境の構築

Ubuntu 16.04 64bit での TeX環境の構築について述べる。

**[gitとの組み合わせについてはこちら](git_integration.md)**を参考にすること。

# ソフトウェアのインストール
## TeXLive のインストール

TeX のソースコードを文書へ変換するソフトウェア（コンパイラ）。  
様々なパッケージが含まれているので、とりあえずこれをインストールしておけば十分。

`sudo apt-get install texlive-lang-cjk`
`sudo apt-get install texlive-publishers`

## pdf へのフォント埋め込み設定

pdfにフォントを埋め込まない場合、特に日本語の文書では中国語のフォントが使われたりして読みにくいことが多いです。
そのための設定を行います。

`kanji-config-updmap status`  
を実行することで、現在のフォント埋め込みに関する設定が確認できる。
> CURRENT family : noEmbed  
> Standby family : ipa  
> Standby family : ipaex  

と表示される場合は、フォント埋め込みが設定されていない。

その場合は  
`kanji-config-updmap ipaex`  
を実行することで、日本語フォントの埋め込み設定をOnにできる。

`kanji-config-updmap status`  
の結果が
> CURRENT family : ipaex  
> Standby family : ipa

となっていれば埋め込みの設定が完了している。

## エディタ

なんでもよいが、pdfファイルとソースコードを表示できるものがよい。

[Atom](https://atom.io/)を勧める。

### Atom の設定
+ シンタックスハイライティング： [language-latex](https://atom.io/packages/language-latex)  
TeXの文法に応じて色付けしてくれる。  
なお，Atomでのパッケージの検索とインストールは File メニューの Settings で設定のタブを開き，Install を選んで表示される画面から行うことができる。

+ pdfの表示： [pdf-view](https://atom.io/packages/pdf-view)  
Atom内でpdfを表示するパッケージ。  
エディタの左にソースコード、右にpdfというように表示すると編集しやすい。

その他の[Atomの便利設定](../ubuntu/atom.md)についても参照のこと

# 文書の作成
## 文書作成の準備
フォルダの作成とlatexmkrcファイルの準備  
作業フォルダを作成し、その中に以下のlatexmkrcファイルをコピーする。
+ [英語文書用latexmkrcファイル](English/latexmkrc)
+ [日本語文書用latexmkrcファイル](Japanese/latexmkrc)

文書の種類に応じて、以下のファイルを上記フォルダ内にコピーする。
+ 英語論文：[ソースファイル](English/manuscript.tex), [bibTeX ファイル](English/refs.bib)
+ 日本語論文：[ソースファイル](Japanese/manuscript.tex), [bibTeX ファイル](English/refs.bib)
+ 科研費：[申請書ソース配布ページ](http://osksn2.hep.sci.osaka-u.ac.jp/~taku/kakenhiLaTeX/)
+ 概要：[日本物理学会テンプレート](Japanese/JPS_texTemplate.tex)  
なお、上記ファイルは[日本物理学会で配布されているテンプレート](https://www.gakkai-web.net/gakkai/jps/jps_n/template.html) の文字エンコードをUTF-8に変換したものである。

## 自動コンパイルの起動
ターミナルで上記のフォルダに移動し、  
`latexmk -pvc`  
を実行する。  
ソースコードが更新（保存）されるごとにコンパイルしてpdfファイルを作成してくれる。
