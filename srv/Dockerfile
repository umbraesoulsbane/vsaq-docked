FROM centos:7
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

RUN	git clone --recursive https://github.com/google/vsaq /var/vsaq
# install_deps/check_deps seems to exclude some deps
RUN git clone https://github.com/google/safe-html-types /var/vsaq/third_party/safe-html-types
RUN git clone https://github.com/google/closure-templates /var/vsaq/third_party/closure-templates

WORKDIR /var/vsaq
RUN ./do.sh install_deps
RUN ./do.sh check_deps
RUN ./do.sh build
RUN cp -r build/. /var/www/html/
#RUN ./do.sh run

EXPOSE 80

# Simple startup script to avoid some issues observed with container restart
ADD ./srv/run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
