FROM eoelab.org:1032/build-image-stacks/mcsm-image-stacks/mcsm:base

LABEL maintainer="Pd.ch <cpd233@outlook.com>"

EXPOSE 23333

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

RUN git clone --single-branch -b master --depth 1 https://gitee.com/MCSManager/MCSManager-Web-Production /opt/docker-mcsm/releases/web && \
    cd /opt/docker-mcsm/releases/web && npm i --production --registry=https://registry.npmmirror.com

WORKDIR /opt/docker-mcsm/releases/web

CMD node app.js