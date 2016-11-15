# docker-compose-httpd-apache-proxy-tomcat-wildfly

Simple [`docker-compose`] setup that starts an [`httpd`] server that proxies
HTTP and HTTPS requests towards a [`tomcat`] or a [`wildfly`] server over [AJP].

## Example

Example configuration for a Debian-based Apache installation using Let's Encrypt.

```
<IfModule mod_ssl.c>
        <VirtualHost *:443>
                ServerName <DOMAIN>
                ServerAdmin webmaster@localhost
                ErrorLog ${APACHE_LOG_DIR}/error.log
                CustomLog ${APACHE_LOG_DIR}/access.log combined
                SSLEngine on
                SSLCertificateFile      /etc/letsencrypt/live/<DOMAIN>/fullchain.pem
                SSLCertificateKeyFile /etc/letsencrypt/live/<DOMAIN>/privkey.pem
                ProxyRequests Off
                # Last slash is required!!!
                ProxyPass / ajp://localhost:8009/<CONTEXT_PATH>/
                ProxyPassReverse / ajp://localhost:8009/<CONTEXT_PATH>/
        </VirtualHost>
</IfModule>
```

`<DOMAIN>` is your domain name for which you have Let's Encrypt issued a certificate.
`<CONTEXT_PATH>` is the context path of the web-application (don't forget that the
closing slash).

[`docker-compose`]: https://docs.docker.com/compose/
[`httpd`]: https://httpd.apache.org/
[`tomcat`]: https://tomcat.apache.org/
[`wildfly`]: http://wildfly.org/
[AJP]: https://en.wikipedia.org/wiki/Apache_JServ_Protocol
