FROM eoelab.org:1032/mirrored-sources/mirrored-sources/debian:bookworm

LABEL maintainer="Pd.ch <cpd233@outlook.com>"

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

USER root

# Configure environment
ENV DEBIAN_FRONTEND=noninteractive \
    LANG=zh_CN.UTF-8 \
    LANGUAGE=zh_CN.UTF-8 \
    LC_ALL=zh_CN.UTF-8 \
    TZ=Asia/Shanghai

# Copy files
COPY cert/cert.pem /usr/local/share/ca-certificates/eoelab.org.crt

RUN sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list.d/debian.sources && \
    apt-get update --yes && apt-get upgrade --yes && \
    apt-get install --yes --no-install-recommends ca-certificates gnupg curl locales git zip unzip nodejs npm && \
    update-ca-certificates && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "zh_CN.UTF-8 UTF-8">/etc/locale.gen && locale-gen