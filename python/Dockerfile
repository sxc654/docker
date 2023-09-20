FROM python:3.8.3-alpine

#******************更换Alpine源为mirrors.ustc.edu.cn******************
RUN echo https://mirrors.ustc.edu.cn/alpine/v3.11/main > /etc/apk/repositories && \
    echo https://mirrors.ustc.edu.cn/alpine/v3.11/community >> /etc/apk/repositories

RUN apk update \
    && apk add --no-cache git curl libmcrypt libmcrypt-dev openssh-client rsync g++ make autoconf supervisor tzdata \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone

# This hack is widely applied to avoid python printing issues in docker containers.
# See: https://github.com/Docker-Hub-frolvlad/docker-alpine-python3/pull/13
ENV PYTHONUNBUFFERED=1

ENV PIP_ROOT_USER_ACTION=ignore

RUN echo "**** install Python ****" && \
    apk add --update --no-cache py3-configobj py3-setuptools python3 python3-dev && \
    if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi

RUN echo "**** install pip ****" && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache --upgrade pip wheel && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi
