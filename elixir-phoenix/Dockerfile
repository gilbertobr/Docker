FROM centos:7
USER root
RUN mkdir /app
ENV ACCESS_TOKEN desenv
ENV SECRET_TOKEN desenv
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
RUN yum install -y epel-release
RUN yum install -y curl vim wget git mariadb mariadb-server postgresql postgresql-server sqlite httpd sudo screen
RUN yum clean all
RUN yum install -y https://packages.erlang-solutions.com/erlang-solutions-1.0-1.noarch.rpm
RUN yum install -y wxBase.x86_64 gcc gcc-c++ glibc-devel make ncurses-devel openssl-devel autoconf java-1.8.0-openjdk-devel
RUN yum install -y openssh-server
RUN yum install -y esl-erlang
RUN mkdir /opt/elixir
RUN git clone https://github.com/elixir-lang/elixir.git /opt/elixir
RUN cd /opt/elixir && make && make install
RUN rm -f ~/.erlang.cookie
RUN mix local.hex --force && mix local.rebar --force
RUN curl -sL https://rpm.nodesource.com/setup_12.x | sudo -E bash -
RUN yum install -y inotify-tools
RUN mix archive.install --force hex phx_new 1.4.9
RUN yum update -y && yum clean all

EXPOSE 22
EXPOSE 80
EXPOSE 443
EXPOSE 3306
EXPOSE 5432
EXPOSE 4000

VOLUME /app /var/lib/pgsql/data /var/lib/mysql

# Para iniciar serviços
CMD ["/usr/sbin/init"]


#Para configurar o postgresql
#/usr/bin/postgresql-setup initdb
#sed -i "74s/^/local   all             postgres                                trust\n/" /var/lib/pgsql/data/pg_hba.conf
#sed -i "75s/^/host    all     all     0.0.0.0\/0                               md5\n/" /var/lib/pgsql/data/pg_hba.conf
#service postgresql start

#CRIAR USUARIO NO POSTGRESQL
#CREATE USER usuario_novo WITH SUPERUSER;
#GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO usuario_novo;
#GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO usuario_novo;
#ALTER USER usuario_novo WITH PASSWORD 'SENHA';
