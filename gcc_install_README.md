# Install-GCC
How to install GCC on Linux without root

#### 1. GCC及其依赖库  
编译之前需先安装好GCC的依赖库：gmp、mpfr和mpc。编译还依赖m4等编译工具，如果没有，则在执行configue时会报相应的错误，这时需要先安装好这些编译工具。

  1.1. gmp库   
  GMP为“GNU MP Bignum Library”的缩写，是一个GNU开源数学运算库，国内镜像下载地址：
  
  1) https://mirrors.tuna.tsinghua.edu.cn/gnu/gmp/
  2) http://mirrors.nju.edu.cn/gnu/gmp/
  3) http://mirrors.ustc.edu.cn/gnu/gmp/
  
  1.2. mpfr库
  mpfr是一个GNU开源大数运算库，它依赖gmp，国内镜像下载地址：
  
  1) https://mirrors.tuna.tsinghua.edu.cn/gnu/mpfr/
  2) http://mirrors.nju.edu.cn/gnu/mpfr/
  3) http://mirrors.ustc.edu.cn/gnu/mpfr/
  
  1.3. mpc库
  mpc是GNU的开源复杂数字算法，它依赖gmp和mpfr，国内镜像下载地址：
  
  1) https://mirrors.tuna.tsinghua.edu.cn/gnu/mpc/
  2) http://mirrors.nju.edu.cn/gnu/mpc/
  3) http://mirrors.ustc.edu.cn/gnu/mpc/
  
  1.4. m4编译工具
  本文选择的是最新版本m4-1.4.16，下载地址：
  
  1) https://mirrors.tuna.tsinghua.edu.cn/gnu/m4/
  2) http://mirrors.nju.edu.cn/gnu/m4/  
  3) http://mirrors.ustc.edu.cn/gnu/m4/

  1.5. 安装源代码包
  涉及到的所有安装源代码包：
    
    mkdir gcc
    cd gcc
    wget https://mirrors.tuna.tsinghua.edu.cn/gnu/gmp/gmp-6.3.0.tar.gz
    wget https://mirrors.tuna.tsinghua.edu.cn/gnu/mpfr/mpfr-4.2.2.tar.gz
    wget https://mirrors.tuna.tsinghua.edu.cn/gnu/mpc/mpc-1.3.1.tar.gz
    wget https://mirrors.tuna.tsinghua.edu.cn/gnu/m4/m4-1.4.20.tar.gz
    wget https://mirrors.tuna.tsinghua.edu.cn/gnu/gcc/gcc-10.1.0/gcc-10.1.0.tar.gz
   
  
  1.6. GCC的依赖库间还互有依赖：mpfr依赖gmp、mpc依赖gmp和mpfr，所以GCC的编译安装顺序为：
  
  1) m4（如果需要）
  2) gmp
  3) mpfr
  4) mpc
  5) GCC

  为了不污染已有的编译和运行环境，将GCC及依赖库均安装到/usr/local或/usr/software指定目录， gcc安装时指定依赖库目录需要单独存放（即依赖库分别安装到不同的指定目录下），如果依赖库安装在同一个目录下gcc configure步骤可能会报错。

#### 2. 编译安装依赖库
2.1. 编译安装m4

    tar zxf m4-1.4.20.tar.gz
    cd m4-1.4.20
    ./configure --prefix=/usr/program
    make
    make install
  
2.2. 编译安装gmp：    
执行configure生成Makefile时，需要用到m4，一般路径为/usr/bin/m4，如果没有则需要先安装，否则报错“no usable m4”错误。

    tar zxf gmp-6.3.0.tar.gz
    cd gmp-6.3.0
    ./configure --prefix=/usr/software/gmp
    make
    make install

2.3. 编译安装mpfr

    tar xzf  mpfr-4.2.2.tar.gz
    cd mpfr-4.2.2
    ./configure --prefix=/usr/software/mpfr --with-gmp=/usr/software/gmp
    make
    make install

2.4. 编译安装mpc

    tar xzf  mpc-1.3.1.tar.gz
    cd mpc-1.3.1
    ./configure --prefix=/usr/software/mpc --with-gmp=/usr/software/gmp --with-mpfr=/usr/software/mpfr
    make
    make install

#### 3. 设置LD_LIBRARY_PATH
在编译GCC之前，如果不设置LD_LIBRARY_PATH（如果编译gmp时没有指定“--prefix”时安装，一般不用再显示设置），则可能编译时报“error while loading shared libraries: libmpfr.so.6: cannot open shared object file: No such file or directory”等错误。

    export LD_LIBRARY_PATH=/usr/software/gmp/lib:/usr/software/mpfr/lib:/usr/software/mpc/lib:$LD_LIBRARY_PATH

#### 4. 编译安装gcc
在执行make编译GCC时，有些费时，请耐心等待。在一台Intel Xeon 2.30GHz的48核128GB内存机器上花费228分钟（将近4个小时，同台机器编译9.1.0花费190分钟），编译GCC-8.3.0的GCC版本为4.8.5（64位）。

    tar xzf gcc-10.1.0.tar.gz
    cd gcc-10.1.0
    ./configure --prefix=/usr/local/gcc --with-gmp=/usr/software/gmp --with-mpfr=/usr/software/mpfr --with-mpc=/usr/software/mpc
    make -j4
    make install
    ln -s /usr/local/gcc /usr/local/gcc
    export PATH=/usr/local/gcc/bin:$PATH
    export LD_LIBRARY_PATH=/usr/local/gcc/lib64:$LD_LIBRARY_PATH
    export MANPATH=/usr/local/gcc/share/man:$MANPATH
    gcc --version
