
======
Vtiger
======

Installation notes with NGINX + FPM
===================================

1. Increase ``fastcgi_read_timeout`` to e.g. 3000.

2. Define : ::

    php_admin_value[error_reporting] = E_WARNING & ~E_NOTICE & ~E_DEPRECATED

