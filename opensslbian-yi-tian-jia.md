## OpenSSL交叉编译

zlib的下载地址为：[http://www.openssl.org/source/](http://www.openssl.org/source/)，下载解压到虚拟机中，对6502和6657两种平台发布进行交叉编译。

### 6502交叉编译

进入zlib的源码目录。

#### 1.导出环境变量

```
export CC=arm-none-linux-gnueabi-gcc
```

### 2.配置

```
./config no-asm shared --prefix=/usr/local/ssl
```

#### 3.编译

```
make
```

#### 4.安装

```
make install
```

在/usr/local/zlib/lib目录下是动态与静态库文件，/usr/local/zlib//include下是头文件。

#### 5.修改python的模块文件

在Modules/setup 取消注释setup.dist的214行218、219、220与221行，修改成为如下语句

![](/assets/sslcompile.png)

跟着对python进行重新配置、编译、安装

#### 6.添加openssl到python中

将/usr/local/ssl/lib/文件夹的文件拷贝到python的lib目录下，以后加入到arm中的linux的LD\_LIBRARY\_PATH变量中。

![](/assets/importzlib.png)

