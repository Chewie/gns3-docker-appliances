FROM centos:7

ENV container docker

RUN yum install -y epel-release

RUN yum install -y iproute2 dhclient vim \
    nano bind-utils net-tools \
    nginx \
    && yum clean all

# Remove networking scripts that came with networking packages
RUN rm -f /etc/rc.d/**/network

# Remove unnecessary bloat, as suggest by the official image docs
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*; \
ln -s /lib/systemd/system/console-getty.service \
/lib/systemd/system/multi-user.target.wants;

# Enable autologin as root
COPY console-getty.override.conf /etc/systemd/system/console-getty.service.d/override.conf

# Add /etc/shadow entry for root
COPY shadow /etc/shadow

# Persist configuration files for GNS3
VOLUME /etc

CMD ["/usr/sbin/init"]
