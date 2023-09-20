FROM eoelab.org:1032/build-image-stacks/mcsm-image-stacks/mcsm:base

LABEL maintainer="Pd.ch <cpd233@outlook.com>"

EXPOSE 24444

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

RUN apt-get update --yes && apt-get install --yes --no-install-recommends openjdk-17-jre-headless && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    git clone --single-branch -b master --depth 1 https://gitee.com/MCSManager/MCSManager-Daemon-Production /opt/docker-mcsm/releases/daemon && \
    cd /opt/docker-mcsm/releases/daemon && npm i --production --registry=https://registry.npmmirror.com

WORKDIR /opt/docker-mcsm/releases/daemon

CMD node app.js
