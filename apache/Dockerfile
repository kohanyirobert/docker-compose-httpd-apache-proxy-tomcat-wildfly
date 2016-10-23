FROM httpd:2-alpine
ENV _HTTPD_DIR /usr/local/apache2
RUN sed -i 's,^#\(LoadModule proxy_module modules/mod_proxy.so\)$,\1,' $_HTTPD_DIR/conf/httpd.conf
RUN sed -i 's,^#\(LoadModule proxy_ajp_module modules/mod_proxy_ajp.so\)$,\1,' $_HTTPD_DIR/conf/httpd.conf
RUN sed -i 's,^#\(LoadModule ssl_module modules/mod_ssl.so\)$,\1,' $_HTTPD_DIR/conf/httpd.conf
RUN sed -i 's,^#\(LoadModule socache_shmcb_module modules/mod_socache_shmcb.so\)$,\1,' $_HTTPD_DIR/conf/httpd.conf
RUN sed -i 's,^#\(Include conf/extra/httpd-ssl.conf\)$,\1,' $_HTTPD_DIR/conf/httpd.conf
RUN echo 'Include conf/other/*.conf' >> $_HTTPD_DIR/conf/httpd.conf
RUN mkdir -p $_HTTPD_DIR/conf/other
RUN echo 'ProxyRequests Off' > $_HTTPD_DIR/conf/other/ajp.conf
RUN echo "ProxyPass / ajp://tomcat.$COMPOSE_PROJECT_NAME:8009/" >> $_HTTPD_DIR/conf/other/ajp.conf
RUN echo "ProxyPassReverse / ajp://tomcat.$COMPOSE_PROJECT_NAME:8009/" >> $_HTTPD_DIR/conf/other/ajp.conf
RUN apk update
RUN apk add openssl
RUN openssl req -x509 -nodes -days 1 -newkey rsa:2048 -subj /CN=* -keyout /usr/local/apache2/conf/server.key -out /usr/local/apache2/conf/server.crt
RUN apk del openssl
