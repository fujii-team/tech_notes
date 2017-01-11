# Ubuntu の matplotlib できれいな図を書く

## 準備：seaborn のインストール
グラフライブラリ `seaborn`をインストールする。

> pip insatll seaborn


## インポート
> import matplotlib.pyplt as plt  
> import matplotlib  
> import seaborn as sns

## コンテキストの設定
> sns.set_context('poster')  
> sns.set_style('ticks')

## フォントの設定

> fontprop = matplotlib.font_manager.FontProperties(fname="/usr/share/fonts/truetype/ttf-dejavu//")  
> matplotlib.rcParams['mathtext.fontset'] = 'custom'  
> matplotlib.rcParams['mathtext.rm'] = 'DejaVu Sans'  
> matplotlib.rcParams['mathtext.it'] = 'DejaVu Sans:italic'  
> matplotlib.rcParams['mathtext.bf'] = 'DejaVu Sans:bold'  
> matplotlib.rcParams['mathtext.cursive'] = 'DejaVu Sans:oblique'


## 描画
> plt.plot(x, y)

軸を左・下だけにする  
> sns.despine()

複数グラフの時は
> plt.tight_layout()  

## 保存
> plt.savefig("filename.pdf")  
> plt.savefig("filename.png")
