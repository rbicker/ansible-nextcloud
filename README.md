rbicker.nextcloud
=================

* install Nextcloud on CentOS 7 and 8
* tested for versions 14 - 20
* install dependencies: nginx, php7.3, redis 5, mariadb
* generate ssl cert (self signed) if nextcloud\_use\_https is true
* follow best practices, performance tuning
* Nextcloud's updater.phar can be used to update the instance to the latest version

Requirements
------------

* currently only tested on centos 7.3 - 8.2

Role Variables
--------------

```yaml
nextcloud_domain: nextcloud.mydomain.com # domain used in nginx and nextcloud version (REQUIRED)
mysql_root_pw_modify: true # set to false if you do NOT want to modify the mysql root password
mysql_root_pw: secret # root password for mysql
nextcloud_repo_url: https://download.nextcloud.com/server/releases # where to get the nextcloud archive
nextcloud_version: latest-18 # version to install, choose any from https://download.nextcloud.com/server/releases/ without the file extension (default: latest)
php_version: "7.4" # PHP version to install (default: "7.3")
mariadb_version: "10.4" # MariaDB version to install (default: "10.4")
nextcloud_use_https: true # set to false if you want to run your instance behind a loadbalancer with ssl-termination
nextcloud_ssl_cert: /etc/nginx/nextcloud.crt # ssl cert path
nextcloud_ssl_key: /etc/nginx/nextcloud.key # ssl key path
nextcloud_ssl_skip_gen: false # set to true if you do NOT want role to handle ssl cert generation (then you must provide nextcloud_ssl_* configured files)
nextcloud_ssl_subject: '/C=CH/ST=Lucerne/L=Lucerne/CN={{ nextcloud_domain }}' # subject for self-signed ssl cert generation
nextcloud_web_root: /var/www/nextcloud # web root
nextcloud_data_root: '/nextcloud/data'
nextcloud_admin_user: admin # nextcloud admin username
nextcloud_admin_pw: admin # nextcloud admin password
nextcloud_mysql_db: nextcloud # name of nextcloud mysql db
nextcloud_mysql_user: nextcloud # username for nextcloud mysql db
nextcloud_mysql_pw: nextcloud  # password for nextcloud mysql db
nextcloud_hsts_options: max-age=15768000; includeSubDomains; preload; # if set, hsts will be enabled with the given options
nextcloud_upgrade: false # if set to true, nextcloud's updater.phar is run to upgrade nextcloud to the latest version
nextcloud_max_upload_size: 16G # max upload size
nextcloud_max_upload_time: 3600 # max upload time
nextcloud_upload_tmp_dir: /nextcloud/tmp # php tmp directory
nextcloud_http_port: 80 # http port
nextcloud_https_port: 443 # https port
nextcloud_php_memory_limit: 512M # memory_limit in php.ini
nextcloud_manage_yum_repos: true # configure epel, Remi and MariaDB yum repositories
nextcloud_config_options: # additional options to set in config.php
 - { option: overwrite.cli.url, value: "'https://nextcloud.example.com'" }
 - { option: mail_smtpmode, value: "'smtp'" }
 - { option: mail_smtpsecure, value: "'ssl'" }
 - { option: mail_domain, value: "'gmail'" }
 - { option: mail_smtphost, value: "'smtp.gmail.com'" }
 - { option: mail_from_address, value: "'john.smith'" }
 - { option: mail_smtpauthtype, value: "'LOGIN'" }
 - { option: mail_smtpauth, value: 1 }
 - { option: mail_smtpport, value: "'465'" }
 - { option: mail_smtpname, value: "'john.smith'" }
 - { option: mail_smtppassword, value: "'secret123'" }
nextcloud_crypto_config: intermediate  # modern, intermediate or old crypto config

```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
      - { role: rbicker.nextcloud, nextcloud_domain: nextcloud.mydomain.com }
```

License
-------

MIT
