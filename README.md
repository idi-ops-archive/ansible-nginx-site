Ansible Nginx Site
==================

Deloys a site file for Nginx

Requirements
------------

nginx-common

Role Variables
--------------

* `nginx_sites`:  list of site files

Each site file should be configured with the following variables:

  * `port`: port to listen
  * `domains`: list of domains for the virtual server
  * `setup`: list of configu chunks to add to the file

Example Playbook
----------------

```
---
- hosts: localhost
  become: yes
  roles:
    - role: nginx-common
    - role: nginx-site
          nginx_sites:
            - name: mysite
              port: 80
              domains:
                - localhost
                - mysite.com
              setup:
                - "root /var/www/"
                - "client_max_body_size 128M"
                - "location / { index index.html; }"
                - "access_log  /var/log/nginx/mysite-access.log main"
                - "error_log /var/log/nginx/mysite-error.log warn"

```    
