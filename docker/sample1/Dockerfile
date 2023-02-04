FROM python:3.11
ENV PYTHONBUFFERED 1

# サービス名：サービスごとに変える
ENV SERVICE_NAME "sample1" 

# 言語設定
RUN apt-get update \
    && apt-get install -y locales \
    && locale-gen ja_JP.UTF-8 \
    && echo "export LANG=ja_JP.UTF-8" >> ~/.bashrc 

# X11の設定
RUN apt-get update -y\
    && apt-get install x11-apps -y
ENV DISPLAY host.docker.internal: 0.0


# Python
WORKDIR /${SERVICE_NAME}
ADD docker/${SERVICE_NAME}/etc/requirements.txt /${SERVICE_NAME}
RUN apt-get -y update \
    && apt-get -y install \
        apt-utils \
        gcc \
    && apt-get clean  \
    && rm -rf /var/lib/apt/lists/* \
    && pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt
