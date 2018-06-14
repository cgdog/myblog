---
title: ubuntu14.04 64位 cuda7.5 配置caffe
id: 224
categories:
  - machine learning
date: 2016-06-01 19:59:33
tags:
  - deep learning
---

记录一自己安装caffe的过程，仅供自己参考。

## 一、安装cuda7.5 （GPU版的需要）

直接从Nvidia官网下载cuda-repo-ubuntu1404-7-5-local_7.5-18_amd64.deb，2GB左右，这是最新的CUDA，里面包含驱动，安装时,我没有关闭图形界面(然后，重启时，进入图形登录界面，出现提示音，然后黑屏了，我按ctrl+alt+F1，进入伪终端，运行sudo service lightdm start，然后按alt+F7还是黑屏，重新启后又不黑屏了正常登录。在另一台机器上安装时，并没有遇见黑屏的现象)。安装教程参考Nvidia官方文档：[http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#axzz47JDgI4Zi](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#axzz47JDgI4Zi)

具体ubuntu版安装见官网教程:[http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#ubuntu-installation](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#ubuntu-installation)

注意，不要忽略上述链接中的第5步[Perform the post-installation actions](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions).这是配置环境变量，可以配在/etc/profile文件末尾，配好要重启电脑，用source /etc/profile，并不能让环境变量立即生效(小心重启黑屏哦，哈哈哈)。

## 二、打开caffe官网[http://caffe.berkeleyvision.org/install_apt.html](http://caffe.berkeleyvision.org/install_apt.html)

一路安装依赖，
1 cuda上面已安装过了。

2


``` bash
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
```


3


``` bash
sudo apt-get install libatlas-base-dev
```


4

``` bash
sudo apt-get install python-dev
```


5

``` bash
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
```


6 安装boost，这个好像官网上没说(或者我没看到吧)。不安装这个，编译caffe时，会报boost/thread.hpp no such file or directory之类的错误。


``` bash
sudo apt-get install libboost-all-dev
```


另外，我还安装了这些依赖，可能是不需的吧(我安装faster-r-cnn时必须安装这些依赖，而faster-r-cnn里面包含有caffe)：

``` bash
apt-get install cython
apt-get install python-opencv
sudo pip install easydict
sudo apt-get install python-yaml
sudo apt-get install python-protobuf
sudo apt-get install python-skimage
```

## 三、编译caffe

[http://caffe.berkeleyvision.org/installation.html#compilation](http://caffe.berkeleyvision.org/installation.html#compilation)

我用的sudo make all加sudo make pycaffe

编译时基本上会报一个错误：

找不到库文件 libcudart.so.7.5，

解决方案（忘记在哪看到的这个解决方案了，当时只记在word上了，忘记链接了，thanks）：执行命令 sudo gedit /etc/ld.so.conf.d/cuda.conf，在文件中添加如下内容：



``` bash
/usr/local/cuda/lib64 
/lib
```

然后再执行命令：


``` bash
sudo ldconfig -v
```

此后，编译一路畅通。