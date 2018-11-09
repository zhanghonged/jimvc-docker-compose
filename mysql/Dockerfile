FROM mysql:5.6
LABEL maintaner="Zhang Hong zhanghonged@126.com"

# 更换163的源，下载curl和ca-certificates包
RUN set -x \
        && sed -i 's/^/#/g' /etc/apt/sources.list \
        && sed -i '1i\deb http://mirrors.163.com/debian/ jessie main non-free contrib\' /etc/apt/sources.list \
        && sed -i '1i\deb http://mirrors.163.com/debian/ jessie-updates main non-free contrib\' /etc/apt/sources.list \
        && sed -i '1i\deb http://mirrors.163.com/debian/ jessie-backports main non-free contrib\' /etc/apt/sources.list \
        && sed -i '1i\deb-src http://mirrors.163.com/debian/ jessie main non-free contrib\' /etc/apt/sources.list \
        && sed -i '1i\deb-src http://mirrors.163.com/debian/ jessie-updates main non-free contrib\' /etc/apt/sources.list \
        && sed -i '1i\deb-src http://mirrors.163.com/debian/ jessie-backports main non-free contrib\' /etc/apt/sources.list \
        && sed -i '1i\deb http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib\' /etc/apt/sources.list \
        && sed -i '1i\deb-src http://mirrors.163.com/debian-security/ jessie/updates main non-free contrib\' /etc/apt/sources.list \
        && apt-get update \
        && apt-get install -y ca-certificates \
        && apt-get install -y --no-install-recommends curl \
        && rm -rf /var/lib/apt/lists/*

# 设置系统时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone
        
# 下载数据库初始化脚本，并执行初始化
RUN curl -sL https://raw.githubusercontent.com/jamesiter/JimV-C/master/misc/init.sql -o /docker-entrypoint-initdb.d/init.sql

# 本地拷贝
#COPY init.sql /docker-entrypoint-initdb.d/
