# Dockerfile for LiveCode Community Server on Centos 7 with Apache
FROM centos:7

LABEL com.inidus.version="0.0.1" \
      vendor="Inidus Limited" \
      description="LiveCode Server CE on Centos 7 with Apache"

ENV LIVECODE_VER=8_1_6
ENV LIVECODE_ZIP=LiveCodeCommunityServer-8_1_6-Linux-x86_64.zip

RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --disableplugin=fastestmirror --setopt=tsflags=nodocs install httpd wget curl unzip glibc.i686 libgcc.i686 && \
    yum clean all && \
    rm -rf /var/cache/yum

RUN mkdir -p /usr/local/livecode && cd /usr/local/livecode && \
    wget -q "http://livecodestatic.com/downloads/livecode/${LIVECODE_VER}/${LIVECODE_ZIP}" && \
    unzip ${LIVECODE_ZIP} && \
    chmod 755 livecode-community-server && \
    rm ${LIVECODE_ZIP}

EXPOSE 8080

COPY httpd/httpd.conf /etc/httpd/conf/httpd.conf

ENV APACHE_RUN_USER apache
ENV APACHE_RUN_GROUP apache
ENV APACHE_LOG_DIR /var/log/httpd
ENV APACHE_RUN_DIR=/var/run/httpd

# Simple startup script to avoid some issues observed with container restart
COPY run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
