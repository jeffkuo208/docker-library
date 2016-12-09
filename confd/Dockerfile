FROM alpine:3.4

ENV GOPATH /go

RUN mkdir -p "$GOPATH/src/" "$GOPATH/bin" && chmod -R 777 "$GOPATH" && \
    mkdir -p /go/src/github.com/kelseyhightower/confd

RUN echo "http://mirrors.aliyun.com/alpine/v3.4/main" > /etc/apk/repositories && \
    echo "http://mirrors.aliyun.com/alpine/v3.4/community" >> /etc/apk/repositories && \
	apk --update add go bash && \
    ln -s /go/src/github.com/kelseyhightower/confd /app

WORKDIR /app
