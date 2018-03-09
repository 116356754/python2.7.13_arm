## SQLite交叉编译

SQLite的下载地址为：[http://www.sqlite.org/download.html](http://www.sqlite.org/download.html)，下载解压到虚拟机中，对6502和6657两种平台发布进行交叉编译。

### 6502与6657交叉编译

进入SQLite的源码目录。

#### 1.导出环境变量

```
#6502环境导出
export CC=arm-none-linux-gnueabi-gcc
```

```
#6657环境导出
export CC=arm-linux-gnueabihf-gcc
```

### 2.配置

```
#6502环境导出
./configure --host=arm-none-linux-gnueabi --prefix=/usr/local/sqlite
```

```
#6657环境导出
./configure --host=arm-linux-gnueabihf --prefix=/usr/local/sqlite
```

#### 3.编译

```
make
```

#### 4.安装

```
make install
```

在/usr/local/sqlite/lib目录下是动态与静态库文件，/usr/local/sqlite/include下是头文件。

#### 5.对python进行重新配置

进入到python2\_7\_13\_for\_arm文件夹中

    #6502
    cd python2_7_13_for_arm

    ../Python-2.7.13/configure --prefix=`pwd` \
        --host=arm-none-linux-gnueabi \
        --build=x86_64-linux-gnu \
        --enable-ipv6 \
        --enable-shared \
        ac_cv_file__dev_ptmx="yes" \
        ac_cv_file__dev_ptc="no" \
        LDFLAGS="-L/usr/local/sqlite/lib" \
        CPPFLAGS="-I/usr/local/sqlite/include"

    #6657
    cd python2_7_13_for_arm
    ../Python-2.7.13/configure --prefix=`pwd` \
        --host=arm-none-linux-gnueabi \
        --build=x86_64-linux-gnu \
        --enable-ipv6 \
        --enable-shared \
        ac_cv_file__dev_ptmx="yes" \
        ac_cv_file__dev_ptc="no" \
        LDFLAGS="-L/usr/local/sqlite/lib" \
        CPPFLAGS="-I/usr/local/sqlite/include"

```
    
```

#### 4.编译

```
#6502
make HOSTPYTHON=../python2_7_13_for_x86_64/python \
    HOSTPGEN=../python2_7_13_for_x86_64/Parser/pgen \
    BLDSHARED="arm-none-linux-gnueabi-gcc -shared" \
    CROSS_COMPILE=arm-none-linux-gnueabi- \
    CROSS_COMPILE_TARGET=yes \
    HOSTARCH=arm-none-linux-gnueabi \
    BUILDARCH=x86_64-linux-gnu \
    -j4
```

#### 5.安装

    #6502
    make install HOSTPYTHON=../python2_7_13_for_x86_64/python \
        BLDSHARED="arm-none-linux-gnueabi-gcc -shared" \
        CROSS_COMPILE=arm-none-linux-gnueabi- \
        CROSS_COMPILE_TARGET=yes \
        prefix=`pwd`



