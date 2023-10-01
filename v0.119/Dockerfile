FROM registry.access.redhat.com/ubi9/ubi-minimal:9.2

MAINTAINER Vadim Rutkovsky <vadim@vrutkovs.eu>

LABEL io.openshift.s2i.scripts-url=image:///usr/libexec/s2i

EXPOSE 8080

RUN mkdir -p /opt/app-root/src/static && \
    chmod -R og+rwx /opt/app-root && \
    chown -R 1001:0 /opt/app-root && \
    mkdir -p /usr/libexec/s2i

WORKDIR /opt/app-root/src

ENV VERSION 0.119.0

RUN microdnf install --refresh -y git-core golang nginx tar && \
    mkdir -p /tmp/hugo && \
    curl -sL https://github.com/gohugoio/hugo/releases/download/v${VERSION}/hugo_extended_${VERSION}_Linux-64bit.tar.gz | \
      tar xvzf - -C /tmp/hugo && \
    cp /tmp/hugo/hugo /usr/local/bin/hugo && \
    rm -rf /tmp/hugo && \
    microdnf clean all

COPY ./s2i/* /usr/libexec/s2i/
USER 1001
