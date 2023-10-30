FROM eoelab.org:1032/build-image-stacks/mcsm-image-stacks/mcsm:base

LABEL maintainer="Pd.ch <cpd233@outlook.com>"

EXPOSE 24444

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

RUN curl -s https://repos.azul.com/azul-repo.key | gpg --dearmor -o /usr/share/keyrings/azul.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/azul.gpg] https://repos.azul.com/zulu/deb stable main" | tee /etc/apt/sources.list.d/zulu.list && \
    apt-get update --yes && apt-get install --yes --no-install-recommends zulu17-ca-jre-headless zulu11-ca-jre-headless zulu8-ca-jre-headless  && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    ln -s /usr/lib/jvm/zulu17/bin/java /usr/bin/java17 && \
    ln -s /usr/lib/jvm/zulu11/bin/java /usr/bin/java11 && \
    ln -s /usr/lib/jvm/zulu8/bin/java /usr/bin/java8 && \
    git clone --single-branch -b master --depth 1 https://gitee.com/MCSManager/MCSManager-Daemon-Production /opt/docker-mcsm/releases/daemon && \
    cd /opt/docker-mcsm/releases/daemon && npm i --production --registry=https://registry.npmmirror.com

WORKDIR /opt/docker-mcsm/releases/daemon

CMD node app.js
