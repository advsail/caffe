# Caffe

[![Build Status](https://travis-ci.org/BVLC/caffe.svg?branch=master)](https://travis-ci.org/BVLC/caffe)
[![License](https://img.shields.io/badge/license-BSD-blue.svg)](LICENSE)

Caffe is a deep learning framework made with expression, speed, and modularity in mind.
It is developed by Berkeley AI Research ([BAIR](http://bair.berkeley.edu))/The Berkeley Vision and Learning Center (BVLC) and community contributors.

Check out the [project site](http://caffe.berkeleyvision.org) for all the details like

- [DIY Deep Learning for Vision with Caffe](https://docs.google.com/presentation/d/1UeKXVgRvvxg9OUdh_UiC5G71UMscNPlvArsWER41PsU/edit#slide=id.p)
- [Tutorial Documentation](http://caffe.berkeleyvision.org/tutorial/)
- [BAIR reference models](http://caffe.berkeleyvision.org/model_zoo.html) and the [community model zoo](https://github.com/BVLC/caffe/wiki/Model-Zoo)
- [Installation instructions](http://caffe.berkeleyvision.org/installation.html)

and step-by-step examples.

## Custom distributions

 - [Intel Caffe](https://github.com/BVLC/caffe/tree/intel) (Optimized for CPU and support for multi-node), in particular Intel® Xeon processors.
- [OpenCL Caffe](https://github.com/BVLC/caffe/tree/opencl) e.g. for AMD or Intel devices.
- [Windows Caffe](https://github.com/BVLC/caffe/tree/windows)

## Community

[![Join the chat at https://gitter.im/BVLC/caffe](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/BVLC/caffe?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Please join the [caffe-users group](https://groups.google.com/forum/#!forum/caffe-users) or [gitter chat](https://gitter.im/BVLC/caffe) to ask questions and talk about methods and models.
Framework development discussions and thorough bug reports are collected on [Issues](https://github.com/BVLC/caffe/issues).

Happy brewing!

## License and Citation

Caffe is released under the [BSD 2-Clause license](https://github.com/BVLC/caffe/blob/master/LICENSE).
The BAIR/BVLC reference models are released for unrestricted use.

Please cite Caffe in your publications if it helps your research:

    @article{jia2014caffe,
      Author = {Jia, Yangqing and Shelhamer, Evan and Donahue, Jeff and Karayev, Sergey and Long, Jonathan and Girshick, Ross and Guadarrama, Sergio and Darrell, Trevor},
      Journal = {arXiv preprint arXiv:1408.5093},
      Title = {Caffe: Convolutional Architecture for Fast Feature Embedding},
      Year = {2014}
    }

## Added By Myself

## How to build Caffe on Ubuntu 16.04

If you just want to use the officially-compiled caffe bins instead of modifying caffe code, using a docker is a better option. Currently there are two very-well maintained caffe docker.

1. bvlc/caffe:cpu
2. ufoym/deepo:cpu

Detailed description of how to use `bvlc/caffe:cpu` is located [Here](https://github.com/advsail/caffe_docker).

Steps to build caffe on a Ubuntu 16.04 machine.

Prerequisites: Install the dependent packages

```shell
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
for req in $(cat ./python/requirements.txt); do pip install $req; done
```

Fix 3 installation errors due to using Python 2.x version. Matplotlib error was ignored.

```shell
pip install 'scikit-image<0.15'
pip install 'networkx==2.2'
pip install IPython==5.0 --user
```

As you will see when you run the classification of an image, an `skimage.io` will occur as flowing. `ImportError: No module named skimage.io` Run the following command to install skimage.

```shell
sudo apt-get install python-skimage
```

For reference, if you meet new errors regarding of python packages, you can use the following command instead of using `pip install`

```shell
sudo apt-get install python-matplotlib python-numpy python-pil python-scipy
sudo apt-get install build-essential cython
```

Prepare the Makefile.config

```shell
cp Makefile.config.example Makfile.config
Uncommend CPU_ONLY := 1 in Makefile.config and save the file
```

Build the project

```shell
cd build
make clean
cmake ..
make all
```

Install the bins

```shell
make install
```

Test the installation

```shell
make runtest
```

If you follow the `make` method on [BVLC/caffe](http://caffe.berkeleyvision.org/installation.html#compilation) you will run into two errors, so this way is not recommended. If you insist to use `make`, fixes are listed below.

[Error 1: hdf5.h missing issue](https://askubuntu.com/questions/629654/building-caffe-failed-to-see-hdf5-h)

[Error 2: libcaffe.so.1.0.0 error issue](https://github.com/BVLC/caffe/issues/5555)


## A classification example

Before running classification, we need to download the models first. Run the following command to download the model file.

```shell
scripts/download_model_binary.py models/bvlc_reference_caffenet
```

Classification command example

```shell
python python/classify.py examples/images/cat.jpg foo
```

Note that the results are saved into `foo.npy`, which is a numpy data file. Use the following command to see the results in python.

```python
import numpy as np
np.load('foo.npy')
```







