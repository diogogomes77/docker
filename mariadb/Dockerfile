FROM diogogomes77/debian:latest
MAINTAINER Diogo Gomes <diogo.gomes77@gmail.com>
ENV MARIADB_DB NONE
ENV MARIADB_USER docker
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys CBCB082A1BB943DB && \
	echo "deb http://ftp.osuosl.org/pub/mariadb/repo/10.0/debian/ wheezy main" > /etc/apt/sources.list.d/mariadb.list && \
	apt-get update && \
	apt-get install -y mariadb-server && \
	apt-get clean && \
	echo -n > /var/lib/apt/extended_states
RUN sed -i -e "s/^bind-address/#bind-address/" /etc/mysql/my.cnf && \
	sed -i -e "s/^datadir.*=.*/datadir = \/data/" /etc/mysql/my.cnf && \
	sed -i -e "s/^innodb_buffer_pool_size.*=.*/innodb_buffer_pool_size = 64M/" /etc/mysql/my.cnf
ADD config /config
ADD supervisord.conf /etc/supervisor/conf.d/mariadb.conf
EXPOSE 3306
