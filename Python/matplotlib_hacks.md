# Ubuntu の matplotlib できれいな図を書く

## 準備：seaborn のインストール
グラフライブラリ `seaborn`をインストールする。

> pip insatll seaborn


## インポート
```python
import seaborn as sns
sns.set_context("paper", 2.5, {"lines.linewidth": 1.5, "lines.markersize": 7})
sns.set_style('ticks')

import matplotlib

fontprop = matplotlib.font_manager.FontProperties(fname="/usr/share/fonts/truetype/ttf-dejavu//")
matplotlib.rcParams['mathtext.fontset'] = 'custom'
matplotlib.rcParams['mathtext.rm'] = 'DejaVu Sans'
matplotlib.rcParams['mathtext.it'] = 'DejaVu Sans:italic'
matplotlib.rcParams['mathtext.bf'] = 'DejaVu Sans:bold'
matplotlib.rcParams['mathtext.cal'] = 'DejaVu Sans:oblique'
```

## 描画
> plt.plot(x, y)

軸を左・下だけにする  
> sns.despine()

複数グラフの時は
> plt.tight_layout()  

## 保存
> plt.savefig("filename.pdf")  
> plt.savefig("filename.png")
