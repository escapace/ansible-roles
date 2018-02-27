# Ansible Roles

[![build status](https://travis-ci.org/escapace/ansible-roles.svg?branch=master)](https://travis-ci.org/escapace/ansible-roles)
[![license](https://img.shields.io/github/license/escapace/ansible-roles.svg)](<>)

Production ready, continuously tested collection of [Ansible](https://ansible.com) roles targeting
Centos and RHEL operating systems.

-   Python 3 support
-   Namespaced role variables
-   Continously tested on Docker, AWS EC2 and baremetal \[[1](https://travis-ci.org/escapace/ansible-roles),[2](https://travis-ci.org/escapace/stack "Travis CI")]

## Table of Contents

-   [Roles](#roles)
    -   [dotfiles](#dotfiles)
    -   [docker](#docker)
    -   [duo_unix](#duo_unix)
    -   [epel](#epel)
    -   [ferm](#ferm)
    -   [logrotate](#logrotate)
    -   [lvm](#lvm)
    -   [ntp](#ntp)
    -   [packagecloud](#packagecloud)
    -   [ssh](#ssh)
    -   [sudo](#sudo)
    -   [tunnelbroker](#tunnelbroker)
    -   [unnatended upgrades](#unnatended-upgrades)
    -   [virtualbox](#virtualbox)
-   [License](#license)

## Roles

### dotfiles

Drop-in user-space, user-agnostic zsh; tmux; git &c configuration. \[[3](https://github.com/l5x/dotfiles "dotfiles github repository"),[4](https://github.com/l5x/vim "vim dotfiles github repository")]

### docker

Docker configuration tailored for the enterprise linux operating system.

-   Docker best practices and guidelines 
-   Support for docker community and enterprise edition
-   Devicemapper storage driver with thinly provisioned logical volumes \[[5](https://docs.docker.com/storage/storagedriver/select-storage-driver/ "Docker storage driver documentation")]
-   Systemd execution order tailored for network mounted block storage

### duo_unix

Two factor, keyboard interactive OpenSSH and PAM authentication for users in a predefined group. \[[6](https://duo.com/docs/duounix "Duo Unix ")]

### epel

Ansible role for the extra packages for enterprise linux repository. \[[7](https://fedoraproject.org/wiki/EPEL "EPEL")]

### ferm

Ansible role for ferm \[[8](http://ferm.foo-projects.org "ferm")] iptables manager. Includes sensible systemctl defaults and implementation of the recommendations for filtering ICMPv6 messages (RFC4890) \[[9](https://www.ietf.org/rfc/rfc4890.txt "Recommendations for Filtering ICMPv6 Messages in Firewalls")]

### logrotate

Log file automatic rotation, compression and removal.

### lvm

A declarative LVM partitioner solution. The partition layout is described in a declarative manner which is then processed on startup by the storage setup service effectively reconciling the configuration state with the actual partitioning layout.

### ntp

Ansible role for the chrony \[[10](https://chrony.tuxfamily.org "chrony")] network time protocol daemon.

### packagecloud

Ansible role for the escapace’s software repository. \[[11](https://github.com/escapace/rpmbuild "escapace’s rpmbuild"),[12](https://packagecloud.io/escapace/stack/ "packagecloud repository")]

### ssh

Ansible role for OpenSSH configuration implementing Mozilla’s OpenSSH security guidelines \[[13](https://infosec.mozilla.org/guidelines/openssh "Mozilla’s OpenSSH security guidelines ")] and support for optional keyboard interactive authentication.

### sudo

Ansible role implementing sensible sudo defaults.

### tunnelbroker

Ansible role for Hurricane Electric’s IPv6 tunnel broker.

### unnatended upgrades

Ansible role implementing unnatended security update policy.

### virtualbox

Ansible role for Oracle VM VirtualBox hypervisor.

## License

This software is released under the terms of the Apache-2.0 license.

This software includes or is derivative of works listed below. Please refer to
the specific files and/or packages for more detailed information about the
authors, copyright notices, and licenses.

-   [mantl](https://github.com/mantl/mantl) Copyright © 2015 Cisco Systems, Inc.
