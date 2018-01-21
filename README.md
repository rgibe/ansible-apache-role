## Overview

This is an "*ansible role*" to manage [Apache HTTP Server](http://httpd.apache.org/): installation and configuration.

I tried to keep it as simple as I can

~~~
ansible-apache-role]$ tree
.
├── defaults
│   └── main.yml
├── handlers
│   └── main.yml
├── README.md
├── tasks
│   └── main.yml
├── templates
│   └── apache
│       ├── conf-enabled
│       │   ├── htaccess.conf
│       │   ├── ratelimit.conf
│       │   ├── ssl.conf
│       │   └── status.conf
│       └── sites-enabled
│           ├── vhproxy.conf.j2
│           └── vhredirect.conf.j2
└── vars
    └── main.yml
~~~

## Tested on

Debian/Ubuntu

## Usage

You can try it with a playbook like this

~~~
$> more apacheSetup.yml
---
---
- name: Setup Apache and VHs
  hosts: host1
  tasks:
    - name: install apt packages
      apt: name={{ item }} update_cache=yes cache_valid_time=3600
      become: true
      with_items:
        - curl
    - name: install and configure Apache (HTTPD)
      include_role:
        name: ansible-apache-role
~~~

Directory hierarchy

~~~
$ tree -L 5
.
├── ansible.cfg
├── hosts
└── playbooks
    └── apacheSetup
        ├── apacheSetup.yml
        └── roles
            └── ansible-apache-role
~~~

**RUN**:
ansible-playbook playbooks/apacheSetup/apacheSetup.yml
