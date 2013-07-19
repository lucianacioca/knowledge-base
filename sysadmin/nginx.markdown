
# NGINX with FastCGI #

- <http://wiki.nginx.org/HttpFastcgiModule>
- <http://php-fpm.org/wiki/Main_Page>

Install packages :

~~~~~
aptitude install php5-fpm nginx-extras
~~~~~

Example of NGINX configuration :

~~~~~
# /etc/nginx/sites-enabled/example

server {
	server_name www.example.com;
	root /home/example/htdocs;
	index index.html index.php;
	location ~* \.php$ {
		fastcgi_pass unix:/home/example/php5-fpm.sock;
		include fastcgi_params;
	}
}
~~~~~

Example of FastCGI configuration :

~~~~~
# /etc/php5/fpm/pool.d/example.conf 

[example]
prefix=/home/example
user = www-data
group = example
access.log = /home/example/log/access.log
slowlog = log/slow.log
request_slowlog_timeout = 30
;chroot = $prefix

pm = dynamic
pm.max_children = 5
pm.start_servers = 2
pm.min_spare_servers = 1
pm.max_spare_servers = 3
pm.status_path = /status
ping.path = /ping

listen = php5-fpm.sock
listen.owner = example
listen.group = example
listen.mode = 0660

php_admin_value[error_log] = /home/example/log/php.log
php_admin_flag[log_errors] = on
php_flag[display_errors] = off
~~~~~

