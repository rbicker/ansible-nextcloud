rbicker.nextcloud
=================

* install nextcloud (13) on centos 7
* install dependencies: nginx, php7.1, redis, mariadb
* generate ssl cert (self signed) if nextcloud\_use\_https is true
* follow best practises, performance tuning 
* Nextcloud's updater.phar can be used to update the instance to the latest version


Requirements
------------

* Currently only tested with centos 7.4

Role Variables
--------------

```
nextcloud_domain: nextcloud.mydomain.com # domain used in nginx and nextcloud version (REQUIRED)
mysql_root_pw: secret # root password for 
nextcloud_repo_url: https://download.nextcloud.com/server/releases # where to get the nextcloud archive
nextcloud_version: 13.0.0 # version to install
nextcloud_use_https: true # set to false if you want to run your instance behind a loadbalancer with ssl-termination
nextcloud_ssl_cert: /etc/nginx/nextcloud.crt # self-signed ssl cert path
nextcloud_ssl_key: /etc/nginx/nextcloud.key # ssl key path
nextcloud_ssl_skip_gen: false # set to true if you do NOT want role to handle ssl cert generation (then you must provide nextcloud_ssl_* configured files)
nextcloud_ssl_subject: '/C=CH/ST=Lucerne/L=Lucerne/O=/CN={{ nextcloud_domain }}' # subject for ssl cert
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
nextcloud_manage_yum_repos: true # configure epel & webtatic yum repositories
```

Example Playbook
----------------

```
- hosts: servers
  roles:
      - { role: rbicker.nextcloud, nextcloud_domain: nextcloud.mydomain.com }
```

License
-------

BSD

