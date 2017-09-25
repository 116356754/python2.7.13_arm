## python2.7.13在6502平台上编译

首先将python2.7.13解压到虚拟机中，

```bash
#解压
tar -xf Python-2.7.13.tar.xz
```

在解压的Python-2.7.13平级目录再新建两个目录

```bash
#创建python2_7_13_for_x86_64
mkdir python2_7_13_for_x86_64
```

```bash
#创建python2_7_13_for_arm
mkdir python2_7_13_for_arm
```

* ### 修改Python-2.7.13的setup.py

在python2.7.13解压的文件夹名称为Python-2.7.13下面有个setup.py文件，对该文件进行修改，注释掉236行与237行代码，如下所示：

```
@@ -233,8 +239,8 @@ class PyBuildExt(build_ext):

             # If a module has already been built statically,
             # don't build it here
-            if ext.name in sys.builtin_module_names:
-                self.extensions.remove(ext)
+            #if ext.name in sys.builtin_module_names:
+            #    self.extensions.remove(ext)

         # Parse Modules/Setup and Modules/Setup.local to figure out which
         # modules are turned on in the file.
```

* ### 编译X86版本PYTHON

#### 1.进入python2\_7\_13\_for\_x86\_64/目录，然后执行如下脚本：

    ../Python-2.7.13/configure --prefix=`pwd`

#### 2.编译

```
make -j4
```

#### 3.安装

```
make install
```

* ### 交叉编译

#### 1.打补丁

交叉编译的第一步是为python源码打上交叉编译用的patch：[Python-2.7.13-compile.patch.tar.gz](http://files.cnblogs.com/files/pengdonglin137/Python-2.7.13-xcompile.patch.tar.gz)，将补丁文件解压并放置在python2\_7\_13\_for\_arm文件夹中，进入到Python-2.7.13目录中，

```
patch -p1 < ../python2_7_13_for_arm/Python-2.7.13-xcompile.patch
```

#### 2.导出环境变量

```
export CC=arm-none-linux-gnueabi-gcc CXX=arm-none-linux-gnueabi-g++ \
 AR=arm-none-linux-gnueabi-ar RANLIB=arm-none-linux-gnueabi-ranlib
```

#### 3.配置

进入到python2\_7\_13\_for\_arm文件夹中

    cd python2_7_13_for_arm

    ../Python-2.7.13/configure --prefix=`pwd` \
        --host=arm-none-linux-gnueabi \
        --build=x86_64-linux-gnu \
        --enable-ipv6 \
        --enable-shared \
        ac_cv_file__dev_ptmx="yes" \
        ac_cv_file__dev_ptc="no"

#### 4.编译

```
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

    make install HOSTPYTHON=../python2_7_13_for_x86_64/python \
        BLDSHARED="arm-none-linux-gnueabi-gcc -shared" \
        CROSS_COMPILE=arm-none-linux-gnueabi- \
        CROSS_COMPILE_TARGET=yes \
        prefix=`pwd`



