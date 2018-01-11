# py-faster-rcnn-install
## 方案1
ubuntu>=17 sudo apt install caffe-cpu
或者 用 sudo apt build-dep caffe-cpu        # dependencies for CPU-only version
## 方案2
### 安装依赖
http://caffe.berkeleyvision.org/install_apt.html
### 修改makefile
https://github.com/rbgirshick/py-faster-rcnn#requirements-software
### Anaconda3内安装其他依赖库
1. conda install scikit-image hdf5 h5py
2. conda install -c menpo opencv3=3.1.0
3. conda install protobuf
### Error: no pyconfig.h
CPLUS_INCLUDE_PATH = /home/lab/anaconda2/include/python3.6m/
