FROM alpine:3.12.0

ARG USERNAME
ARG PASSWORD

ENV SQUID_VERSION=4.11-r0
ENV TZ=Asia/Tokyo

RUN apk update \
 && apk add --no-cache \
      apache2-utils \
      squid=${SQUID_VERSION} \
      tzdata \
 && rm -rf /var/cache/apk/* \
 && cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
 && htpasswd -b -c /etc/squid/passwords ${USERNAME} ${PASSWORD}

COPY squid.conf /etc/squid/squid.conf
COPY blacklist /etc/squid/blacklist

EXPOSE 8080
USER squid
CMD  ["/usr/sbin/squid", "-Nd1"]
