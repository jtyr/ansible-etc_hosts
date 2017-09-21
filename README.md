etc_hosts
=========

Ansible role which contains a module that helps to manage the `/etc/hosts`
file.

This module was originally submitted as a
[PR](https://github.com/ansible/ansible/pull/19283) to Ansible but it was
refused.


Examples
--------

```
- name: Example how to use the etc_hosts module
  hosts: all
  roles:
    - hosts
  tasks:
    - name: Add a new record without alias
      etc_hosts:
        ip: 10.0.0.1
        hostname: some.domain1.com

    - name: Add a new record with hostname for the same IP
      etc_hosts:
        ip: 10.0.0.1
        hostname: some.domain2.com

    - name: Add a new record with another IP for the same hostname
      etc_hosts:
        ip: 10.0.0.2
        hostname: some.domain3.com

    - name: Add a new record with hostname and alias for the same IP
      etc_hosts:
        ip: 10.0.0.3
        hostname: some.domain3.com
        alias: some

    - name: Add a new record with multiple aliases
      etc_hosts:
        ip: 10.0.0.4
        hostname: some.domain4.com
        alias:
          - some
          - other

    - name: Update the list of aliases for the existing IP and hostname
      etc_hosts:
        ip: 10.0.0.4
        hostname: some.domain4.com
        alias:
          - some
          - other
          - alias

    - name: Remove all records with the specified IP
      etc_hosts:
        ip: 10.0.0.1
        state: absent

    - name: Remove all records with the specified hostname
      etc_hosts:
        hostname: some.domain3.com
        state: absent

    - name: Remove record with specified IP and hostname
      etc_hosts:
        ip: 10.0.0.4
        hostname: some.domain4.com
        state: absent
```


Installation
------------

The role can be downloaded either via Ansible Galaxy command:

```
$ ansible-galaxy install jtyr.hosts,master,hosts
```

or via Ansible Gallaxy requirements file:

```
$ cat ./requirements.yaml
---

- src: https://github.com/jtyr/ansible-hosts.git
  name: hosts
$ ansible-galaxy -r ./requirements.yaml
```

or via Git:

```
$ git clone https://github.com/jtyr/ansible-hosts.git hosts
```


License
-------

MIT


Author
------

Jiri Tyr
