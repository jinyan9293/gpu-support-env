# <center>用conda安装Alphafold3</center>  

## 1. 创建conda环境

    conda create -n afd3.0.1 python=3.11 -y

    conda activate afd3.0.1

    git clone https://github.com/google-deepmind/alphafold3.git

    cd alphafold3

## 2. 安装依赖库

    pip install -r dev-requirements.txt

## 3. 安装af3

    pip install . --no-deps --verbose

## 4. 安装数据库驱动

    build_data
## 

# <center>如果出现以下类似问题</center>

## 5. 重装gcc 和 g++ （由于报错提示服务器gcc/g++版本太老，需要安装更高版本）

如果编译失败，cmake最为关键，需要安装最新版本的依赖库

    conda install gcc_linux-64 gxx_linux-64

安装完成后重新操作第3步。

## 6. 解决python依赖库版本冲突问题

通过测试调整python依赖库版本，最终得到依赖库文件rms.txt，详见下面文档。

## 7. 安装python 依赖库

    pip install -r rms.txt
    
    pip install cmake ninja pybind11 scikit_build_core

## 8. 安装af3

    pip install . --no-deps --verbose

## 9. 安装数据库驱动

    build_data

显示安装成功就可以使用了。

## **rms.txt**

    absl-py==2.1.0
    chex==0.1.87
    dm-haiku==0.0.13
    dm-tree==0.1.8
    filelock==3.16.1
    jax[cuda12]==0.4.34
    jax-cuda12-pjrt==0.4.34
    jax-cuda12-plugin[with-cuda]==0.4.34
    jax-triton==0.2.0
    jaxlib==0.4.34
    jaxtyping==0.2.34
    jmp==0.0.4
    ml-dtypes==0.5.0
    numpy==2.1.3
    nvidia-cublas-cu12
    nvidia-cuda-cupti-cu12
    nvidia-cuda-nvcc-cu12
    nvidia-cuda-runtime-cu12
    nvidia-cudnn-cu12
    nvidia-cufft-cu12
    nvidia-cusolver-cu12
    nvidia-cusparse-cu12
    nvidia-nccl-cu12
    nvidia-nvjitlink-cu12
    opt-einsum==3.4.0
    pillow==11.0.0
    rdkit
    scipy==1.14.1
    tabulate==0.9.0
    toolz==1.0.0
    tqdm==4.67.0
    triton==3.1.0
    typeguard==2.13.3
    typing-extensions==4.12.2
    zstandard==0.23.0

## 手动修改 *pyproject.toml* 使依赖包版本与上述已安装包版本一致

    [build-system]
    requires = [
        "scikit_build_core",
        "pybind11",
        "cmake>=3.28",
        "ninja",
        "numpy",
    ]
    build-backend = "scikit_build_core.build"

    [project]
    name = "alphafold3"
    version = "3.0.1"
    requires-python = ">=3.11"
    readme = "README.md"
    license = {file = "LICENSE"}
    dependencies = [
        "absl-py",
        "chex",
        "dm-haiku==0.0.13",
        "dm-tree",
        "jax==0.4.34",
        "jax[cuda12]==0.4.34",
        "jax-triton==0.2.0",
        "jaxtyping==0.2.34",
        "numpy",
        "rdkit==2024.3.2",
        "triton==3.1.0",
        "tqdm",
        "typeguard==2.13.3",
        "zstandard",
    ]

    [project.optional-dependencies]
    test = ["pytest>=6.0"]

    [tool.scikit-build]
    wheel.exclude = [
        "**.pyx",
        "**/CMakeLists.txt",
        "**.cc",
        "**.h"
    ]
    sdist.include = [
        "LICENSE",
        "OUTPUT_TERMS_OF_USE.md",
        "WEIGHTS_PROHIBITED_USE_POLICY.md",
        "WEIGHTS_TERMS_OF_USE.md",
    ]

    [tool.cibuildwheel]
    build = "cp3*-manylinux_x86_64"
    manylinux-x86_64-image = "manylinux_2_28"

    [project.scripts]
    build_data = "alphafold3.build_data:build_data"

