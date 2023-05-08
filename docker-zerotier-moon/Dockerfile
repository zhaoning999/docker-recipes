ARG ALPINE_VERSION=edge

# FROM alpine:${ALPINE_VERSION}
FROM debian
ARG ZT_VERSION=1.10.0

LABEL maintainer="seedgou <seedgou@gmail.com>"

RUN apt update && apt install -y bash curl procps && curl -s https://install.zerotier.com | bash

COPY startup.sh /startup.sh
EXPOSE 9993

ENTRYPOINT ["/startup.sh"]
