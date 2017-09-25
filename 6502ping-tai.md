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

* ## 编译X86版本PYTHON

进入python源码目录，执行：

```
./configure
```



