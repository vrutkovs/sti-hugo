FROM golang:alpine

MAINTAINER Steve Morrissey <uberamd@gmail.com>

LABEL io.openshift.s2i.scripts-url=image:///usr/libexec/s2i

EXPOSE 8080

RUN mkdir -p /opt/app-root/src/static && \
    chmod -R og+rwx /opt/app-root && \
    chown -R 1001:0 /opt/app-root && \
    mkdir -p /usr/libexec/s2i

WORKDIR /opt/app-root/src

RUN apk add --update wget ca-certificates git openssl mercurial binutils && \
    update-ca-certificates && \
    mkdir -p /go/bin && \
    wget https://github.com/gohugoio/hugo/releases/download/v0.40.3/hugo_0.40.3_Linux-64bit.tar.gz && \
    tar xvzf hugo_0.40.3_Linux-64bit.tar.gz && \
    cp hugo_0.40.3_Linux-64bit/hugo /go/bin/hugo && \
    rm -rf hugo_0.40.3_Linux-64bit.tar.gz hugo_0.40.3_Linux-64bit && \
    strip /go/bin/hugo && \
    apk del git mercurial binutils  && \
    rm -rf /go/src /go/pkg

COPY ./s2i/* /usr/libexec/s2i/
USER 1001
