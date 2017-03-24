rbicker.nextcloud
=================

* install or upgrade nextcloud on centos 7
* install dependencies: nginx, php7, redis, mariadb
* generate ssl cert (self signed)
* follow best practises, performance tuning 


Requirements
------------

* Currently only tested with centos 7.3

Role Variables
--------------

```
nextcloud_domain: nextcloud.mydomain.com # domain used in nginx and nextcloud version (REQUIRED)
mysql_root_pw: secret # root password for 
nextcloud_repo_url: https://download.nextcloud.com/server/releases # where to get the nextcloud archive
nextcloud_version: 11.0.2 # version to install (or upgrade to)
nextcloud_ssl_cert: /etc/nginx/nextcloud.crt # ssl cert path
nextcloud_ssl_key: /etc/nginx/nextcloud.key # ssl key path
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
nextcloud_upgrade: false # upgrade instance if given nextcloud_version does not match the installed version
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

