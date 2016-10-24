# docker-compose-httpd-apache-proxy-tomcat-wildfly

Simple [`docker-compose`] setup that starts an [`httpd`] server that proxies
HTTP and HTTPS requests towards a [`tomcat`] or a [`wildfly`] server over [AJP].

[`docker-compose`]: https://docs.docker.com/compose/
[`httpd`]: https://httpd.apache.org/
[`tomcat`]: https://tomcat.apache.org/
[`wildfly`]: http://wildfly.org/
[AJP]: https://en.wikipedia.org/wiki/Apache_JServ_Protocol
