
NGINX
=====

Ressources
----------

List of directives : http://nginx.org/en/docs/dirindex.html

Configuring Your LEMP System (Linux, nginx, MySQL, PHP-FPM) For Maximum Performance : http://www.howtoforge.com/configuring-your-lemp-system-linux-nginx-mysql-php-fpm-for-maximum-performance

High performance web server with Nginx and PHP-FPM : http://lukasz.cepowski.com/devlog/43,high-performance-web-server-with-nginx-and-php-fpm

Optimizations
-------------

Set ``worker_processes`` equal to the number of cores.

Enable ``sendfile``, ``tcp_nopush``, ``tcp_nodelay`` (by default on Debian).

Lower ``keepalive_timeout``.

