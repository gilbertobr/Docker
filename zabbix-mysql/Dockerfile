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
RUN echo "LANG=en_US.utf8" > /etc/locale.conf
RUN echo "LC_ALL=en_US.UTF-8" >> /etc/locale.conf
RUN yum install -y deltarpm
RUN yum update -y
RUN rpm -Uvh https://repo.zabbix.com/zabbix/4.4/rhel/7/x86_64/zabbix-release-4.4-1.el7.noarch.rpm
RUN yum clean all
RUN yum -y install zabbix-server-mysql zabbix-web-mysql zabbix-apache-conf zabbix-agent
RUN mysql -u root -pmypassword -e "create database zabbix character set utf8 collate utf8_bin;"
RUN mysql -u root -pmypassword -e "grant all privileges on zabbix.* to zabbix@localhost identified by 'mypassword';"
RUN zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -uzabbix -p zabbix
RUN sed -i "126s/^/DBPassword=mypassword" /etc/zabbix/zabbix_server.conf
RUN sed -i "20s/^/php_value date.timezone America/Sao_Paulo" /etc/httpd/conf.d/zabbix.conf
RUN systemctl restart zabbix-server zabbix-agent httpd
RUN systemctl enable zabbix-server zabbix-agent httpd
VOLUME /var/lib/mysql

EXPOSE 22/tcp 80/tcp 3306/tcp 10050/tcp 10051/tcp 10052/tcp 10053/tcp 10050/udp 10051/udp 10052/udp 10053/udp
