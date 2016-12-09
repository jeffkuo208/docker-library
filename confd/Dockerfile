FROM alpine:3.3

ENV CONFD_VERSION="0.11.0" \
    CONFD_URL="https://github.com/kelseyhightower/confd/releases/download" \
    GLIBC_VERSION=2.23-r3 \
    LANG=C.UTF-8

	
RUN echo "http://mirrors.aliyun.com/alpine/v3.3/main" > /etc/apk/repositories  \
    && echo "http://mirrors.aliyun.com/alpine/v3.3/community" >> /etc/apk/repositories  \
	&& apk add --update -t deps openssl \
    && apk add --update bash \
	&& apk add --update libstdc++ curl ca-certificates bash  \
	&& cd /tmp \
    && for pkg in glibc-${GLIBC_VERSION} glibc-bin-${GLIBC_VERSION} glibc-i18n-${GLIBC_VERSION}; do curl https://code.aliyun.com/jeffg208/repo/raw/master/alpine/sgerrand/alpine-pkg-glibc/releases/${GLIBC_VERSION}/${pkg}.apk -o /tmp/${pkg}.apk; done  \
    && apk add --allow-untrusted /tmp/*.apk  \
    && rm -v /tmp/*.apk \
    && wget ${CONFD_URL}/v${CONFD_VERSION}/confd-${CONFD_VERSION}-linux-amd64 -O /bin/confd \
    && apk add --allow-untrusted ${GLIBC_PKG} ${GLIBC_BIN_PKG} \
    && ( /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 C.UTF-8 || true ) \
    && echo "export LANG=C.UTF-8" > /etc/profile.d/locale.sh  \
    && /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc-compat/lib  \
    && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' >> /etc/nsswitch.conf \
    && chmod +x /bin/confd \
    && apk del --purge deps \
    && rm -rf /tmp/* /var/cache/apk/*


ENTRYPOINT ["/bin/confd"]