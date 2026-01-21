# <center>Install vllm</center>

## 1. Create vllm conda environment

    conda create -n vllm python=3.12 -y
    conda activate vllm

## 2. Install gcc

    conda install gcc=14.2 gxx=14.2 -y

## 3. Install torch

### conda install

    conda install pytorch==2.4.0 torchvision==0.19.0 torchaudio==2.4.0 pytorch-cuda=12.1 -c pytorch -c nvidia

    // conda install pytorch==2.4.1 torchvision==0.19.1 torchaudio==2.4.1 pytorch-cuda=12.4 -c pytorch -c nvidia

    // Version 2.6.0 does not support conda installation

### pip install

    pip install torch==2.4.0 torchvision==0.19.0 torchaudio==2.4.0 --index-url https://download.pytorch.org/whl/cu121

    // pip install torch==2.4.1 torchvision==0.19.1 torchaudio==2.4.1 --index-url https://download.pytorch.org/whl/cu124

    // pip install torch==2.6.0 torchvision==0.21.0 torchaudio==2.6.0 --index-url https://download.pytorch.org/whl/cu124

## 4. Install xformers

### 注意xformers和pytorch的版本对应关系

    pip install xformers==0.0.27.post2

    // pip install xformers==0.0.28

    // pip install xformers==0.0.29.post2

## 5. 安装vllm

### 注意vllm的版本和以上环境的兼容关系

    pip install vllm==0.6.3.post1


## 1. Create vllm env

    conda create -n vllm_new python=3.12 -y
    conda activate vllm_new

## 2. Install gcc

    conda install gcc=13 gxx=13 -y
    
### 解决报错

    /usr/local/cuda-12.4/include/crt/host_config.h:143:2: error: #error -- unsupported GNU version! gcc versions later than 13 are not supported! The nvcc flag '-allow-unsupported-compiler' can be used to override this version check; however, using an unsupported host compiler may cause compilation failure or incorrect run time execution. Use at your own risk.


## 3. Install Pytorch

    pip install torch==2.6.0 torchvision==0.21.0 torchaudio==2.6.0 --index-url https://download.pytorch.org/whl/cu124

## 4. Install Xformers

    export CPATH=/usr/local/cuda-12.4/targets/x86_64-linux/include/:$CPATH
    export LD_LIBRARY_PATH=/usr/local/cuda-12.4/targets/x86_64-linux/lib:$LD_LIBRARY_PATH
    export PATH=/usr/local/cuda-12.4/bin/:$PATH

    git clone 

    git submodule update --init --recursive


# 5. Install vllm

    pip install vllm --pre --extra-index-url https://wheels.vllm.ai/nightly
