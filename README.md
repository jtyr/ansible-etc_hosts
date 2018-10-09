etc_hosts
=========

Ansible role which helps to manage the `/etc/hosts` file.

Module used by this role was originally submitted as a
[PR](https://github.com/ansible/ansible/pull/19283) to Ansible but it was
refused.


Examples
--------

```yaml
- name: Example how to use the etc_hosts role
  hosts: all
  vars:
    etc_hosts:
      # Add simple record
      - ip: 10.0.0.2
        hostname: some.domain3.com
      # Add record with aliases
      - ip: 10.0.0.4
        hostname: some.domain4.com
        alias:
          - some
          - other
          - alias
      # Remove record
      - ip: 10.0.0.4
        hostname: some.domain4.com
        state: absent
  roles:
    - etc_hosts

- name: Example how to use the etc_hosts module in standalone mode
  hosts: all
  roles:
    - etc_hosts
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

```shell
$ ansible-galaxy install jtyr.etc_hosts,master,etc_hosts
```

or via Ansible Gallaxy requirements file:

```shell
$ cat ./requirements.yaml
---

- src: https://github.com/jtyr/ansible-etc_hosts.git
  name: etc_hosts
$ ansible-galaxy -r ./requirements.yaml
```

or via Git:

```shell
$ git clone https://github.com/jtyr/ansible-etc_hosts.git etc_hosts
```


License
-------

MIT


Author
------

Jiri Tyr
