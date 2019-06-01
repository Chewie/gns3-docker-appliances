FROM centos:7

ENV container docker

RUN yum install -y epel-release

RUN yum install -y iproute2 dhclient vim \
    nano bind-utils net-tools \
    && yum clean all

# Remove networking scripts that came with networking packages
RUN rm -f /etc/rc.d/**/*

# Enable autologin as root
COPY console-getty.override.conf /etc/systemd/system/console-getty.service.d/override.conf

# Persist configuration files for GNS3
VOLUME /etc

VOLUME ["/sys/fs/cgroup"]

CMD ["/usr/sbin/init"]
