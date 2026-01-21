# <center>pytorch_geometric install</center>

## 先安装pytorch

    conda install pytorch==1.7.0 cudatoolkit=10.2 -c pytorch

## 检查自己虚拟环境中已安装的pytoch版本，安装的pytorch是cpu还是gpu的，以及cuda版本等等，操作命令如下代码。

    import torch
    print(torch.__version__)                # 查看pytorch安装的版本号
    print(torch.cuda.is_available())        # 查看cuda是否可用。True为可用，即是gpu版本pytorch
    print(torch.cuda.get_device_name(0))    # 返回GPU型号
    print(torch.cuda.device_count())        # 返回可以用的cuda（GPU）数量，0代表一个
    print(torch.version.cuda)               # 查看cuda的版本

## 去GitHub的pyg-team主页中找到pytorch-geometric包。网址如下：

    https://github.com/pyg-team/pytorch_geometric?tab=readme-ov-file


## Additional Libraries
    If you want to utilize the full set of features from PyG, there exists several additional libraries you may want to install:

    pyg-lib: Heterogeneous GNN operators and graph sampling routines
    torch-scatter: Accelerated and efficient sparse reductions
    torch-sparse: SparseTensor support
    torch-cluster: Graph clustering routines
    torch-spline-conv: SplineConv support
    These packages come with their own CPU and GPU kernel implementations based on the PyTorch C++/CUDA/hip(ROCm) extension interface. For a basic usage of PyG, these dependencies are fully optional. We recommend to start with a minimal installation, and install additional dependencies once you start to actually need them.

    For ease of installation of these extensions, we provide pip wheels for all major OS/PyTorch/CUDA combinations, see here（https://data.pyg.org/whl/）.

## 点击进入
    
    https://data.pyg.org/whl/torch-1.7.0%2Bcu102.html

## 下载对应的依赖包whl， 依次安装：

    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_cluster-1.5.9-cp37-cp37m-linux_x86_64.whl
    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_scatter-2.0.7-cp37-cp37m-linux_x86_64.whl
    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_sparse-0.6.9-cp37-cp37m-linux_x86_64.whl
    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_spline_conv-1.2.1-cp37-cp37m-linux_x86_64.whl

    先安装torch_scatter

    pip install torch_scatter-2.0.7-cp37-cp37m-win_amd64.whl

    第二步安装torch_sparse

    pip install torch_sparse-0.6.9-cp37-cp37m-win_amd64.whl

    第三步安装torch_cluster

    pip install torch_cluster-1.5.9-cp37-cp37m-win_amd64.whl

    第四步安装torch_spline_conv

    pip install torch_spline_conv-1.2.1-cp37-cp37m-win_amd64.whl

## 最后安装torch_geometric

    pip install torch_geometric==1.6.3
    
## 整体安装方法

    conda install pytorch==1.7.0 cudatoolkit=10.2 -c pytorch
    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_cluster-1.5.9-cp37-cp37m-linux_x86_64.whl
    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_scatter-2.0.7-cp37-cp37m-linux_x86_64.whl
    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_sparse-0.6.9-cp37-cp37m-linux_x86_64.whl
    wget https://data.pyg.org/whl/torch-1.7.0%2Bcu102/torch_spline_conv-1.2.1-cp37-cp37m-linux_x86_64.whl
    pip install *.whl
    pip install torch_geometric==1.6.3