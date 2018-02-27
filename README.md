# Ansible Roles

[![build status](https://travis-ci.org/escapace/ansible-roles.svg?branch=master)](https://travis-ci.org/escapace/ansible-roles)
[![license](https://img.shields.io/github/license/escapace/ansible-roles.svg)](<>)

Production ready, continuously tested collection of [Ansible](https://ansible.com) roles targeting
Centos and RHEL operating systems.

-   Python 3 support
-   Namespaced role variables
-   Continously tested on Docker, AWS EC2 and baremetal \[[1](https://travis-ci.org/escapace/ansible-roles),[2](https://travis-ci.org/escapace/stack "Travis CI")]

## Roles

- [docker](#docker)
- [dotfiles](#dotfiles)
- [duo_unix](#duo_unix)
- [epel](#epel)
- [ferm](#ferm)
- [logrotate](#logrotate)
- [lvm](#lvm)
- [ntp](#ntp)
- [packagecloud](#packagecloud)
- [ssh](#ssh)
- [sudo](#sudo)
- [tunnelbroker](#tunnelbroker)
- [unnatended upgrades](#unnatended-upgrades)
- [virtualbox](#virtualbox)

## docker

Docker configuration tailored for the enterprise linux operating system.

-   Docker best practices and guidelines 
-   Support for docker community and enterprise edition
-   Devicemapper storage driver with thinly provisioned logical volumes \[[3](https://docs.docker.com/storage/storagedriver/select-storage-driver/ "Docker storage driver documentation")]
-   Systemd execution order tailored for network mounted block storage

### Installation

```sh
$ ansible-galaxy install escapace.docker
```

### Variables

| Variable                      |      Default      | Description                                        |
| ----------------------------- | :---------------: | -------------------------------------------------- |
| `docker_lvm_data_volume_size` |      `95%VG`      | Docker LVM volume size                             |
| `docker_volume_name`          |      `docker`     | Docker LVM volume name                             |
| `docker_volume_group_name`    |     `default`     | Docker LVM volume group name                       |
| `docker_icc_enabled`          |      `false`      | Docker inter-containter networking                 |
| `docker_ipv4_cidr`            |  `192.168.0.0/16` | Docker IPv4 network CIDR                           |
| `docker_ipv6_enabled`         |      `false`      | Docker IPv6 support                                |
| `docker_ipv6_cidr`            | `2001:db8:1::/64` | Docker IPv6 network CIDR                           |
| `docker_edition`              |        `ce`       | Docker edition                                     |
| `docker_gc_install`           |       `true`      | Docker garbage collection of containers and images |
| `docker_selinux_enabled`      |       `true`      | Docker SELinux support                             |

## dotfiles

Drop-in user-space, user-agnostic zsh; tmux; git &c configuration. \[[4](https://github.com/l5x/dotfiles "dotfiles github repository"),[5](https://github.com/l5x/vim "vim dotfiles github repository")]

### Installation

```sh
$ ansible-galaxy install escapace.dotfiles
```

### Variables

| Variable                              | Default | Description                        |
| ------------------------------------- | :-----: | ---------------------------------- |
| `dotfiles_username`                   |         | Username                           |
| `dotfiles_key`                        |         | OpenSSH publick key                |
| `dotfiles_keyboard_interactive_group` |         | OpenSSH keyboard interactive group |

## duo_unix

Two factor, keyboard interactive OpenSSH and PAM authentication for users in a predefined group. \[[6](https://duo.com/docs/duounix "Duo Unix ")]

### Installation

```sh
$ ansible-galaxy install escapace.duo_unix
```

### Variables

| Variable                |  Default | Description                                          |
| ----------------------- | :------: | ---------------------------------------------------- |
| `duo_unix_duo_ikey`     |          | Duo Security integration key                         |
| `duo_unix_duo_skey`     |          | Duo Security secret key                              |
| `duo_unix_duo_host`     |          | Duo Security API hostname                            |
| `duo_unix_groups`       |          | Comma-separated list of groups                       |
| `duo_unix_duo_pushinfo` |   `no`   | Include information in the Duo Push message          |
| `duo_unix_duo_failmode` | `secure` | fail “safe” (allow access) or “secure” (deny access) |
| `duo_unix_duo_prompts`  |    `3`   | Maximum number of prompts before denying access      |
| `duo_unix_autopush`     |   `no`   | automatically send a push login request              |

## epel

Ansible role for the extra packages for enterprise linux repository. \[[7](https://fedoraproject.org/wiki/EPEL "EPEL")]

### Installation

```sh
$ ansible-galaxy install escapace.epel
```

| Variable   |                                  Default                                 | Description                |
| ---------- | :----------------------------------------------------------------------: | -------------------------- |
| `epel_url` | `https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm` | `epel-release` package url |

## ferm

Ansible role for ferm \[[8](http://ferm.foo-projects.org "ferm")] iptables manager. Includes sensible systemctl defaults and implementation of the recommendations for filtering ICMPv6 messages (RFC4890) \[[9](https://www.ietf.org/rfc/rfc4890.txt "Recommendations for Filtering ICMPv6 Messages in Firewalls")]

### Installation

```sh
$ ansible-galaxy install escapace.ferm
```

### Variables

| Variable               | Default | Description                  |
| ---------------------- | :-----: | ---------------------------- |
| `ferm_ipv4_forwarding` |   `1`   | Enable IPv4 forwarding       |
| `ferm_ipv6_forwarding` |   `1`   | Enable IPv6 forwarding       |
| `ferm_ipv6_accept_ra`  |   `0`   | Accept router advertisements |

## logrotate

Log file automatic rotation, compression and removal.

### Installation

```sh
$ ansible-galaxy install escapace.logrotate
```

## lvm

A declarative LVM partitioner solution. The partition layout is described in a declarative manner which is then processed on startup by the storage setup service effectively reconciling the configuration state with the actual partitioning layout.

### Installation

```sh
$ ansible-galaxy install escapace.lvm
```

### Variables

| Variable                |  Default  | Description                         |
| ----------------------- | :-------: | ----------------------------------- |
| `lvm_volume_group_name` | `default` | Volume group name                   |
| `lvm_physical_device`   |           | Physical device such as `/dev/xvdb` |

## ntp

Ansible role for the chrony \[[10](https://chrony.tuxfamily.org "chrony")] network time protocol daemon.

### Installation

```sh
$ ansible-galaxy install escapace.ntp
```

### Variables

| Variable             |  Default | Description                                    |
| -------------------- | :------: | ---------------------------------------------- |
| `ntp_server_options` | `iburst` | Server options                                 |
| `ntp_stratumweight`  |  `0.001` | How important is stratum when selecting source |

## packagecloud

Ansible role for the escapace’s software repository. \[[11](https://github.com/escapace/rpmbuild "escapace’s rpmbuild"),[12](https://packagecloud.io/escapace/stack/ "packagecloud repository")]

### Installation

```sh
$ ansible-galaxy install escapace.packagecloud
```

## ssh

Ansible role for OpenSSH configuration implementing Mozilla’s OpenSSH security guidelines \[[13](https://infosec.mozilla.org/guidelines/openssh "Mozilla’s OpenSSH security guidelines ")] and support for optional keyboard interactive authentication.

### Installation

```sh
$ ansible-galaxy install escapace.ssh
```

### Variables

| Variable                         |      Default      | Description                        |
| -------------------------------- | :---------------: | ---------------------------------- |
| `ssh_keyboard_interactive_group` | `kbd-interactive` | OpenSSH keyboard interactive group |

## sudo

Ansible role implementing sensible sudo defaults.

### Installation

```sh
$ ansible-galaxy install escapace.sudo
```

## tunnelbroker

Ansible role for Hurricane Electric’s IPv6 tunnel broker.

### Installation

```sh
$ ansible-galaxy install escapace.tunnelbroker
```

### Variables

| Variable                   | Default | Description                                  |
| -------------------------- | :-----: | -------------------------------------------- |
| `tunnelbroker_interface`   |  `sit1` | Network interface name                       |
| `tunnelbroker_defaultgw`   |  `true` | Route all IPv6 traffic through tunnel broker |
| `tunnelbroker_client_ipv6` |         | Client IPv6 addresss with the mask           |
| `tunnelbroker_client_ipv6` |         | Server IPv4 address                          |
| `tunnelbroker_server_ipv6` |         | Server IPv6 address (without the mask)       |

## unnatended upgrades

Ansible role implementing unnatended security update policy.

### Installation

```sh
$ ansible-galaxy install escapace.unattended-upgrades
```

### Variables

| Variable                             |   Default  | Description                                                                                                                |
| ------------------------------------ | :--------: | -------------------------------------------------------------------------------------------------------------------------- |
| `unattended_upgrades_yum_update_cmd` | `security` | Update kind (default, security, security-severity:critical, minimal, minimal-security, minimal-security-severity:critical) |

## virtualbox

Ansible role for Oracle VM VirtualBox hypervisor.

### Installation

```sh
$ ansible-galaxy install escapace.virtualbox
```

### Variables

| Variable             | Default | Description        |
| -------------------- | :-----: | ------------------ |
| `virtualbox_version` |  `5.1`  | VirtualBox version |

# License

This software is released under the terms of the Apache-2.0 license.

This software includes or is derivative of works listed below. Please refer to
the specific files and/or packages for more detailed information about the
authors, copyright notices, and licenses.

-   [mantl](https://github.com/mantl/mantl) Copyright © 2015 Cisco Systems, Inc.
