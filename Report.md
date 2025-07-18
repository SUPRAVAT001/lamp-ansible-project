lamp-ansible-project/
├── inventory
├── lamp-setup.yml
├── Jenkinsfile
├── roles/
│   ├── apache/
│   │   └── tasks/main.yml
│   ├── mysql/
│   │   └── tasks/main.yml
│   └── php/
│       └── tasks/main.yml
└── report.md

# inventory
localhost ansible_connection=local

# lamp-setup.yml
- hosts: localhost
  become: true
  roles:
    - apache
    - mysql
    - php

# roles/apache/tasks/main.yml
- name: Install Apache
  apt:
    name: apache2
    state: present
    update_cache: yes

- name: Ensure Apache is running
  service:
    name: apache2
    state: started
    enabled: true

# roles/mysql/tasks/main.yml
- name: Install MariaDB Server
  apt:
    name: mariadb-server
    state: present
    update_cache: yes

- name: Ensure MariaDB is running
  service:
    name: mysql
    state: started
    enabled: true

# roles/php/tasks/main.yml
- name: Install PHP and required modules
  apt:
    name:
      - php
      - libapache2-mod-php
      - php-mysql
    state: present
    update_cache: yes

# Jenkinsfile
free style job


## Apache Version
apache2 -v

jenkins@DASH:/home/sdash/lamp-ansible-project$ apache2 -v
Server version: Apache/2.4.58 (Ubuntu)
Server built:   2025-04-03T14:36:49
```

## PHP Version
```
php -v

jenkins@DASH:/home/sdash/lamp-ansible-project$ php -v
PHP 8.3.6 (cli) (built: Jul 14 2025 18:30:55) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.3.6, Copyright (c) Zend Technologies
    with Zend OPcache v8.3.6, Copyright (c), by Zend Technologies
```
