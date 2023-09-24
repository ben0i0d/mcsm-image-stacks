FROM eoelab.org:1032/build-image-stacks/mcsm-image-stacks/mcsm:base

LABEL maintainer="Pd.ch <cpd233@outlook.com>"

EXPOSE 24444

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

COPY adoptium.gpg /tmp/adoptium.gpg

RUN cat /tmp/adoptium.gpg | tee /etc/apt/keyrings/adoptium.asc  && \
    echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://mirrors.tuna.tsinghua.edu.cn/Adoptium/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list  && \
    apt-get update --yes && apt-get install --yes --no-install-recommends temurin-17-jre temurin-11-jre temurin-8-jre  && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    git clone --single-branch -b master --depth 1 https://gitee.com/MCSManager/MCSManager-Daemon-Production /opt/docker-mcsm/releases/daemon && \
    cd /opt/docker-mcsm/releases/daemon && npm i --production --registry=https://registry.npmmirror.com

WORKDIR /opt/docker-mcsm/releases/daemon

CMD node app.js
