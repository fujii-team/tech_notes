# 論文をTeXで書く

卒論・修論をTeXで書くと、以下のメリットがあります

+ 図番号・式番号・引用文献番号などが自動的に振られる
+ 図をフォルダごとに管理できる
+ git で管理ができる。
+ フォーマットを気にせず、内容にだけ集中できる

ただし、最初のセットアップなどに時間がかかったりすることが多いので、
ここに簡単な概要を述べる。


# 卒論・修論用TeXファイルの作り方

テンプレートファイルを[ここ](samples/sotsuron_ja) を適当なフォルダにダウンロードする。

ファイル構造は以下のようになっている。

sotsuron_ja  
　├ latexmk  
　├ .gitignore  
　├ git-latexdiff  
　├ manuscripts.tex  
　├ introduction.tex  
　├　…  
　├ refs.bib  
　└ figs  
　　　├ figure1.pdf  
　　　├　…  

ここで、manuscripts.tex にはどういったパッケージを使うかの情報と、各TeXファイルのリンク、
さらに摘要を書く。
各章は intdocution.tex のように別ファイルとして保存されている。
別ファイルとして保存しておくとわかりやすい。

また、参考文献は refs.bib 内に bibtex フォーマットで書いておく。
Mendeley などでは bibtex で論文をコピーできる。

上記ファイルをコンパイルするためには、 `latexmk -pvc manuscripts.tex` を実行する。


# 投稿論文用TeXファイルの作り方

 [ここ](samples/paper_en) にあるサンプルファイルをダウンロードする。
上記の「卒論・修論用TeXファイルの作り方」と同様のファイル構造である。
