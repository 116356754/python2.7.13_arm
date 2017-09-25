## zlib交叉编译

zlib的下载地址为：[http://www.zlib.net/](http://www.zlib.net/)，下载解压到虚拟机中，对6502和6657两种平台发布进行交叉编译。

### 6502交叉编译

进入zlib的源码目录。

#### 1.导出环境变量

```
export CC=arm-none-linux-gnueabi-gcc
```

### 2.配置

```
./configure --prefix=/usr/local/zlib
```

3.编译

```
make
```

4.安装

```
make install
```



