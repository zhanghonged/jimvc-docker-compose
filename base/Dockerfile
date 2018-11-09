FROM python:2.7
LABEL maintaner="Zhang Hong zhanghonged@126.com"

ARG PYPI
ARG JIMVC_PATH
ARG JIMVC_DOWNLOAD_URL
ARG DBNAME
ARG DBHOST
ARG DBUSER
ARG DBPASSWORD
ARG REDISHOST
ARG REDISPASSWORD

# 设置系统时区
RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

# 本地拷贝包
#COPY master.tar.gz /
#RUN set -x \
#        && mkdir /run/jimv \
#        && mkdir -p $JIMVC_PATH \
#        && mkdir -p /opt/templates \
#        && tar -zxf /master.tar.gz --strip-components 1 -C ${JIMVC_PATH}

# 从github下载包
RUN set -x  \
        && mkdir /run/jimv \
        && mkdir -p $JIMVC_PATH \
        && mkdir -p /opt/templates \
        && curl -sL ${JIMVC_DOWNLOAD_URL} | tar -zxf - --strip-components 1 -C ${JIMVC_PATH}

WORKDIR ${JIMVC_PATH}

RUN grep -v "^$" requirements.txt | xargs -n 1 pip install -i $PYPI 

COPY jimvc.conf /etc/
COPY wait-for-it.sh $JIMVC_PATH

RUN set -x \ 
        && sed -i "s/DBNAME/$DBNAME/" /etc/jimvc.conf \
        && sed -i "s/DBHOST/$DBHOST/" /etc/jimvc.conf \
        && sed -i "s/DBUSER/$DBUSER/" /etc/jimvc.conf \
        && sed -i "s/DBPASSWORD/$DBPASSWORD/" /etc/jimvc.conf \
        && sed -i "s/REDISHOST/$REDISHOST/" /etc/jimvc.conf \
        && sed -i "s/REDISPASSWORD/$REDISPASSWORD/" /etc/jimvc.conf

CMD ["./wait-for-it.sh", "mysql:3306", "--","gunicorn" "-c" "gunicorn_config.py" "main:app"]
