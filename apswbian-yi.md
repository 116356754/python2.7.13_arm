## APSW库编译

apsw的下载地址为[apsw-3.22.0-r1.zip](https://github.com/rogerbinns/apsw/releases/download/3.22.0-r1/apsw-3.22.0-r1.zip)，该库以来前面编译的SQLite3，所以需要事先能够编译出Sqlite安装到/usr/local/sqlite目录中。

### 升级python

ubuntu12.04自带的python为2.7.3的，而该版本unicode默认是unsigned long，也就是4个字节的长度，而我们编译的python2.7.13的unicode是unsigned short，也就是2个字节的长度，虽然也能编译出来，但是在2.7.13中会报错：`undefined symbol: PyUnicodeUCS4_DecodeUTF8`

移除原来的python

```
rm /usr/bin/python
```

解压python2.7.13到目录中

```
tar xf Python-2.7.13.tar
```

配置

```
./configure --prefix=/usr/local/python27
```

编译

```
make
```

安装

```
make install
```

建立新的python的软链接

```
ln -s /usr/local/python27/bin/python /usr/bin/python
```

这时候我们再查看一下版本，确认是2.7.13

```
python -V
```

## APSW交叉编译

### 6502与6657交叉编译

进入APSW的源码目录。

#### 1.导出环境变量

```
#6502环境导出
export TOOLCHAIN=arm-none-linux-gnueabi-
export CC=arm-none-linux-gnueabi-gcc CXX=arm-none-linux-gnueabi-g++ AR=arm-none-linux-gnueabi-ar RANLIB=arm-none-linux-gnueabi-ranlib
export BLDSHARED="${TOOLCHAIN}gcc -shared"
export LDSHARED="${TOOLCHAIN}gcc -shared"
```

```
#6657环境导出
export TOOLCHAIN=arm-linux-gnueabihf-
export CC=arm-linux-gnueabihf-gcc CXX=arm-linux-gnueabihf-g++ AR=arm-linux-gnueabihf-ar RANLIB=arm-linux-gnueabihf-ranlib
export BLDSHARED="${TOOLCHAIN}gcc -shared"
export LDSHARED="${TOOLCHAIN}gcc -shared"
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



