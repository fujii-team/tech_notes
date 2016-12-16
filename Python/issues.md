# Intel MKL FATAL ERROR:
Anaconda のVirtual env環境で

`Intel MKL FATAL ERROR: Cannot load libmkl_avx.so or libmkl_def.so.`

と言われる問題について。

`conda upgrade mkl, mkl-service -f`

`conda upgrade numpy -f`

`conda upgrade scipy -f`

としたら解決した。
