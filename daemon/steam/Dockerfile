FROM eoelab.org:1032/build-image-stacks/mcsm-image-stacks/mcsm:base

LABEL maintainer="Pd.ch <cpd233@outlook.com>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

#COPY conf/debian.sources /etc/apt/sources.list.d/debian.sources

RUN sed -i 's/main/main contrib non-free non-free-firmware/g' /etc/apt/sources.list.d/debian.sources &&\
    echo steam steam/question select "I AGREE" | debconf-set-selections &&\
    echo steam steam/license note '' | debconf-set-selections &&\
    dpkg --add-architecture i386 &&\
    apt-get update --yes && apt-get install --yes --no-install-recommends steamcmd &&\
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    ln -s /usr/games/steamcmd /usr/bin/steamcmd && steamcmd +quit && \
    git clone --single-branch -b master --depth 1 https://gitee.com/MCSManager/MCSManager-Daemon-Production /opt/docker-mcsm/releases/daemon && \
    cd /opt/docker-mcsm/releases/daemon && npm i --production --registry=https://registry.npmmirror.com

WORKDIR /opt/docker-mcsm/releases/daemon

CMD node app.js
