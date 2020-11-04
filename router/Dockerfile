FROM centos:8

ENV container docker

RUN yum install -y epel-release

RUN yum install -y iproute dhclient vim \
    nano bind-utils net-tools \
    dhcp-relay dhcp-server bird iptables-services radvd \
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
/lib/systemd/system/multi-user.target.wants;\
ln -s /lib/systemd/system/console-getty.service \
/lib/systemd/system/multi-user.target.wants;


# Enable autologin as root
COPY console-getty.override.conf /etc/systemd/system/console-getty.service.d/override.conf

# Add /etc/shadow entry for root
COPY shadow /etc/shadow

COPY iptables_default /etc/sysconfig/iptables

# Enable iptables restore at boot
RUN mkdir -p /etc/systemd/system/basic.target.wants; \
ln -s /usr/lib/systemd/system/iptables.service /etc/systemd/system/basic.target.wants/iptables.service

# Store bird config in /etc/bird/bird.conf instead of /etc/bird.conf
COPY bird.override.conf /etc/systemd/system/bird.service.d/override.conf
RUN mkdir -p /etc/bird && mv /etc/bird.conf /etc/bird/bird.conf

# Change the default colorscheme, because solarputty is shit
RUN echo 'colorscheme desert' > /root/.vimrc

# Persist configuration files for GNS3
VOLUME /etc/sysconfig
VOLUME /etc/bird

CMD ["/usr/sbin/init"]
