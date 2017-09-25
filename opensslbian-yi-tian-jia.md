OpenSSL交叉编译



```
./config no-asm shared --prefix=/usr/local/ssl \
    --cross-compile-prefix=/usr/local/arm/4.8.3/bin/arm-none-linux-gnueabi-
```



