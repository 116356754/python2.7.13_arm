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

* ## 修改Python-2.7.13的setup.py

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

* ## 编译X86版本PYTHON

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



