FROM centos:7
USER root

RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
RUN yum update -y
RUN yum install unzip net-tools sysstat openssh-clients libaio nmap-ncat libstdc++.so.6 vim screen curl gmp libidn wget nano make nc libtool-ltdl glibc ntp perl-core perl w3m bind-utils nmap sed libaio rsync telnet aspell -y
RUN mkdir /zimbra_installer && cd /zimbra_installer && wget https://files.zimbra.com/downloads/8.8.15_GA/zcs-8.8.15_GA_3869.RHEL7_64.20190918004220.tgz
RUN cd /zimbra_installer && tar zxpvf zcs-8.8.15_GA_3869.RHEL7_64.20190918004220.tgz

# Para iniciar serviços
CMD ["/usr/sbin/init"]
