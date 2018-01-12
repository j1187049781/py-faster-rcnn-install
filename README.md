# py-faster-rcnn-install
## 编译环境 step 1 
ubuntu>=17 sudo apt build-dep caffe-cpu    # dependencies for CPU-only version
##  编译环境 step 2
### 安装依赖
http://caffe.berkeleyvision.org/install_apt.html
### 安装其他依赖库
1. for req in $(cat requirements.txt); do pip install $req; done
## 编译
### No GPU
https://www.cnblogs.com/justinzhang/p/5386837.html
1. /py-faster-rcnn/lib/fast_rcnn/config.py
    __C.USE_GPU_NMS = False
2. 将 ~/py-faster-rcnn/tools/test_net.py和 ~/py-faster-rcnn/tools/train_net.py的caffe.set_mode_gpu()修改为caffe.set_mode_cpu()
3. 将~/py-faster-rcnn/lib/setup.py中，含有'nms.gpu_nms’的部分去掉，去掉后的内容如下
```python
ext_modules = [
    Extension(
        "utils.cython_bbox",
        ["utils/bbox.pyx"],
        extra_compile_args={'gcc': ["-Wno-cpp", "-Wno-unused-function"]},
        include_dirs = [numpy_include]
    ),
    Extension(
        "nms.cpu_nms",
        ["nms/cpu_nms.pyx"],
        extra_compile_args={'gcc': ["-Wno-cpp", "-Wno-unused-function"]},
        include_dirs = [numpy_include]
    ),
    Extension(
        'pycocotools._mask',
        sources=['pycocotools/maskApi.c', 'pycocotools/_mask.pyx'],
        include_dirs = [numpy_include, 'pycocotools'],
        extra_compile_args={
            'gcc': ['-Wno-cpp', '-Wno-unused-function', '-std=c99']},
    ),
]
```
### 修改makefile
1. https://github.com/rbgirshick/py-faster-rcnn#requirements-software
2. https://github.com/j1187049781/py-faster-rcnn-install/blob/master/Error:hdf5
3. sudo apt-get install python-numpy
## for run demo
1. sudo pip install easydict
2. sudo pip install opencv-python
3. nms_wraper.py -->no nms_gpu
4. sudo apt-get install python-tk
5. download model  https://github.com/rbgirshick/py-faster-rcnn#requirements-software
6. python demo.py --cpu
