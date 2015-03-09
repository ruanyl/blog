---
title:  "Integrate django with apache2 via mod_wsgi"
date:   2013-12-23 21:07:51
categories: Server
tags: Django Python Apache
author: Bigruan
---

For django 1.6:

First, install mod_wsgi
```bash
~$ sudo apt-get install libapache2-mod-wsgi
```

Config virtual Host for Apache:

```bash
~$ sudo touch /etc/apache2/sites-available/appname.example.com
~$ sudo vim /etc/apache2/sites-available/appname.example.com
```

Add these:

```apacheconf
<VirtualHost *:80>
	ServerAdmin webmaster@localhost

	DocumentRoot /var/www/appname
	ServerName appname.example.com

    Alias /robots.txt /path/to/mysite.com/static/robots.txt
    Alias /favicon.ico /path/to/mysite.com/static/favicon.ico

    AliasMatch ^/([^/]*\.css) /path/to/mysite.com/static/styles/$1

    Alias /media/ /path/to/mysite.com/media/
    Alias /static/ /path/to/mysite.com/static/

    <Directory /path/to/mysite.com/static>
    Order deny,allow
    Allow from all
    </Directory>

    <Directory /path/to/mysite.com/media>
    Order deny,allow
    Allow from all
    </Directory>

    WSGIScriptAlias / /path/to/mysite.com/mysite/wsgi.py

    <Directory /path/to/mysite.com/mysite>
    <Files wsgi.py>
    Order allow,deny
    Allow from all
    </Files>
    </Directory>

	ErrorLog ${APACHE_LOG_DIR}/appname.example.com-error.log
	CustomLog ${APACHE_LOG_DIR}/appname.example.com-access.log combined

	LogLevel warn
</VirtualHost>
```

Then enable this site:
```bash
~$ sudo a2ensite appname.example.com
~$ sudo /etc/init.d/apache2 restart
```

Add the django project path to System Path of Ubuntu.
```python
import os,sys
#Add the path of django project to System Path
sys.path.append('/home/username/path/to/djangoproject')
os.environ.setdefault("DJANGO_SETTINGS_MODULE", "djangoproject.settings")

from django.core.wsgi import get_wsgi_application
application = get_wsgi_application()
```
