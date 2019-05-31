FROM centos:7

ENV container docker

RUN yum install -y epel-release iproute2 dhclient vim \
    nano bind-utils net-tools \
    dhcp bind bird2
    && yum clean all

# Enable autologin as root
COPY console-getty.override.conf /etc/systemd/system/console-getty.service.d/override.conf

CMD ["/usr/sbin/init"]
