# Tensorflow error : kernel version mismatch
```
E tensorflow/stream_executor/cuda/cuda_diagnostics.cc:229] kernel version 352.55 does not match DSO version 352.63 -- cannot find working devices in this configuration
```
Tensor flow と cuda でバージョンが違うと言われた。
```
sudo apt-get remove cuda
sudo apt-get install cuda
sudo shutdown -r now
```
すると治った。
再起動だけでよい？
