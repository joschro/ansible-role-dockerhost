Dockerhost
==========

Ansible role to set up a Raspberry Pi 2 as a Docker host running on CentOS 7.

Requirements
------------

A Raspberry Pi 2 (the one with 1GB RAM), and the latest CentOS 7 image for the Raspberry Pi 2, available from
```
http://mirror.centos.org/altarch/7/isos/armhfp/
```
(e.g. CentOS-Userland-7-armv7hl-Minimal-1511-RaspberryPi2.img.xz)

This compressed image needs to be extracted and written to an empty SD card (all existing data will be overwritten!), e.g. with
```
xz -cd <path-to-directory-containing-the-image>/CentOS-Userland-7-armv7hl-Minimal-1511-RaspberryPi2.img.xz | dd of=/dev/mmcblk0 bs=4M
```
if /dev/mmcblk0 is the SD card device; make sure to have umounted all partitions on the SD card!

Place the SD card into the Raspberry Pi 2, make sure a keyboard is connected, a network cable and a screen as well, and power it up. After the initial boot, login with
```
rpi2 login: root
Password: centos
```
Run
```
ip add sh eth0
```
and note the IP address next to the line beginning with "inet".

Copy your SSH key to the Raspberry using this IP address
```
ssh-copy-id root@<ipaddress>
```
you may need to remove the line beginning with this IP address in ~/.ssh/known_hosts in case you already have ssh'ed to this IP address before.

Role Variables
--------------

None right now.

Dependencies
------------

None right now.

Example Playbook
----------------
```
- name: Deploy a docker host
  hosts: dockerhosts
  remote_user: root

  roles:
    - dockerhost
```
with an inventory file like this for example:
```
[dockerhosts]
dockerhost ansible_ssh_host=<above-ip-address> ansible_ssh_user=root
```

License
-------

GPLv3

Author Information
------------------

Joachim Schröder, jos (at) redhat.com
