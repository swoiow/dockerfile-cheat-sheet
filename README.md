# dockerfile-cheat-sheet
A list of Dockerfile useful command.

---
> 设置语言

```
ENV LC_ALL=C.UTF-8 \
    LANG=C.UTF-8
```

---
> 设置[时区](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
```
ENV TZ=Asia/Shanghai
```

---
> 拷贝 ldd

```
ldd /usr/bin/env | grep "=> /" | awk '{print $3}' | xargs -I '{}' cp -L -n -v '{}' /tmp/libs/
```

---
> 安装 dumb-init

```
ADD https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64 /usr/local/bin/dumb-init
RUN chmod +x /usr/local/bin/dumb-init
```

---
> 删除 test pyc pyo

```
find /usr/local -depth \
    \( \
        \( -type d -a \( -name test -o -name tests \) \) \
        -o \
        \( -type f -a \( -name '*.pyc' -o -name '*.pyo' \) \) \
    \) -exec rm -rf '{}'
```

---
> alpine / debian / ubuntu (通用) 删除无用文件

```
rm -rf /root/.cache /tmp/* /var/lib/apt/* /var/cache/* /var/log/* 
```

---
> 设置 alpine 更新镜像 (Mirror)

- mirrors.aliyun.com
- mirrors.ustc.edu.cn
- mirrors.tuna.tsinghua.edu.cn

```
ARG MIRROR=mirrors.aliyun.com
ARG SOURCES="/etc/apk/repositories"
RUN sed -i 's/http/https/g' $SOURCES \
    && sed -i 's/dl-cdn.alpinelinux.org/'$MIRROR'/g' $SOURCES
```

---
> 设置 debian 更新镜像 (Mirror)

- mirrors.tuna.tsinghua.edu.cn
- mirrors.ustc.edu.cn
- mirrors.163.com
- mirrors.aliyun.com

```
ARG MIRROR=mirrors.ustc.edu.cn
ARG SOURCES="/etc/apt/sources.list"
RUN sed -i 's/deb.debian.org/'$MIRROR'/g' $SOURCES
```

---
> 设置 ubuntu 更新镜像 (Mirror)
