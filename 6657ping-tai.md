## python2.7.13在6657平台上编译

区别6502在于交叉编译的时候，导出的环境变量和编译以及安装的时候，其他都是和6502一模一样。1、

### 1.导出环境变量

```
export CC=arm-linux-gnueabihf-gcc CXX=arm-linux-gnueabihf-g++ AR=arm-linux-gnueabihf-ar \
RANLIB=arm-linux-gnueabihf-ranlib
```

### 2.配置

    ../Python-2.7.13/configure --prefix=`pwd` \
        --host=arm-linux-gnueabihf \
        --build=x86_64-linux-gnu \
        --enable-ipv6 \
        --enable-shared \
        ac_cv_file__dev_ptmx="yes" \
        ac_cv_file__dev_ptc="no"

3.编译

```
make HOSTPYTHON=../python2_7_13_for_x86_64/python \
    HOSTPGEN=../python2_7_13_for_x86_64/Parser/pgen \
    BLDSHARED="arm-linux-gnueabihf-gcc -shared" \
    CROSS_COMPILE=arm-linux-gnueabihf- \
    CROSS_COMPILE_TARGET=yes \
    HOSTARCH=arm-linux-gnueabihf \
    BUILDARCH=x86_64-linux-gnu \
    -j4
```

### 4.安装

    make install HOSTPYTHON=../python2_7_13_for_x86_64/python \
        BLDSHARED="arm-linux-gnueabihf-gcc -shared" \
        CROSS_COMPILE=arm-linux-gnueabihf- \
        CROSS_COMPILE_TARGET=yes \
        prefix=`pwd`



