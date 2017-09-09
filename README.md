Ansible Consul Role
===================

This is a simple Ansible Role that installs the Hashicorp Consul agent in client or server configuration.
The role permits to enable the Consul UI. It creates the data and configuration directory for Consul.

Requirements
------------

The role requires a RHEL-like distribution. It's been tested on the following stack:

* CentOS 7
* Ansible 2.3
* Consul 0.9.3

Role Variables
--------------

The role uses the variables defined in this source:

* defaults/main.yml

All the variables are the prefix consul_


```
consul_version: "0.9.3"
```
 - Consul version to install
 - Default: 0.9.3

```
consul_archive: "consul_{{ consul_version }}_linux_amd64.zip"
```
 - Consul installation distribution filename
 - Default: consul_0.9.3_linux_amd64.zip

```
consul_repo_url: "https://releases.hashicorp.com/consul/{{ consul_version }}/{{ consul_archive }}"
```

 - Consul distribution file download URL
 - Default: https://releases:hashicorp.com/consul/0.9.3/consul_0.9.3_linux_amd64.zip


```
consul_user: "consul"
consul_group: "consul"
```

 - Consul user/group
 - Default: consul

```
consul_install_path: "/opt/consul"
```
 - Base Binary installation path
 - Default: /opt/consul

```
consul_bin: "/usr/bin/consul"
```
 - Consul binary file
 - Default: /usr/bin/consul

```
consul_datacenter: "dc1"
```
 - Consul datacenter name
 - Default: dc1

```
consul_data_dir: "/var/lib/consul"
```
 - Data path as defined in [data_dir or -data-dir](https://www.consul.io/docs/agent/options.html#_data_dir)
 - Default: /var/lib/consul

```
consul_conf_dir: "/etc/consul.d/"
```
 - Additional configuration path
 - Default: /etc/consul.d

```
consul_is_server: true
```
 - Specifies if the agent is in server or client mode
 - Default: server mode

```
consul_ui_enabled: true
```
 - Specifies if the web ui is enabled or not
 - Default: Yes

```
consul_client_addr: "0.0.0.0"
```
 - Client address
 - Defatul: 0.0.0.0

```
consul_bind_addr: "{{ ansible_ssh_host }}"
```
 - The interface address to bind to
 - Default value: dynamic from hosts inventory

```
consul_cleanup: true
```
 - Remove distribution file and temporary files after installation
 - Default: true

```
consul_cluster:
  servers: [ "{{ consul_bind_addr }}" ]
  clients: []
```
 - List of server nodes
 - Default: itself

Example Playbook
----------------

```
---
- hosts: localhost
  remote_user: root
  connection: local
  become: true
  roles:
    - { role: ansible_role_consul, consul_bind_addr: ansible_eth1.ipv4.address }

```

License
-------

BSD

Author Information
------------------

Mauro Medda aka deftunix < medda.mauro at gmail dot com >

Inspired to the work of [Brian Shumate](https://galaxy.ansible.com/brianshumate/consul/)
