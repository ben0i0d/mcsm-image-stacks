FROM eoelab.org:1032/mirrored-sources/mirrored-sources/debian:bookworm

LABEL maintainer="Pd.ch <cpd233@outlook.com>"

EXPOSE 24444

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Configure environment
ENV DEBIAN_FRONTEND=noninteractive \
    TZ=Asia/Shanghai

# Copy files
COPY cert/eoelab.org.crt /usr/local/share/ca-certificates/eoelab.org.crt

RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update --yes && apt-get upgrade --yes && \
    apt-get install --yes --no-install-recommends ca-certificates locales git zip unzip nodejs npm openjdk-17-jre-headless && \
    update-ca-certificates && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && locale-gen && \
    git clone --single-branch -b master --depth 1 https://gitee.com/MCSManager/MCSManager-Daemon-Production /opt/docker-mcsm/releases/daemon && \
    cd /opt/docker-mcsm/releases/daemon && npm i --production --registry=https://registry.npmmirror.com

WORKDIR /opt/docker-mcsm/releases/daemon

CMD node app.js
