# Dockerfile for xray based alpine
# Copyright (C) 2019 - 2020 Teddysun <i@teddysun.com>
# Reference URL:
# https://github.com/XTLS/Xray-core
# https://github.com/v2ray/v2ray-core
# https://github.com/v2ray/geoip
# https://github.com/v2ray/domain-list-community

FROM alpine:latest
LABEL maintainer="Teddysun <i@teddysun.com>"

WORKDIR /root
COPY xray.sh /root/xray.sh
COPY config.json /etc/xray/config.json
RUN set -ex \
	&& apk add --no-cache tzdata ca-certificates \
	&& mkdir -p /var/log/xray \
	&& chmod +x /root/xray.sh \
	&& /root/xray.sh \
	&& rm -fv /root/xray.sh \
	&& wget -O /usr/bin/geosite.dat https://github.com/v2fly/domain-list-community/releases/latest/download/dlc.dat \
	&& wget -O /usr/bin/geoip.dat https://github.com/v2fly/geoip/releases/latest/download/geoip.dat

VOLUME /etc/xray
ENV TZ=Asia/Shanghai
CMD [ "/usr/bin/xray", "-config", "/etc/xray/config.json" ]
