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

在/usr/local/zlib/lib目录下是动态与静态库文件，/usr/local/zlib//include下是头文件。

