FROM centos:latest
LABEL key="Author" name="https://github.com/umbraesoulsbane/"

RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install httpd && \
	yum -y install unzip && \
	yum -y install ant  && \
	yum -y install git && \
	yum -y install curl && \
	yum -y install maven && \
	yum -y install wget && \
	yum -y install java-1.8.0-openjdk && \
    yum clean all

# Forked VSAQ Repo (https://github.com/google/vsaq) to correct submodule dependancies and allow for customization.
RUN	git clone --recursive https://github.com/umbraesoulsbane/vsaq/ /var/vsaq

# Local Development - Patch in custom files WIP
# RUN rm /var/vsaq/vsaq/static/*.*
# COPY ./vsaq/static/*.* /var/vsaq/vsaq/static/
RUN rm /var/vsaq/client_side_only_impl/*.*
COPY ./vsaq/client_side_only_impl/*.* /var/vsaq/client_side_only_impl/

WORKDIR /var/vsaq
RUN ./do.sh install_deps
RUN ./do.sh check_deps
RUN ./do.sh build
# RUN ./do.sh build_prod
RUN cp -r build/. /var/www/html/
# RUN ./do.sh run

EXPOSE 80

# Simple startup script to avoid some issues observed with container restart
ADD ./srv/run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
