# Debian/Ubuntu Backports with Ansible

[![Ansible Role: jnv.debian-backports](https://img.shields.io/ansible/role/224.svg?style=flat-square)](https://galaxy.ansible.com/jnv/debian-backports)

Adds backports repository for Debian and Ubuntu.

**Note for Debian users:** Debian provides backports [only for the latest stable version](https://backports.debian.org/news/stretch-backports/).

## Usage

Install via [Galaxy](https://galaxy.ansibleworks.com/):

```
ansible-galaxy install jnv.debian-backports
```

In your playbook:

```yaml
- hosts: all
  roles:
    # ...
    - jnv.debian-backports
```

The role uses [apt_repository module](http://docs.ansible.com/apt_repository_module.html) which has additional requirements.

You can use `default_release` option for [apt module](http://docs.ansible.com/apt_module.html) to install package from backports. For example:

```yaml
tasks:
  - apt: name=mosh state=present default_release={{ansible_distribution_release}}-backports
```

`ansible_distribution_release` variable contains release name, i.e. `precise` or `wheezy`.

## Variables

- `backports_uri`: URI of the backports repository; change this if you want to use a particular mirror.
    + Debian: `http://ftp.debian.org/debian`
    + Ubuntu: `http://archive.ubuntu.com/ubuntu`
- `backports_components`: Release and components for sources.list
    + Debian: `{{backports_distribution}}-backports backports main contrib non-free`
    + Ubuntu: `{{backports_distribution}}-backports main restricted universe multiverse`
