FROM centos:7
MAINTAINER The CentOS Project <cloud-ops@centos.org>
LABEL Vendor="CentOS" \
      License=GPLv2 \
      Version=2.4.6-40


RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install httpd && \
    yum -y --setopt=tsflags=nodocs install glibc.i686 && \
    yum -y --setopt=tsflags=nodocs install libgcc.i686 && \
    yum -y --setopt=tsflags=nodocs install wget curl unzip && \
    yum clean all && \
    rm -rf /var/cache/yum

RUN mkdir -p /usr/local/livecode && cd /usr/local/livecode && \
    wget "http://livecodestatic.com/downloads/livecode/8_1_6/LiveCodeCommunityServer-8_1_6-Linux-x86_64.zip" && \
    unzip LiveCodeCommunityServer-8_1_6-Linux-x86_64.zip && \
    chmod 755 livecode-community-server

EXPOSE 8080

COPY httpd/httpd.conf /etc/httpd/conf/httpd.conf

ENV APACHE_RUN_USER apache
ENV APACHE_RUN_GROUP apache
ENV APACHE_LOG_DIR /var/log/httpd
ENV APACHE_RUN_DIR=/var/run/httpd

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
