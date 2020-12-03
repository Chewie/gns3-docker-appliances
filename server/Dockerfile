FROM centos:8

ENV container docker

RUN yum install -y epel-release

RUN yum install -y iproute dhclient vim \
    nano bind-utils net-tools \
    nginx \
    && yum clean all \
    && rm -rf /var/cache/yum

# Remove networking scripts that came with networking packages
RUN rm -rf /etc/rc.d/**/network /etc/sysconfig/network-scripts

# Remove unnecessary bloat, as suggested by the official image docs
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*; \
systemctl unmask console-getty; \
ln -s /lib/systemd/system/systemd-user-sessions.service \
/lib/systemd/system/multi-user.target.wants; \
ln -s /lib/systemd/system/console-getty.service \
/lib/systemd/system/multi-user.target.wants; \
systemctl enable nginx

# Enable autologin as root
COPY console-getty.override.conf /etc/systemd/system/console-getty.service.d/override.conf

# Add /etc/shadow entry for root
COPY shadow /etc/shadow

# Change the default colorscheme, because solarputty is shit
RUN echo 'colorscheme desert' > /root/.vimrc

# Use a custom conf to answer with remote addr and hostname
COPY nginx.conf /etc/nginx/nginx.conf

# Persist configuration files for GNS3
VOLUME /etc/sysconfig

CMD ["/usr/sbin/init"]
