---
title:  "Continuous Deploy Your Private Repo From Github"
date:   2015-10-06 23:25:19
categories: Server
tags: CI
author: Bigruan
---

### Assume:

1. You have a private repo at Github
2. You have a VPS(Ubuntu 14.04), e.g.,DigitalOcean
3. It's a Nodejs project, which means that you need to run npm
4. You use `gulp` or `grunt` or whatever building tools
5. Your app is running under `Apache2`, it means the default user `www-data` of `Apache` don't have permission to run some command.

### You want:

Every time there is push, deploy it to your VPS and run building scripts.

### Steps:

1. Make sure owner of */var/www/* is *www-data* (default Apache user). If not
```bash
sudo chown -R www-data:www-data /var/www/
```

2. Do ssh authentication for git, so that it won't ask for user&pass
```bash
sudo -Hu www-data mkdir /var/www/.ssh
sudo -Hu www-data ssh-keygen -t rsa -C "your@email.com" # use your github email
sudo -Hu www-data cat /var/www/.ssh/id_rsa.pub #copy it
open https://github.com/settings/ssh #paste the ssh key here
# clone the repo use ssh url:
git clone git@github.com:<user>/<repo>.git

# type *ssh -T git@github.com* if you see something like:
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
# you are now authenticated!
```

3. Upgrade nodejs to a proper version
```bash
sudo apt-get install nodejs
sudo apt-get install npm

sudo npm cache clean -f
sudo npm install -g n
sudo n stable
sudo ln -sf /usr/local/n/versions/node/<VERSION>/bin/node /usr/bin/node
```
4. Let *www-data* has permission to run *npm*
```bash
sudo visudo
# add this to the file
www-data    ALL=NOPASSWD: /usr/bin/npm
```

5. Add webhook to your private repo
```
open https://github.com/<user>/<repo>/settings/hooks/new
add the link to your deploy script, for example:
http://your.domain/deploy.php
```

6. Add *deploy.php*
```php
<?php
try
{
  $payload = json_decode($_REQUEST['payload']);
}
catch(Exception $e)
{
  exit(0);
}

//log the request
file_put_contents('logs/github.txt', print_r($payload, TRUE), FILE_APPEND);


if ($payload->ref === 'refs/heads/master')
{
  // path to your site deployment script
  exec('./build.sh');
}

?>
```
e.g.,build.sh
```bash
#!/bin/bash
cd /var/www/oupai365/

git pull origin master
npm install
./node_modules/bower/bin/bower install
./node_modules/gulp/bin/gulp.js vendor
./node_modules/gulp/bin/gulp.js build
./node_modules/gulp/bin/gulp.js
```

