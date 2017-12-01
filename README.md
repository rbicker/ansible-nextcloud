rbicker.nextcloud
=================

* install nextcloud (12) on centos 7
* install dependencies: nginx, php7.1, redis, mariadb
* generate ssl cert (self signed) if nextcloud\_use\_https is true
* follow best practises, performance tuning 

Important:
* php version has been upgraded from 7.0 to 7.1, if you would like to update a server which has been installed by an older version of this role, run "yum remove -y php70w\*"
* upgrading nextcloud was removed from this role

Requirements
------------

* Currently only tested with centos 7.4

Role Variables
--------------

```
nextcloud_domain: nextcloud.mydomain.com # domain used in nginx and nextcloud version (REQUIRED)
mysql_root_pw: secret # root password for 
nextcloud_repo_url: https://download.nextcloud.com/server/releases # where to get the nextcloud archive
nextcloud_version: 12.0.2 # version to install
nextcloud_use_https: true # set to false if you want to run your instance behind a loadbalancer with ssl-termination
nextcloud_ssl_cert: /etc/nginx/nextcloud.crt # self-signed ssl cert path
nextcloud_ssl_key: /etc/nginx/nextcloud.key # ssl key path
nextcloud_ssl_skip_gen: false # set to true if you do NOT want role to handle ssl cert generation (then you must provide nextcloud_ssl_* configured files)
nextcloud_ssl_subject: '/C=CH/ST=Lucerne/L=Lucerne/O=/CN={{ nextcloud_domain }}' # subject for ssl cert
nextcloud_working_dir: /nextcloud # directory for storing scripts
nextcloud_web_root: /var/www/nextcloud # web root 
nextcloud_data_root: '{{ nextcloud_working_dir }}/data'
nextcloud_backup_dir: '{{ nextcloud_working_dir }}/backup'
nextcloud_admin_user: admin # nextcloud admin username
nextcloud_admin_pw: admin # nextcloud admin password
nextcloud_mysql_db: nextcloud # name of nextcloud mysql db
nextcloud_mysql_user: nextcloud # username for nextcloud mysql db
nextcloud_mysql_pw: nextcloud  # password for nextcloud mysql db
nextcloud_hsts_options: max-age=15768000; includeSubDomains; preload; # if set, hsts will be enabled with the given options

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

