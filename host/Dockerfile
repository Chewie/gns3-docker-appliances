FROM centos:7

ENV container docker

RUN yum install -y epel-release

RUN yum install -y iproute2 dhclient vim \
    nano bind-utils net-tools \
    && yum clean all

# Enable autologin as root
COPY console-getty.override.conf /etc/systemd/system/console-getty.service.d/override.conf

# Persist configuration files for GNS3
VOLUME /etc

VOLUME ["/sys/fs/cgroup"]

CMD ["/usr/sbin/init"]
