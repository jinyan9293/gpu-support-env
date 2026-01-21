# GPU 环境安装说明

## 理解GPU服务器CUDA驱动、CUDAToolkit、CUDNN及其他神经网络框架工具(tensorflow、pytorch、keras)

* 显卡是我们平时说的GPU，现在大多数的电脑使用NVIDIA公司生产的显卡；常见的型号有Tesla V100，GTX950M，GTX1050TI，GTX1080等。

* 显卡驱动Driver，特指NVIDIA的显卡驱动程序。

* CUDA是显卡厂商NVIDIA推出的运算平台。CUDA™是一种由NVIDIA推出的通用并行计算架构，是一种并行计算平台和编程模型，该架构使GPU能够解决复杂的计算问题。CUDA英文全称是Compute Unified Device Architecture。

    >有人说：CUDA是一门编程语言，像C,C++,python 一样，也有人说CUDA是API。  
    >官方说：CUDA是一个并行计算平台和编程模型，能够使得使用GPU进行通用计算变得简单和优雅。  
    >运行CUDA应用程序要求系统至少具有一个具有CUDA功能的GPU和与CUDA Toolkit兼容的驱动程序。  
    >查看CUDA版本命令：nvcc -V 或nvcc --version或cat /usr/local/cuda/version.txt  

    需要知道：CUDA和CUDA Driver显卡驱动不是一一对应的，比如同一台电脑上可同时安装CUDA 9.0、CUDA 9.2、CUDA 10.0等版本。

### 1. 基本依赖逻辑顺序
  
>显卡驱动版本-> CUDA版本 -> cudnn -> tensorflow / pytorch;

### 2. 硬盘驱动版本与CUDA工具包版本对应表

>每一个版本的CUDAtoolkit都对应一个最低版本的CUDA驱动，CUDA驱动相对于CUDAtoolkit是向下兼容的，即某一版本的CUDAtookit可以在包括最低版本及以上更高级版本的CUDA驱动上运行。 
><https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/index.html>  

### 3. CUDNN与CUDA版本对应表

>同一个CUDA 版本支持安装多个版本的cuDNN。  
><https://developer.nvidia.com/rdp/cudnn-archive>  

### 4. tensorflow与CUDNN、CUDA之间的版本对应表

><https://blog.csdn.net/ly869915532/article/details/124542362>

### 5. tensorrt与CUDA、CUDNN之间的版本对应表

><https://docs.nvidia.com/deeplearning/tensorrt/archives/index.html>
><https://blog.csdn.net/weixin_41540237/article/details/131589929>

## 完整环境安装经验

### 创建conda环境

    conda create --name alphafold python==3.8

### 以GPU服务器centos系统为例，先查看硬盘信息

    nvidia-smi

### 1. 安装cuda (nvidia)

    conda install cudatoolkit==11.2.2

### 2. 安装cudnn (nvidia)

    conda install cudnn=8.1

### 3. 安装jax、jaxlib

    pip install --upgrade --no-cache-dir jax==0.3.25 jaxlib==0.3.25+cuda11.cudnn82 -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html

### 4. 安装tensorflow

    pip install tensorflow_gpu==2.10.0
        
        
>注：应先安装tensorrt (nvidia)

    pip install tensorrt

>如果导入tensorflow报错，可以尝试：
><https://www.cnblogs.com/yaos/p/17859452.html>

    cd /home/shuchang.wu/miniconda3/envs/alphafold/lib/python3.8/site-packages/tensorrt_libs
    ln -s libnvinfer.so.10 libnvinfer.so.7
    ln -s libnvinfer_plugin.so.10 libnvinfer_plugin.so.7

    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/shuchang.wu/miniconda3/envs/alphafold/lib/python3.8/site-packages/tensorrt_libs

>安装完毕可执行以下命令测试：
    python -c "import tensorflow as tf;print(tf.reduce_sum(tf.random.normal([1000, 1000])))"
