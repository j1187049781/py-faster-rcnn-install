# py-faster-rcnn-install
## 编译环境 step 1 
ubuntu>=17 sudo apt install caffe-cpu
或者 用 sudo apt build-dep caffe-cpu        # dependencies for CPU-only version
##  编译环境 step 2
### 安装依赖
http://caffe.berkeleyvision.org/install_apt.html
### 修改makefile
https://github.com/rbgirshick/py-faster-rcnn#requirements-software
###安装其他依赖库
0. for req in $(cat requirements.txt); do pip install $req; done
1. 
2. 
3. 
### No GPU
https://www.cnblogs.com/justinzhang/p/5386837.html
1. /py-faster-rcnn/lib/fast_rcnn/config.py
    __C.USE_GPU_NMS = False
2. 将 ~/py-faster-rcnn/tools/test_net.py和 ~/py-faster-rcnn/tools/train_net.py的caffe.set_mode_gpu()修改为caffe.set_mode_cpu()
3. 将~/py-faster-rcnn/lib/setup.py中，含有'nms.gpu_nms’的部分去掉，去掉后的内容如下
''' 
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
'''
